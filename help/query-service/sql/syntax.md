---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;sintaxis sql;sql;ctas;CTAS;Crear tabla como selección
solution: Experience Platform
title: Sintaxis SQL en Query Service
topic-legacy: syntax
description: Este documento muestra la sintaxis SQL admitida por Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---

# Sintaxis SQL en Query Service

El servicio de consulta de Adobe Experience Platform permite utilizar ANSI SQL estándar para las instrucciones `SELECT` y otros comandos limitados. Este documento cubre la sintaxis SQL admitida por [!DNL Query Service].

## SELECT consultas {#select-queries}

La siguiente sintaxis define una consulta `SELECT` compatible con [!DNL Query Service]:

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

Esta cláusula se puede utilizar para leer datos de forma incremental en una tabla basada en los ID de instantánea. Un ID de instantánea es un marcador de punto de comprobación representado por un número de tipo Long que se aplica a una tabla de lago de datos cada vez que se escriben datos en ella. La cláusula `SNAPSHOT` se adjunta a la relación de tabla a la que se utiliza junto.

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

Tenga en cuenta que una cláusula `SNAPSHOT` funciona con un alias de tabla o tabla pero no sobre una subconsulta o vista. Una cláusula `SNAPSHOT` funcionará en cualquier parte donde se pueda aplicar una consulta `SELECT` de una tabla.

Además, puede utilizar `HEAD` y `TAIL` como valores de desplazamiento especiales para las cláusulas de instantánea. El uso de `HEAD` hace referencia a un desplazamiento antes de la primera instantánea, mientras que `TAIL` hace referencia a un desplazamiento después de la última instantánea.

### cláusula WHERE

De forma predeterminada, las coincidencias producidas por una cláusula `WHERE` en una consulta `SELECT` distinguen entre mayúsculas y minúsculas. Si desea que las coincidencias no distingan entre mayúsculas y minúsculas, puede utilizar la palabra clave `ILIKE` en lugar de `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La lógica de las cláusulas LIKE e ILIKE se explica en la siguiente tabla:

| Cláusula | Operador |
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

Esta consulta devuelve clientes con nombres que comienzan en &quot;A&quot; o &quot;a&quot;.

### UNIR

Una consulta `SELECT` que utiliza uniones tiene la siguiente sintaxis:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIÓN, INTERSECCIÓN y EXCEPTO

Las cláusulas `UNION`, `INTERSECT` y `EXCEPT` se utilizan para combinar o excluir filas similares de dos o más tablas:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREAR TABLA COMO SELECCIONE

La siguiente sintaxis define una consulta `CREATE TABLE AS SELECT` (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**Parámetros**

- `schema`: Título del esquema XDM. Utilice esta cláusula solo si desea utilizar un esquema XDM existente para el nuevo conjunto de datos creado por la consulta CTAS.
- `rowvalidation`: (Opcional) Especifica si el usuario desea la validación de nivel de fila de cada lote nuevo introducido para el conjunto de datos recién creado. El valor predeterminado es `true`.
- `select_query`: Una  `SELECT` declaración. La sintaxis de la consulta `SELECT` se encuentra en la sección [SELECT queries section](#select-queries).

**Ejemplo**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>La instrucción `SELECT` debe tener un alias para las funciones de agregado como `COUNT`, `SUM`, `MIN`, etc. Además, la sentencia `SELECT` se puede proporcionar con o sin paréntesis (). Puede proporcionar una cláusula `SNAPSHOT` para leer los deltas incrementales en la tabla de destino.

## INSERTAR EN

El comando `INSERT INTO` se define de la siguiente manera:

```sql
INSERT INTO table_name select_query
```

**Parámetros**

- `table_name`: El nombre de la tabla en la que desea insertar la consulta.
- `select_query`: Una  `SELECT` declaración. La sintaxis de la consulta `SELECT` se encuentra en la sección [SELECT queries section](#select-queries).

**Ejemplo**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> La sentencia `SELECT` **no debe** incluirse entre paréntesis (). Además, el esquema del resultado de la instrucción `SELECT` debe ajustarse al de la tabla definida en la instrucción `INSERT INTO`. Puede proporcionar una cláusula `SNAPSHOT` para leer los deltas incrementales en la tabla de destino.

## TABLA DE COLOCACIÓN

El comando `DROP TABLE` suelta una tabla existente y elimina el directorio asociado con la tabla del sistema de archivos si no es una tabla externa. Si la tabla no existe, se produce una excepción.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parámetros**

- `IF EXISTS`: Si se especifica esto, no se genera ninguna excepción si la tabla no  **** contiene ningún texto.

## CREAR VISTA

La siguiente sintaxis define una consulta `CREATE VIEW`:

```sql
CREATE VIEW view_name AS select_query
```

**Parámetros**

- `view_name`: Nombre de la vista que se va a crear.
- `select_query`: Una  `SELECT` declaración. La sintaxis de la consulta `SELECT` se encuentra en la sección [SELECT queries section](#select-queries).

**Ejemplo**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## VISTA DE COLOCACIÓN

La siguiente sintaxis define una consulta `DROP VIEW`:

```sql
DROP VIEW [IF EXISTS] view_name
```

**Parámetro**

- `IF EXISTS`: Si se especifica esto, no se genera ninguna excepción si la vista no  **** contiene ninguna.
- `view_name`: Nombre de la vista que se va a eliminar.

**Ejemplo**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] Comandos SQL

La subsección siguiente cubre los comandos Spark SQL admitidos por el servicio de consulta.

### SET

El comando `SET` establece una propiedad y devuelve el valor de una propiedad existente o enumera todas las propiedades existentes. Si se proporciona un valor para una clave de propiedad existente, se anula el valor antiguo.

```sql
SET property_key = property_value
```

**Parámetros**

- `property_key`: El nombre de la propiedad que desea enumerar o modificar.
- `property_value`: El valor que desea que la propiedad se establezca como.

Para devolver el valor de cualquier configuración, utilice `SET [property key]` sin `property_value`.

## Comandos PostgreSQL

Las subsecciones siguientes abarcan los comandos PostgreSQL admitidos por el servicio de consultas.

### INICIO

El comando `BEGIN`, o alternativamente el comando `BEGIN WORK` o `BEGIN TRANSACTION`, inicia un bloque de transacciones. Cualquier instrucción que se introduzca después del comando begin se ejecutará en una sola transacción hasta que se proporcione un comando COMMIT o ROLLBACK explícito. Este comando es el mismo que `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CERRAR

