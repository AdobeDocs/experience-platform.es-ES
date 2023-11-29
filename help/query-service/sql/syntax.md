---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;sintaxis sql;sql;ctas;CTAS;Crear tabla como seleccionar
solution: Experience Platform
title: Sintaxis SQL en el servicio de consultas
description: Este documento muestra la sintaxis SQL admitida por Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 1e9d6b0c43461902c5b966aa1d0576103e872e0c
workflow-type: tm+mt
source-wordcount: '4134'
ht-degree: 2%

---

# Sintaxis SQL en el servicio de consultas

El servicio de consultas de Adobe Experience Platform permite utilizar ANSI SQL estándar para `SELECT` instrucciones y otros comandos limitados. Este documento describe la sintaxis SQL admitida por [!DNL Query Service].

## SELECCIONAR consultas {#select-queries}

La siguiente sintaxis define un `SELECT` consulta admitida por [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

donde `from_item` puede ser una de las siguientes opciones:

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

y `grouping_element` puede ser una de las siguientes opciones:

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

y `with_query` es:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

Las siguientes subsecciones proporcionan detalles sobre cláusulas adicionales que puede utilizar en sus consultas, siempre que sigan el formato descrito anteriormente.

### Cláusula SNAPSHOT

Esta cláusula se puede utilizar para leer de forma incremental los datos de una tabla en función de los ID de instantánea. Un ID de instantánea es un marcador de punto de comprobación representado por un número de tipo Long que se aplica a una tabla de lago de datos cada vez que se escriben datos en ella. El `SNAPSHOT` se adjunta a la relación de tabla a la que se utiliza junto.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Ejemplo

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Tenga en cuenta que `SNAPSHOT` La cláusula funciona con una tabla o alias de tabla, pero no sobre una subconsulta o vista. A `SNAPSHOT` funcionará en cualquier lugar a `SELECT` se puede aplicar una consulta en una tabla.

Además, puede utilizar `HEAD` y `TAIL` como valores de desplazamiento especiales para cláusulas de instantánea. Uso de `HEAD` hace referencia a un desplazamiento antes de la primera instantánea, mientras que `TAIL` hace referencia a un desplazamiento después de la última instantánea.

>[!NOTE]
>
>Si está realizando una consulta entre dos ID de instantánea y la instantánea de inicio ha caducado, pueden producirse los dos escenarios siguientes, dependiendo de si el indicador de comportamiento de reserva opcional (`resolve_fallback_snapshot_on_failure`) se ha definido:
>
>- Si se establece el indicador de comportamiento de reserva opcional, el servicio de consultas seleccionará la instantánea disponible más antigua, la definirá como instantánea de inicio y devolverá los datos entre la instantánea disponible más antigua y la instantánea de finalización especificada. Estos datos son **inclusivo** de la instantánea más antigua disponible.
>
>- Si no se establece el indicador de comportamiento de reserva opcional, se devuelve un error.

### Cláusula WHERE

De forma predeterminada, las coincidencias producidas por un `WHERE` Cláusula sobre `SELECT` Las consultas distinguen entre mayúsculas y minúsculas. Si desea que las coincidencias distingan entre mayúsculas y minúsculas, puede utilizar la palabra clave `ILIKE` en lugar de `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La lógica de las cláusulas LIKE e ILIKE se explica en la siguiente tabla:

| Cláusa | Operador |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**Ejemplo**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Esta consulta devuelve clientes con nombres que comienzan por &quot;A&quot; o &quot;a&quot;.

### UNIRSE

A `SELECT` La consulta que utiliza uniones tiene la siguiente sintaxis:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT y EXCEPT

El `UNION`, `INTERSECT`, y `EXCEPT` Las cláusulas se utilizan para combinar o excluir como filas de dos o más tablas:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREAR TABLA COMO SELECCIÓN {#create-table-as-select}

La siguiente sintaxis define un `CREATE TABLE AS SELECT` Consulta (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE') ] AS (select_query)
```

| Parámetros | Descripción |
| ----- | ----- |
| `schema` | Título del esquema XDM. Utilice esta cláusula solo si desea utilizar un esquema XDM existente para el nuevo conjunto de datos creado por la consulta CTAS. |
| `rowvalidation` | (Opcional) Especifica si el usuario desea la validación a nivel de fila de cada lote nuevo introducido para el conjunto de datos recién creado. El valor predeterminado es `true`. |
| `label` | Cuando cree un conjunto de datos con una consulta CTAS, utilice esta etiqueta con el valor de `profile` para etiquetar el conjunto de datos como habilitado para el perfil. Esto significa que el conjunto de datos se marca automáticamente para el perfil a medida que se crea. Consulte el documento de extensiones de atributos derivadas para obtener más información sobre el uso de `label`. |
| `select_query` | A `SELECT` declaración. La sintaxis del `SELECT` La consulta se puede encontrar en la [sección SELECCIONAR consultas](#select-queries). |

**Ejemplo**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>El `SELECT` debe tener un alias para las funciones de agregado, como `COUNT`, `SUM`, `MIN`, etc. Además, la variable `SELECT` se puede proporcionar con o sin paréntesis (). Puede proporcionar un `SNAPSHOT` para leer los deltas incrementales en la tabla de destino.

## INSERTAR EN

El `INSERT INTO` El comando se define de la siguiente manera:

```sql
INSERT INTO table_name select_query
```

| Parámetros | Descripción |
| ----- | ----- |
| `table_name` | Nombre de la tabla en la que desea insertar la consulta. |
| `select_query` | A `SELECT` declaración. La sintaxis del `SELECT` La consulta se puede encontrar en la [sección SELECCIONAR consultas](#select-queries). |

**Ejemplo**

>[!NOTE]
>
>El siguiente es un ejemplo inventado y simplemente con fines educativos.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> El `SELECT` declaración **no debe** se incluirá entre paréntesis (). Además, el esquema del resultado del `SELECT` debe ajustarse a la de la tabla definida en la variable `INSERT INTO` declaración. Puede proporcionar un `SNAPSHOT` para leer los deltas incrementales en la tabla de destino.

La mayoría de los campos de un esquema XDM real no se encuentran en el nivel raíz y SQL no permite el uso de notación de puntos. Para lograr un resultado realista utilizando campos anidados, debe asignar cada campo en su `INSERT INTO` ruta.

Hasta `INSERT INTO` rutas anidadas, utilice la sintaxis siguiente:

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**Ejemplo**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## SOLTAR TABLA

El `DROP TABLE` El comando borra una tabla existente y elimina el directorio asociado a la tabla del sistema de archivos si no se trata de una tabla externa. Si la tabla no existe, se produce una excepción.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parámetros | Descripción |
| ------ | ------ |
| `IF EXISTS` | Si se especifica, no se produce ninguna excepción si la tabla no lo hace **no** existen. |

## CREAR BASE DE DATOS

El `CREATE DATABASE` crea una base de datos de Azure Data Lake Storage (ADLS).

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## SOLTAR BASE DE DATOS

El `DROP DATABASE` elimina la base de datos de una instancia.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parámetros | Descripción |
| ------ | ------ |
| `IF EXISTS` | Si se especifica, no se produce ninguna excepción si la base de datos **no** existen. |

## SOLTAR ESQUEMA

El `DROP SCHEMA` El comando borra un esquema existente.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parámetros | Descripción |
| ------ | ------ |
| `IF EXISTS` | Si se especifica, no se produce ninguna excepción si el esquema **no** existen. |
| `RESTRICT` | Valor predeterminado para el modo. Si se especifica, el esquema solo se borra si **no lo tiene** contiene cualquier tabla. |
| `CASCADE` | Si se especifica, el esquema se suelta junto con todas las tablas presentes en el esquema. |

## CREAR VISTA

La siguiente sintaxis define un `CREATE VIEW` consulta de un conjunto de datos. Este conjunto de datos puede ser un ADLS o un conjunto de datos de almacén acelerado.

```sql
CREATE VIEW view_name AS select_query
```

| Parámetros | Descripción |
| ------ | ------ |
| `view_name` | Nombre de la vista que se va a crear. |
| `select_query` | A `SELECT` declaración. La sintaxis del `SELECT` La consulta se puede encontrar en la [sección SELECCIONAR consultas](#select-queries). |

**Ejemplo**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

La siguiente sintaxis define un `CREATE VIEW` consulta que crea una vista en el contexto de una base de datos y un esquema.

**Ejemplo**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| Parámetros | Descripción |
| ------ | ------ |
| `db_name` | Nombre de la base de datos. |
| `schema_name` | Nombre del esquema. |
| `view_name` | Nombre de la vista que se va a crear. |
| `select_query` | A `SELECT` declaración. La sintaxis del `SELECT` La consulta se puede encontrar en la [sección SELECCIONAR consultas](#select-queries). |

**Ejemplo**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## MOSTRAR VISTAS

La siguiente consulta muestra la lista de vistas.

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## COLOCAR VISTA

La siguiente sintaxis define un `DROP VIEW` consulta:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parámetros | Descripción |
| ------ | ------ |
| `IF EXISTS` | Si se especifica, no se produce ninguna excepción si la vista sí lo hace **no** existen. |
| `view_name` | Nombre de la vista que se va a eliminar. |

**Ejemplo**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Bloque anónimo {#anonymous-block}

Un bloque anónimo consta de dos secciones: ejecutable y de control de excepciones. En un bloque anónimo, la sección ejecutable es obligatoria. Sin embargo, la sección de control de excepciones es opcional.

El siguiente ejemplo muestra cómo crear un bloque con una o más instrucciones que se van a ejecutar juntas:

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

A continuación se muestra un ejemplo con un bloque anónimo.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Instrucciones condicionales en un bloque anónimo {#conditional-anonymous-block-statements}

La estructura de control IF-THEN-ELSE permite la ejecución condicional de una lista de instrucciones cuando una condición se evalúa como TRUE. Esta estructura de control sólo es aplicable dentro de un bloque anónimo. Si esta estructura se utiliza como comando independiente, se produce un error de sintaxis (&quot;Comando no válido fuera de bloque anónimo&quot;).

El siguiente fragmento de código muestra el formato correcto para las instrucciones condicionales IF-THEN-ELSE en un bloque anónimo.

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**Ejemplo**

El ejemplo siguiente ejecuta `SELECT 200;`.

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

Esta estructura se puede utilizar en combinación con `raise_error();` para devolver un mensaje de error personalizado. El bloque de código que se muestra a continuación finaliza el bloque anónimo con &quot;mensaje de error personalizado&quot;.

**Ejemplo**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### Instrucciones IF anidadas

Las instrucciones IF anidadas se admiten en bloques anónimos.

**Ejemplo**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### Bloques de excepción

Los bloques de excepción son compatibles con los bloques anónimos.

**Ejemplo**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHER THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### Automático a JSON {#auto-to-json}

El servicio de consulta admite una configuración opcional de nivel de sesión para devolver campos complejos de nivel superior desde consultas SELECT interactivas como cadenas JSON. El `auto_to_json` Esta configuración permite devolver datos de campos complejos como JSON y luego analizarlos en objetos JSON mediante bibliotecas estándar.

ESTABLECER el indicador de funcionalidad `auto_to_json` como true antes de ejecutar la consulta SELECT que contiene campos complejos.

```sql
set auto_to_json=true; 
```

#### Antes de configurar el `auto_to_json` indicador

En la tabla siguiente se muestra un ejemplo de resultado de consulta antes de `auto_to_json` se aplica la configuración. En ambos casos se utilizó la misma consulta SELECT (como se ve a continuación) dirigida a una tabla con campos complejos.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

Los resultados son los siguientes:

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Después de configurar la variable `auto_to_json` indicador

En la tabla siguiente se muestra la diferencia en los resultados que `auto_to_json` La configuración de tiene en el conjunto de datos resultante. Se utilizó la misma consulta SELECT en ambos casos.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Resolver instantánea de reserva ante un error {#resolve-fallback-snapshot-on-failure}

El `resolve_fallback_snapshot_on_failure` se utiliza para resolver el problema de un ID de instantánea caducado. Los metadatos de la instantánea caducan al cabo de dos días y una instantánea caducada puede invalidar la lógica de un script. Esto puede suponer un problema al utilizar bloques anónimos.

Configure las variables `resolve_fallback_snapshot_on_failure` Opción verdadera para anular una instantánea con un ID de instantánea anterior.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

La siguiente línea de código anula la variable `@from_snapshot_id` con el más antiguo disponible `snapshot_id` de los metadatos.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## Organización de recursos de datos

Es importante organizar lógicamente los recursos de datos dentro del lago de datos de Adobe Experience Platform a medida que crezcan. El servicio de consultas amplía las construcciones SQL que permiten agrupar lógicamente los recursos de datos en una zona protegida. Este método de organización permite compartir recursos de datos entre esquemas sin necesidad de moverlos físicamente.

Se admiten las siguientes construcciones SQL con sintaxis SQL estándar para organizar lógicamente los datos.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Consulte la guía de [organización lógica de los recursos de datos](../best-practices/organize-data-assets.md) para obtener una explicación más detallada sobre las prácticas recomendadas del servicio de consultas.

## La tabla existe

El `table_exists` El comando SQL se utiliza para confirmar si existe o no una tabla en el sistema. El comando devuelve un valor booleano: `true` si la tabla **hace** existen, y `false` si la tabla tiene **no** existen.

Al validar si una tabla existe antes de ejecutar las instrucciones, la variable `table_exists` simplifica el proceso de escritura de un bloque anónimo para cubrir ambos `CREATE` y `INSERT INTO` casos de uso.

La siguiente sintaxis define la variable `table_exists` comando:

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## En línea {#inline}

El `inline` separa los elementos de una matriz de estructuras y genera los valores en una tabla. Solo se puede colocar en la `SELECT` lista o un `LATERAL VIEW`.

El `inline` función **no puede** se colocará en una lista de selección donde haya otras funciones del generador.

De forma predeterminada, las columnas producidas se denominan &quot;col1&quot;, &quot;col2&quot;, etc. Si la expresión es `NULL` a continuación, no se generan filas.

>[!TIP]
>
>Se puede cambiar el nombre de las columnas utilizando la variable `RENAME` comando.

**Ejemplo**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

El ejemplo devuelve lo siguiente:

```text
1  a Spark SQL
2  b Spark SQL
```

Este segundo ejemplo demuestra aún más el concepto y la aplicación del `inline` función. El modelo de datos del ejemplo se ilustra en la siguiente imagen.

![Diagrama de esquema para productListItems.](../images/sql/productListItems.png)

**Ejemplo**

```sql
select inline(productListItems) from source_dataset limit 10;
```

Los valores tomados del `source_dataset` se utilizan para rellenar la tabla de destino.

| SKU | _experiencia | cantidad | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;) | 5 | 10.5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;) |          |              |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] Comandos SQL

La subsección siguiente cubre los comandos SQL de Spark compatibles con el servicio de consultas.

### ESTABLECER

El `SET` establece una propiedad y devuelve el valor de una propiedad existente o enumera todas las propiedades existentes. Si se proporciona un valor para una clave de propiedad existente, se anula el valor antiguo.

```sql
SET property_key = property_value
```

| Parámetros | Descripción |
| ------ | ------ |
| `property_key` | El nombre de la propiedad que desea enumerar o modificar. |
| `property_value` | El valor como el que desea que se establezca la propiedad. |

Para devolver el valor de cualquier configuración, utilice `SET [property key]` sin un `property_value`.

## [!DNL PostgreSQL] comandos

Las subsecciones siguientes cubren las siguientes [!DNL PostgreSQL] comandos admitidos por el servicio de consultas.

### ANALIZAR TABLA {#analyze-table}

El `ANALYZE TABLE` realiza un análisis de distribución y cálculos estadísticos para la tabla o tablas con nombre. El uso de `ANALYZE TABLE` varía en función de si los conjuntos de datos se almacenan en la variable [almacén acelerado](#compute-statistics-accelerated-store) o el [lago de datos](#compute-statistics-data-lake). Consulte sus secciones respectivas para obtener más información sobre su uso.

#### ESTADÍSTICAS DE CÁLCULO en el almacén acelerado {#compute-statistics-accelerated-store}

El `ANALYZE TABLE` El comando calcula las estadísticas de una tabla en el almacén acelerado. Las estadísticas se calculan en consultas CTAS o ITAS ejecutadas para una tabla determinada del almacén acelerado.

**Ejemplo**

```sql
ANALYZE TABLE <original_table_name>
```

A continuación se muestra una lista de cálculos estadísticos disponibles después de utilizar el `ANALYZE TABLE` comando:-

| Valores calculados | Descripción |
|---|---|
| `field` | Nombre de la columna de una tabla. |
| `data-type` | El tipo de datos aceptable para cada columna. |
| `count` | Número de filas que contienen un valor no nulo para este campo. |
| `distinct-count` | El número de valores únicos o distintos para este campo. |
| `missing` | Número de filas que tienen un valor nulo para este campo. |
| `max` | El valor máximo de la tabla analizada. |
| `min` | El valor mínimo de la tabla analizada. |
| `mean` | El valor promedio de la tabla analizada. |
| `stdev` | La desviación estándar de la tabla analizada. |

#### ESTADÍSTICAS DE CÁLCULO en el lago de datos {#compute-statistics-data-lake}

Ahora puede calcular las estadísticas de nivel de columna de [!DNL Azure Data Lake Storage] Conjuntos de datos de (ADLS) con `COMPUTE STATISTICS` Comando SQL. Calcular las estadísticas de columna en todo el conjunto de datos, un subconjunto de un conjunto de datos, todas las columnas o un subconjunto de columnas.

`COMPUTE STATISTICS` amplía el `ANALYZE TABLE` comando. Sin embargo, la variable `COMPUTE STATISTICS`, `FILTERCONTEXT`, y `FOR COLUMNS` Los comandos de no son compatibles con las tablas de almacenamiento acelerado. Estas extensiones para `ANALYZE TABLE` Actualmente, los comandos solo son compatibles con tablas ADLS.

**Ejemplo**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

El `FILTER CONTEXT` El comando calcula las estadísticas de un subconjunto del conjunto de datos en función de la condición de filtro proporcionada. El `FOR COLUMNS` el comando segmenta columnas específicas para su análisis.

>[!NOTE]
>
>El `Statistics ID` y las estadísticas generadas solo son válidas para cada sesión y no se puede acceder a ellas en diferentes sesiones de PSQL.<br><br>Limitaciones:<ul><li>La generación de estadísticas no es compatible con los tipos de datos de matriz o asignación</li><li>Las estadísticas calculadas son **no** persistió entre sesiones.</li></ul><br><br>Opciones:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>De forma predeterminada, el indicador se establece en true. Como resultado, cuando se solicitan estadísticas sobre un tipo de datos no admitido, no se produce un error, pero omite silenciosamente los campos con tipos de datos no admitidos.<br>Para activar notificaciones de errores cuando se soliciten estadísticas sobre tipos de datos no admitidos, utilice: `SET skip_stats_for_complex_datatypes = false`.

La salida de la consola aparece como se ve a continuación.

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

A continuación, puede consultar las estadísticas calculadas directamente haciendo referencia al `Statistics ID`. La instrucción de ejemplo siguiente le permite ver el resultado en su totalidad cuando se utiliza con el `Statistics ID` o el nombre del alias. Para obtener más información acerca de esta función, consulte lo siguiente [documentación del nombre del alias](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Utilice el `SHOW STATISTICS` para mostrar los metadatos de todas las estadísticas temporales generadas en la sesión. Este comando puede ayudarle a refinar el ámbito del análisis estadístico.

```sql
SHOW STATISTICS;
```

A continuación se muestra un ejemplo de salida de SHOW STATISTICS.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Consulte la [documentación de estadísticas de conjuntos de datos](../key-concepts/dataset-statistics.md) para obtener más información.

#### TABLESAMPLE {#tablesample}

El servicio de consulta de Adobe Experience Platform proporciona conjuntos de datos de ejemplo como parte de sus capacidades aproximadas de procesamiento de consultas.
Las muestras de conjuntos de datos se utilizan mejor cuando no necesita una respuesta exacta para una operación de agregado sobre un conjunto de datos. Esta función le permite realizar consultas exploratorias más eficientes en conjuntos de datos grandes emitiendo una consulta aproximada para devolver una respuesta aproximada.

Los conjuntos de datos de muestra se crean con muestras aleatorias uniformes de las existentes [!DNL Azure Data Lake Storage] Conjuntos de datos de (ADLS), utilizando solo un porcentaje de registros del original. La función de ejemplo del conjunto de datos amplía la variable `ANALYZE TABLE` con el comando `TABLESAMPLE` y `SAMPLERATE` Comandos SQL.

En los ejemplos siguientes, la línea uno muestra cómo calcular una muestra del 5 % de la tabla. La línea dos muestra cómo calcular una muestra del 5 % a partir de una vista filtrada de los datos de la tabla.

**ejemplo**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

Consulte la [documentación de muestras de conjuntos de datos](../key-concepts/dataset-samples.md) para obtener más información.

### COMENZAR

El `BEGIN` o, alternativamente, el comando `BEGIN WORK` o `BEGIN TRANSACTION` , inicia un bloque de transacciones. Cualquier instrucción que se introduzca después del comando begin se ejecutará en una sola transacción hasta que se proporcione un comando COMMIT o ROLLBACK explícito. Este comando es el mismo que `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CERRAR

El `CLOSE` libera los recursos asociados con un cursor abierto. Una vez cerrado el cursor, no se permiten operaciones posteriores. Se debe cerrar un cursor cuando ya no sea necesario.

```sql
CLOSE name
CLOSE ALL
```

If `CLOSE name` se utiliza, `name` representa el nombre de un cursor abierto que debe cerrarse. If `CLOSE ALL` se utiliza, todos los cursores abiertos se cierran.

### DESASIGNAR

El `DEALLOCATE` permite anular la asignación de una instrucción SQL previamente preparada. Si no desasigna explícitamente una instrucción preparada, se desasigna cuando finaliza la sesión. Puede encontrar más información sobre las instrucciones preparadas en la [PREPARE, comando](#prepare) sección.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

If `DEALLOCATE name` se utiliza, `name` representa el nombre de la instrucción preparada que debe desasignarse. If `DEALLOCATE ALL` se utiliza, se desasignarán todas las instrucciones preparadas.

### DECLARAR

El `DECLARE` permite al usuario crear un cursor, que puede utilizarse para recuperar un pequeño número de filas de una consulta mayor. Una vez creado el cursor, se recuperan filas de él utilizando `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Parámetros | Descripción |
| ------ | ------ |
| `name` | Nombre del cursor que se va a crear. |
| `query` | A `SELECT` o `VALUES` comando que proporciona las filas que el cursor devolverá. |

### EJECUTAR

El `EXECUTE` se utiliza para ejecutar una instrucción preparada previamente. Dado que las declaraciones preparadas sólo existen durante un período de sesiones, la declaración preparada debe haber sido creada por un `PREPARE` se ejecutó anteriormente en la sesión actual. Puede encontrar más información sobre el uso de instrucciones preparadas en la [`PREPARE` mando](#prepare) sección.

Si la variable `PREPARE` que creó la instrucción especificó algunos parámetros, se debe pasar un conjunto de parámetros compatible a la instrucción `EXECUTE` declaración. Si no se pasan estos parámetros, se generará un error.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parámetros | Descripción |
| ------ | ------ |
| `name` | Nombre de la instrucción preparada que se va a ejecutar. |
| `parameter` | El valor real de un parámetro en la instrucción preparada. Debe ser una expresión que genere un valor compatible con el tipo de datos de este parámetro, tal como se determinó cuando se creó la instrucción preparada.  Si hay varios parámetros para la instrucción preparada, se separan con comas. |

### EXPLICAR

El `EXPLAIN` muestra el plan de ejecución de la instrucción suministrada. El plan de ejecución muestra cómo se analizarán las tablas a las que hace referencia la sentencia.  Si se hace referencia a varias tablas, se mostrará qué algoritmos de combinación se utilizan para reunir las filas necesarias de cada tabla de entrada.

```sql
EXPLAIN statement
```

Utilice el `FORMAT` palabra clave con `EXPLAIN` para definir el formato de la respuesta.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parámetros | Descripción |
| ------ | ------ |
| `FORMAT` | Utilice el `FORMAT` para especificar el formato de salida. Las opciones disponibles son `TEXT` o `JSON`. La salida no textual contiene la misma información que el formato de salida de texto, pero es más fácil de analizar para los programas. El valor predeterminado de este parámetro es `TEXT`. |
| `statement` | Cualquiera `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`, o `CREATE MATERIALIZED VIEW AS` , cuyo plan de ejecución desea ver. |

>[!IMPORTANT]
>
>Cualquier salida que `SELECT` La instrucción que podría devolver se descarta cuando se ejecuta con `EXPLAIN` palabra clave. Otros efectos secundarios de la declaración ocurren como de costumbre.

**Ejemplo**

En el siguiente ejemplo se muestra el plan para una consulta simple en una tabla con un único `integer` filas de columna y 10000:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### BUSCAR

El `FETCH` El comando recupera filas utilizando un cursor creado anteriormente.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parámetros | Descripción |
| ------ | ------ |
| `num_of_rows` | Número de filas que se van a recuperar. |
| `cursor_name` | El nombre del cursor desde el que recupera información. |

### PREPARAR {#prepare}

El `PREPARE` El comando permite crear una instrucción preparada. Una instrucción preparada es un objeto del lado del servidor que se puede utilizar para crear plantillas de instrucciones SQL similares.

Las instrucciones preparadas pueden tomar parámetros, que son valores que se sustituyen en la instrucción cuando se ejecuta. Se hace referencia a los parámetros por posición, utilizando $1, $2, etc., al utilizar instrucciones preparadas.

De forma opcional, puede especificar una lista de tipos de datos de parámetros. Si el tipo de datos de un parámetro no aparece en la lista, el tipo se puede inferir del contexto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parámetros | Descripción |
| ------ | ------ |
| `name` | Nombre de la instrucción preparada. |
| `data_type` | Los tipos de datos de los parámetros de la instrucción preparada. Si el tipo de datos de un parámetro no aparece en la lista, el tipo se puede inferir del contexto. Si necesita agregar varios tipos de datos, puede agregarlos en una lista separada por comas. |

### REVERSIÓN

El `ROLLBACK` El comando deshace la transacción actual y descarta todas las actualizaciones realizadas por la transacción.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECCIONAR EN

El `SELECT INTO` crea una nueva tabla y la rellena con datos calculados por una consulta. Los datos no se devuelven al cliente, como sucede con un `SELECT` comando. Las columnas de la nueva tabla tienen los nombres y tipos de datos asociados con las columnas de salida de la variable `SELECT` comando.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

Encontrará más información sobre los parámetros de consulta SELECT estándar en la [sección de consulta SELECT](#select-queries). Esta sección solo enumera los parámetros que son exclusivos de `SELECT INTO` comando.

| Parámetros | Descripción |
| ------ | ------ |
| `TEMPORARY` o `TEMP` | Un parámetro opcional. Si se especifica, la tabla que se crea será una tabla temporal. |
| `UNLOGGED` | Un parámetro opcional. Si se especifica, la tabla que se crea como será una tabla sin registrar. Encontrará más información sobre las tablas sin registrar en la [[!DNL PostgreSQL] documentación](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | Nombre de la tabla que se va a crear. |

**Ejemplo**

La siguiente consulta crea una nueva tabla `films_recent` consiste únicamente en entradas recientes de la tabla `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRAR

El `SHOW` muestra la configuración actual de los parámetros de tiempo de ejecución. Estas variables se pueden configurar con la variable `SET` mediante la edición de la `postgresql.conf` archivo de configuración, a través de `PGOPTIONS` variable de entorno (cuando se utiliza libpq o una aplicación basada en libpq), o mediante indicadores de línea de comandos al iniciar el servidor Postgres.

```sql
SHOW name
SHOW ALL
```

| Parámetros | Descripción |
| ------ | ------ |
| `name` | El nombre del parámetro de tiempo de ejecución del que desea obtener información. Los valores posibles del parámetro de tiempo de ejecución incluyen los siguientes:<br>`SERVER_VERSION`: Este parámetro muestra el número de versión del servidor.<br>`SERVER_ENCODING`: Este parámetro muestra la codificación del conjunto de caracteres del lado del servidor.<br>`LC_COLLATE`: Este parámetro muestra la configuración regional de la base de datos para la intercalación (orden de texto).<br>`LC_CTYPE`: Este parámetro muestra la configuración regional de la base de datos para la clasificación de caracteres.<br>`IS_SUPERUSER`: este parámetro muestra si la función actual tiene privilegios de superusuario. |
| `ALL` | Mostrar los valores de todos los parámetros de configuración con descripciones. |

**Ejemplo**

La siguiente consulta muestra la configuración actual del parámetro `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### COPIAR

El `COPY` El comando duplica la salida de cualquier `SELECT` consulta a una ubicación especificada. El usuario debe tener acceso a esta ubicación para que este comando se ejecute correctamente.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parámetros | Descripción |
| ------ | ------ |
| `query` | La consulta que desea copiar. |
| `format_name` | El formato en el que desea copiar la consulta. El `format_name` puede ser uno de `parquet`, `csv`, o `json`. El valor predeterminado es `parquet`. |

>[!NOTE]
>
>La ruta de salida completa será `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### MODIFICAR TABLA {#alter-table}

El `ALTER TABLE` El comando permite añadir o soltar restricciones de clave principal o externa, así como añadir columnas a la tabla.

#### AGREGAR o SOLTAR RESTRICCIÓN

Las siguientes consultas SQL muestran ejemplos de cómo agregar o quitar restricciones a una tabla. Las restricciones de clave principal y clave externa se pueden agregar a varias columnas con valores separados por comas. Puede crear claves compuestas pasando dos o más valores de nombre de columna, tal como se ve en los ejemplos siguientes.

**Definir claves principales o compuestas**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**Definir una relación entre tablas basada en una o más claves**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**Definición de una columna de identidad**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**Soltar una restricción/relación/identidad**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| Parámetros | Descripción |
| ------ | ------ |
| `table_name` | El nombre de la tabla que está editando. |
| `column_name` | Nombre de la columna a la que está agregando una restricción. |
| `referenced_table_name` | El nombre de la tabla a la que hace referencia la clave externa. |
| `primary_column_name` | Nombre de la columna a la que hace referencia la clave externa. |


>[!NOTE]
>
>El esquema de tabla debe ser único y no compartido entre varias tablas. Además, el área de nombres es obligatoria para la clave principal, la identidad principal y las restricciones de identidad.

#### Adición o eliminación de identidades principales y secundarias

El `ALTER TABLE` El comando permite agregar o eliminar restricciones para columnas de tabla de identidad principales y secundarias directamente a través de SQL.

En los ejemplos siguientes se agrega una identidad principal y una identidad secundaria mediante la adición de restricciones.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Las identidades también se pueden eliminar soltando restricciones, como se ve en el ejemplo siguiente.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Consulte el documento sobre [configuración de identidades en conjuntos de datos ad hoc](../data-governance/ad-hoc-schema-identities.md) para obtener información más detallada.

#### AÑADIR COLUMNA

Las siguientes consultas SQL muestran ejemplos de adición de columnas a una tabla.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Tipos de datos admitidos

En la tabla siguiente se enumeran los tipos de datos aceptados para agregar columnas a una tabla con [!DNL Postgres SQL], XDM y el [!DNL Accelerated Database Recovery] (ADR) en Azure SQL.

| — | cliente PSQL | XDM | ADR | Descripción |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Tipo de datos numéricos utilizados para almacenar enteros grandes comprendidos entre -9.223.372.036.854.775.807 y 9.223.372.036.854.775.807 en 8 bytes. |
| 2 | `integer` | `int4` | `integer` | Tipo de datos numérico utilizado para almacenar enteros entre -2.147.483.648 y 2.147.483.647 en 4 bytes. |
| 3 | `smallint` | `int2` | `smallint` | Tipo de datos numéricos utilizados para almacenar enteros entre -32.768 y 215-1 32.767 en 2 bytes. |
| 4 | `tinyint` | `int1` | `tinyint` | Tipo de datos numérico utilizado para almacenar enteros de 0 a 255 en 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Un tipo de datos de caracteres de tamaño variable. `varchar` se utiliza mejor cuando el tamaño de las entradas de datos de la columna varía considerablemente. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` y `FLOAT` son sinónimos válidos para `DOUBLE PRECISION`. `double precision` es un tipo de datos de punto flotante. Los valores de punto flotante se almacenan en 8 bytes. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` es un sinónimo válido para `double precision`.`double precision` es un tipo de datos de punto flotante. Los valores de punto flotante se almacenan en 8 bytes. |
| 8 | `date` | `date` | `date` | El `date` Los tipos de datos son valores de fecha de calendario almacenados de 4 bytes sin información de marca de tiempo. El rango de fechas válidas es del 01-01-0001 al 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Tipo de datos que se utiliza para almacenar un instante en el tiempo expresado como fecha y hora del día en el calendario. `datetime` incluye los calificadores de: año, mes, día, hora, segundo y fracción. A `datetime` la declaración puede incluir cualquier subconjunto de estas unidades de tiempo que se unan en esa secuencia, o incluso comprender solo una unidad de tiempo. |
| 10 | `char(len)` | `string` | `char(len)` | El `char(len)` palabra clave se utiliza para indicar que el elemento es un carácter de longitud fija. |

#### AÑADIR ESQUEMA

La siguiente consulta SQL muestra un ejemplo de adición de una tabla a una base de datos o esquema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Las tablas y vistas de ADLS no se pueden añadir a bases de datos o esquemas DWH.


#### QUITAR ESQUEMA

La siguiente consulta SQL muestra un ejemplo de eliminación de una tabla de una base de datos o esquema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Las tablas y vistas de DWH no se pueden eliminar de los esquemas o bases de datos de DWH vinculados físicamente.


**Parámetros**

| Parámetros | Descripción |
| ------ | ------ |
| `table_name` | El nombre de la tabla que está editando. |
| `column_name` | Nombre de la columna que desea agregar. |
| `data_type` | El tipo de datos de la columna que desea agregar. Los tipos de datos admitidos son los siguientes: bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar. |

### MOSTRAR CLAVES PRIMARIAS

El `SHOW PRIMARY KEYS` El comando enumera todas las restricciones de clave principal de la base de datos determinada.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### MOSTRAR CLAVES EXTERNAS

El `SHOW FOREIGN KEYS` El comando enumera todas las restricciones de clave externa para la base de datos determinada.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### MOSTRAR GRUPOS DE DATOS

El `SHOW DATAGROUPS` El comando devuelve una tabla de todas las bases de datos asociadas. Para cada base de datos, la tabla incluye el esquema, el tipo de grupo, el tipo secundario, el nombre secundario y el ID secundario.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### MOSTRAR GRUPOS DE DATOS PARA LA tabla

El `SHOW DATAGROUPS FOR` El comando &quot;table_name&quot; devuelve una tabla de todas las bases de datos asociadas que contienen el parámetro como elemento secundario. Para cada base de datos, la tabla incluye el esquema, el tipo de grupo, el tipo secundario, el nombre secundario y el ID secundario.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parámetros**

- `table_name`: Nombre de la tabla para la que desea buscar bases de datos asociadas.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