El comando `CLOSE` libera los recursos asociados con un cursor abierto. Una vez cerrado el cursor, no se permiten operaciones posteriores en él. Se debe cerrar un cursor cuando ya no se necesite.

```sql
CLOSE name
CLOSE ALL
```

Si se utiliza `CLOSE name`, `name` representa el nombre de un cursor abierto que debe cerrarse. Si se utiliza `CLOSE ALL`, se cerrarán todos los cursores abiertos.

### DESASIGNAR

El comando `DEALLOCATE` le permite localizar una instrucción SQL previamente preparada. Si no asigna explícitamente una instrucción preparada, se desasigna al finalizar la sesión. Puede encontrar más información sobre las instrucciones preparadas en la sección [PREPARE command](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Si se utiliza `DEALLOCATE name`, `name` representa el nombre de la instrucción preparada que debe desasignarse. Si se utiliza `DEALLOCATE ALL`, se desasignarán todas las instrucciones preparadas.

### DECLARAR

El comando `DECLARE` permite al usuario crear un cursor, que se puede utilizar para recuperar un pequeño número de filas de una consulta más grande. Una vez creado el cursor, las filas se recuperan de él mediante `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

**Parámetros**

- `name`: Nombre del cursor que se va a crear.
- `query`: Un comando  `SELECT` o  `VALUES` que proporciona las filas que el cursor devolverá.

### EJECUTAR

El comando `EXECUTE` se utiliza para ejecutar una instrucción preparada anteriormente. Dado que las declaraciones preparadas sólo existen durante una sesión, la instrucción preparada debe haberse creado mediante una instrucción `PREPARE` ejecutada anteriormente en el período de sesiones en curso. Puede encontrar más información sobre el uso de instrucciones preparadas en la sección [`PREPARE` command](#prepare).

Si la sentencia `PREPARE` que creó la sentencia especificó algunos parámetros, se debe pasar un conjunto compatible de parámetros a la sentencia `EXECUTE`. Si estos parámetros no se pasan, se generará un error.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parámetros**

- `name`: Nombre de la instrucción preparada que se va a ejecutar.
- `parameter`: El valor real de un parámetro en la instrucción preparada. Debe ser una expresión que genere un valor compatible con el tipo de datos de este parámetro, tal como se determina cuando se creó la instrucción preparada.  Si hay varios parámetros para la instrucción preparada, se separan con comas.

### EXPLAIN

El comando `EXPLAIN` muestra el plan de ejecución de la instrucción suministrada. El plan de ejecución muestra cómo se analizan las tablas a las que hace referencia la instrucción.  Si se hace referencia a varias tablas, se mostrará qué algoritmos de unión se utilizan para unir las filas necesarias de cada tabla de entrada.

```sql
EXPLAIN option statement
```

Donde `option` puede ser uno de los siguientes:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parámetros**

- `ANALYZE`: Si el  `option` contiene  `ANALYZE`, se muestran los tiempos de ejecución y otras estadísticas.
- `FORMAT`: Si el  `option` contiene  `FORMAT`, especifica el formato de salida, que puede ser  `TEXT` o  `JSON`. La salida no textual contiene la misma información que el formato de salida de texto, pero es más fácil de analizar para los programas. El valor predeterminado de este parámetro es `TEXT`.
- `statement`: Cualquier  `SELECT`,  `INSERT`,  `UPDATE`,  `DELETE`,  `VALUES`,  `EXECUTE`,  `DECLARE`,  `CREATE TABLE AS` o  `CREATE MATERIALIZED VIEW AS` instrucción cuyo plan de ejecución desee ver.

>[!IMPORTANT]
>
>Tenga en cuenta que la instrucción se ejecuta realmente cuando se utiliza la opción `ANALYZE`. Aunque `EXPLAIN` descarta cualquier resultado que devuelva un `SELECT`, otros efectos secundarios de la afirmación ocurren como de costumbre.

**Ejemplo**

El siguiente ejemplo muestra el plan para una consulta simple en una tabla con una sola columna `integer` y 10 000 filas:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### RECUPERAR

El comando `FETCH` recupera filas utilizando un cursor creado anteriormente.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Parámetros**

- `num_of_rows`: Número de filas que se van a recuperar.
- `cursor_name`: Nombre del cursor desde el que se recupera la información.

### PREPARAR {#prepare}

El comando `PREPARE` permite crear una instrucción preparada. Una instrucción preparada es un objeto del lado del servidor que puede utilizarse para crear plantillas de sentencias SQL similares.

Las instrucciones preparadas pueden tomar parámetros, que son valores que se sustituyen en la instrucción cuando se ejecuta. Los parámetros se remiten por posición, utilizando $1, $2, etc., al utilizar instrucciones preparadas.

De forma opcional, puede especificar una lista de tipos de datos de parámetros. Si el tipo de datos de un parámetro no aparece en la lista, el tipo se puede inferir desde el contexto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parámetros**

- `name`: Nombre de la declaración preparada.
- `data_type`: Tipos de datos de los parámetros de la instrucción preparada. Si el tipo de datos de un parámetro no aparece en la lista, el tipo se puede inferir desde el contexto. Si necesita agregar varios tipos de datos, puede agregarlos en una lista separada por comas.

### RETROSPECTIVA

El comando `ROLLBACK` deshace la transacción actual y descarta todas las actualizaciones realizadas por la transacción.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECCIONAR EN

El comando `SELECT INTO` crea una nueva tabla y la rellena con datos calculados por una consulta. Los datos no se devuelven al cliente, como sucede con un comando normal `SELECT`. Las columnas de la nueva tabla tienen los nombres y tipos de datos asociados con las columnas de salida del comando `SELECT`.

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

**Parámetros**

Puede encontrar más información sobre los parámetros de consulta SELECT estándar en la sección [SELECT query](#select-queries). Esta sección solo enumera los parámetros que son exclusivos del comando `SELECT INTO`.

- `TEMPORARY` o  `TEMP`: Un parámetro opcional. Si se especifica, la tabla que se crea será una tabla temporal.
- `UNLOGGED`: Un parámetro opcional. Si se especifica, la tabla que se crea como será una tabla sin registrar. Puede encontrar más información sobre las tablas no registradas en la [Documentación PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: Nombre de la tabla que se va a crear.

**Ejemplo**

La siguiente consulta crea una nueva tabla `films_recent` que consiste únicamente en entradas recientes de la tabla `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRAR

El comando `SHOW` muestra la configuración actual de los parámetros de tiempo de ejecución. Estas variables se pueden configurar usando la instrucción `SET`, editando el archivo de configuración `postgresql.conf`, a través de la variable de entorno `PGOPTIONS` (cuando se usa libpq o una aplicación basada en libpq) o a través de indicadores de línea de comandos al iniciar el servidor Postgres.

```sql
SHOW name
SHOW ALL
```

**Parámetros**

- `name`: Nombre del parámetro de tiempo de ejecución del que desea obtener información. Los valores posibles del parámetro de tiempo de ejecución incluyen los siguientes valores:
   - `SERVER_VERSION`: Este parámetro muestra el número de versión del servidor.
   - `SERVER_ENCODING`: Este parámetro muestra la codificación del conjunto de caracteres del lado del servidor.
   - `LC_COLLATE`: Este parámetro muestra la configuración regional de la base de datos para la intercalación (orden de texto).
   - `LC_CTYPE`: Este parámetro muestra la configuración regional de la base de datos para la clasificación de caracteres.
      `IS_SUPERUSER`: Este parámetro muestra si la función actual tiene privilegios de superusuario.
- `ALL`: Mostrar los valores de todos los parámetros de configuración con descripciones.

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

El comando `COPY` envía la salida de cualquier consulta `SELECT` a una ubicación especificada. El usuario debe tener acceso a esta ubicación para que este comando se ejecute correctamente.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parámetros**

- `query`: La consulta que desea copiar.
- `format_name`: El formato en el que desea copiar la consulta. El `format_name` puede ser uno de `parquet`, `csv` o `json`. De forma predeterminada, el valor es `parquet`.

>[!NOTE]
>
>La ruta de salida completa será `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### MODIFICAR TABLA

El comando `ALTER TABLE` permite añadir o soltar restricciones de claves principales o externas, así como agregar columnas a la tabla.

#### AÑADIR o SOLTAR RESTRICCIÓN

Las siguientes consultas SQL muestran ejemplos de adición o colocación de restricciones en una tabla.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Parámetros**

- `table_name`: El nombre de la tabla que está editando.
- `constraint_name`: Nombre de la restricción que desea agregar o eliminar.
- `column_name`: Nombre de la columna a la que está agregando una restricción.
- `referenced_table_name`: El nombre de la tabla a la que hace referencia la clave externa.
- `primary_column_name`: Nombre de la columna a la que se hace referencia mediante la clave externa.

>[!NOTE]
>
>El esquema de tabla debe ser único y no compartido entre varias tablas. Además, el área de nombres es obligatoria para las restricciones de clave principal.

#### AGREGAR COLUMNA

Las siguientes consultas SQL muestran ejemplos de adición de columnas a una tabla.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Parámetros**

- `table_name`: El nombre de la tabla que está editando.
- `column_name`: El nombre de la columna que desea agregar.
- `data_type`: El tipo de datos de la columna que desea agregar. Los tipos de datos admitidos son los siguientes: bigint, char, cadena, fecha, fecha, hora de fecha, doble, precisión doble, entero, smallint, tinyint, varchar.

### MOSTRAR CLAVES PRINCIPALES

El comando `SHOW PRIMARY KEYS` enumera todas las restricciones de claves principales de la base de datos dada.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### MOSTRAR CLAVES EXTRANJERAS

El comando `SHOW FOREIGN KEYS` enumera todas las restricciones de claves externas para la base de datos dada.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
