---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sintaxis SQL
topic: syntax
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Sintaxis SQL

El servicio de Consulta permite utilizar ANSI SQL estándar para `SELECT` sentencias y otros comandos limitados. Este documento muestra la sintaxis SQL admitida por el servicio de Consulta.

## Definir una consulta SELECT

La siguiente sintaxis define una `SELECT` consulta admitida por el servicio de Consulta:

```
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

donde `from_item` puede ser uno de los siguientes:

```
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

y `grouping_element` puede ser uno de los siguientes:

```
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

y `with_query` es:

```
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### cláusula WHERE ILIKE

La palabra clave ILIKE puede utilizarse en lugar de LIKE para hacer coincidir la cláusula WHERE de la consulta SELECT sin distinción de mayúsculas y minúsculas.

```
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La lógica de las cláusulas LIKE e ILIKE es la siguiente:
- ```WHERE condition LIKE pattern```, ```~~``` es equivalente al patrón
- ```WHERE condition NOT LIKE pattern```, ```!~~``` es equivalente al patrón
- ```WHERE condition ILIKE pattern```, ```~~*``` equivalente al patrón
- ```WHERE condition NOT ILIKE pattern```, ```!~~*``` equivalente al patrón


#### Ejemplo

```
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Devuelve clientes con nombres que comienzan en &quot;A&quot; o &quot;a&quot;.

## UNIONES

Una `SELECT` consulta que utiliza uniones tiene la siguiente sintaxis:

```
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNIÓN, INTERSECCIÓN Y EXCEPTO

Las cláusulas `UNION`, `INTERSECT`y `EXCEPT` son compatibles para combinar o excluir filas similares de dos o más tablas:

```
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## CREAR TABLA COMO SELECCIONE

La siguiente sintaxis define una consulta `CREATE TABLE AS SELECT` (CTAS) admitida por el servicio de Consulta:

```
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

donde `target_schema_title` es el título del esquema XDM. Utilice esta cláusula solo si desea utilizar un esquema XDM existente para el nuevo conjunto de datos creado por la consulta CTAS.

y `select_query` es una `SELECT` instrucción, cuya sintaxis se define arriba en este documento.


### Ejemplo

```
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Tenga en cuenta que para una consulta de CTAS determinada:

1. La `SELECT` instrucción debe tener un alias para las funciones acumuladas como `COUNT`, `SUM`, `MIN`, etc.
2. La `SELECT` declaración se puede proporcionar con o sin paréntesis ().

## INSERTAR EN

La siguiente sintaxis define una `INSERT INTO` consulta admitida por el servicio de Consulta:

```
INSERT INTO table_name select_query
```

donde `select_query` es una `SELECT` instrucción, cuya sintaxis se define arriba en este documento.

### Ejemplo

```
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Tenga en cuenta que para una determinada consulta INSERTAR EN:

1. La `SELECT` declaración NO DEBE encerrarse entre paréntesis ().
2. El esquema del resultado de la `SELECT` instrucción debe ajustarse al de la tabla definida en la `INSERT INTO` instrucción.

### TABLA DE COLOCACIÓN

Suelte una tabla y elimine el directorio asociado con la tabla del sistema de archivos si no es una tabla EXTERNA. Si la tabla que se va a soltar no existe, se producirá una excepción.

```
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Parámetros

- `IF EXISTS`:: Si la tabla no existe, no sucede nada
- `TEMP`:: Tabla temporal

## CREAR VISTA

La siguiente sintaxis define una `CREATE VIEW` consulta admitida por el servicio de Consulta:

```
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Donde `view_name` es el nombre de la vista que se va a crear y `select_query` es una `SELECT` instrucción, cuya sintaxis se define arriba en este documento.

Ejemplo:

```
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### VISTA DE COLOCACIÓN

La siguiente sintaxis define una `DROP VIEW` consulta admitida por el servicio de Consulta:

```
DROP VIEW [IF EXISTS] view_name
```

Donde `view_name` se suprime el nombre de la vista

Ejemplo:

```
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Comandos SQL de Spark

### SET

Establezca una propiedad, devuelva el valor de una propiedad existente o lista todas las propiedades existentes. Si se proporciona un valor para una clave de propiedad existente, se sobrescribe el valor antiguo.

```
SET property_key [ To | =] property_value
```

Para devolver el valor de cualquier configuración, utilice `SHOW [setting name]`.

## Comandos PostgreSQL

### COMENZAR

Este comando se analiza y el comando completado se devuelve al cliente. Es lo mismo que el `START TRANSACTION` comando.

```
BEGIN [ TRANSACTION ]
```

#### Parámetros

- `TRANSACTION`:: Palabras clave opcionales. Lo escucha, no se realiza ninguna acción al respecto.

### CERRAR

`CLOSE` libera los recursos asociados a un cursor abierto. Una vez cerrado el cursor, no se permiten operaciones posteriores. Un cursor debe cerrarse cuando ya no lo necesite.

```
CLOSE { name }
```

#### Parámetros

- `name`:: el nombre de un cursor abierto que se va a cerrar.

### COMPROMISO

No se toma ninguna medida en el Servicio de Consulta como respuesta a la declaración de transacción de confirmación.

```
COMMIT [ WORK | TRANSACTION ]
```

#### Parámetros

- `WORK`
- `TRANSACTION`:: Palabras clave opcionales. No tienen ningún efecto.

### DESASIGNAR

Utilícelo `DEALLOCATE` para deslocalizar una instrucción SQL previamente preparada. Si no asigna explícitamente una instrucción preparada, se desasigna al finalizar la sesión.

```
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Parámetros

- `Prepare`:: Esta palabra clave se omite.
- `name`:: El nombre de la instrucción preparada que se va a asignar.
- `ALL`:: Desasigne todas las declaraciones preparadas.

### DECLARAR

`DECLARE` permite al usuario crear cursores, que se pueden utilizar para recuperar un pequeño número de filas a la vez a partir de una consulta mayor. Una vez creado el cursor, se recuperan filas de él mediante `FETCH`.

```
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Parámetros

- `name`:: Nombre del cursor que se va a crear.
- `WITH HOLD`:: Especifica que el cursor se puede seguir utilizando después de que la transacción que la creó se confirme correctamente.
- `query`:: Un `SELECT` comando o `VALUES` que proporciona las filas que devolverá el cursor.

### EJECUTAR

`EXECUTE` se utiliza para ejecutar una instrucción previamente preparada. Dado que las declaraciones preparadas sólo existen durante una sesión, la declaración preparada debe haber sido creada por una `PREPARE` declaración ejecutada anteriormente en el período de sesiones en curso.

Si la `PREPARE` sentencia que creó la sentencia especificaba algunos parámetros, se debe pasar un conjunto de parámetros compatible a la `EXECUTE` sentencia o se produce un error. Tenga en cuenta que las instrucciones preparadas (a diferencia de las funciones) no se sobrecargan según el tipo o el número de sus parámetros. El nombre de una instrucción preparada debe ser único dentro de una sesión de base de datos.

```
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Parámetros

- `name`:: Nombre de la instrucción preparada que se va a ejecutar.
- `parameter`:: El valor real de un parámetro en la instrucción preparada. Debe ser una expresión que produzca un valor compatible con el tipo de datos de este parámetro, tal como se determina cuando se creó la instrucción preparada.

### EXPLICAR

Este comando muestra el plan de ejecución que el planificador PostgreSQL genera para la instrucción proporcionada. El plan de ejecución muestra cómo se analizarán las tablas a las que hace referencia la instrucción — mediante análisis secuencial sin formato, análisis de índice, etc. — y si se hace referencia a varias tablas, qué algoritmos de combinación se utilizan para unir las filas necesarias de cada tabla de entrada.

La parte más importante de la visualización es el costo estimado de ejecución de la sentencia, que es la conjetura del planificador sobre cuánto tiempo tardará en ejecutar la sentencia (medida en unidades de costo que son arbitrarias, pero que generalmente significan cargas de páginas de disco). En realidad, se muestran dos números: se puede devolver el costo de inicio antes de la primera fila y el costo total para devolver todas las filas. Para la mayoría de las consultas, el costo total es lo que importa, pero en contextos como una subconsulta en EXISTS, el planificador elige el costo de inicio más bajo en lugar del costo total más bajo (porque el ejecutor se detiene después de obtener una fila, de todos modos). Además, si se limita el número de filas que se devolverán con una `LIMIT` cláusula, el planificador realiza una interpolación adecuada entre los costes del punto final para calcular qué plan es realmente el más barato.

La `ANALYZE` opción hace que la instrucción se ejecute, no solo se planifique. A continuación, se agregan estadísticas de tiempo de ejecución real a la visualización, incluido el tiempo total transcurrido empleado en cada nodo de plan (en milisegundos) y el número total de filas que devolvió. Esto es útil para ver si las estimaciones del planificador están cerca de la realidad.

```
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Parámetros

- `ANALYZE`:: Ejecute el comando y muestre los tiempos de ejecución reales y otras estadísticas. Este parámetro tiene el valor predeterminado `FALSE`.
- `FORMAT`:: Especifique el formato de salida, que puede ser TEXT, XML, JSON o YAML. La salida no textual contiene la misma información que el formato de salida de texto, pero es más fácil de analizar para los programas. Este parámetro tiene el valor predeterminado `TEXT`.
- `statement`:: Cualquier `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`o `CREATE TABLE AS``CREATE MATERIALIZED VIEW AS` instrucción, cuyo plan de ejecución desee ver.

>[!IMPORTANT] Tenga en cuenta que la instrucción se ejecuta realmente cuando se utiliza la `ANALYZE` opción. Aunque `EXPLAIN` descarta cualquier resultado que `SELECT` devuelva, otros efectos secundarios de la afirmación se producen como de costumbre.

#### Ejemplo

Para mostrar el plan de una consulta simple en una tabla con una sola `integer` columna y 10000 filas:

```
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` recupera filas utilizando un cursor creado anteriormente.

Un cursor tiene una posición asociada, la cual es utilizada por `FETCH`. La posición del cursor puede estar antes de la primera fila del resultado de la consulta, en cualquier fila del resultado o después de la última fila del resultado. Cuando se crea, se coloca un cursor antes de la primera fila. Después de recuperar algunas filas, el cursor se coloca en la fila recuperada más recientemente. Si `FETCH` se ejecuta al final de las filas disponibles, el cursor se coloca a la izquierda después de la última fila. Si no hay tal fila, se devuelve un resultado vacío y los cursores se dejan colocados antes de la primera fila o después de la última fila, según corresponda.

```
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Parámetros

- `num_of_rows`:: Constante de entero con posible signo que determina la ubicación o el número de filas que se van a recuperar.
- `cursor_name`:: Nombre del cursor abierto.

### PREPARAR

`PREPARE` crea una instrucción preparada. Una instrucción preparada es un objeto del lado del servidor que puede utilizarse para optimizar el rendimiento. Cuando se ejecuta la `PREPARE` sentencia, la instrucción especificada se analiza, analiza y reescribe. Cuando se emite un `EXECUTE` comando, se planifica y ejecuta la instrucción preparada. Esta división de tareas evita el trabajo de análisis de análisis repetitivo, al tiempo que permite que el plan de ejecución dependa de los valores de parámetro específicos suministrados.

Las sentencias preparadas pueden tomar parámetros, valores que se sustituyen en la sentencia cuando se ejecuta. Al crear la instrucción preparada, consulte los parámetros por posición, utilizando $1, $2, etc. Se puede especificar opcionalmente una lista correspondiente de tipos de datos de parámetros. Cuando no se especifica el tipo de datos de un parámetro o se declara como desconocido, el tipo se deduce del contexto en el que se hace referencia al parámetro por primera vez, si es posible. Al ejecutar la instrucción, especifique los valores reales de estos parámetros en la `EXECUTE` instrucción.

Las instrucciones preparadas solo duran durante la sesión de base de datos actual. Cuando finaliza la sesión, se olvida la instrucción preparada, por lo que debe volver a crearse antes de volver a utilizarse. Esto también significa que una sola instrucción preparada no puede ser utilizada por varios clientes de base de datos simultáneos. Sin embargo, cada cliente puede crear su propia declaración preparada para usar. Las instrucciones preparadas se pueden limpiar manualmente mediante el `DEALLOCATE` comando .

Las sentencias preparadas tienen la mayor ventaja de rendimiento cuando se utiliza una sola sesión para ejecutar un gran número de sentencias similares. La diferencia de rendimiento es particularmente importante si las instrucciones son complejas de planificar o reescribir, por ejemplo si la consulta implica una combinación de muchas tablas o requiere la aplicación de varias reglas. Si la afirmación es relativamente sencilla de planificar y reescribir, pero relativamente cara de ejecutar, la ventaja de rendimiento de las declaraciones preparadas es menos evidente.

```
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Parámetros

- `name`:: Un nombre arbitrario dado a esta declaración preparada en particular. Debe ser única en una sola sesión y se utiliza posteriormente para ejecutar o deslocalizar una instrucción previamente preparada.
- `data-type`:: El tipo de datos de un parámetro de la instrucción preparada. Si el tipo de datos de un parámetro en particular no se especifica o se especifica como desconocido, se deduce del contexto en el que se hace referencia por primera vez al parámetro. Para hacer referencia a los parámetros de la declaración preparada, utilice $1, $2, etc.


### ROLLBACK

`ROLLBACK` revierte la transacción actual y provoca que se descarten todas las actualizaciones realizadas por la transacción.

```
ROLLBACK [ WORK ]
```

#### Parámetros

- `WORK`

### SELECCIONAR EN

`SELECT INTO` crea una tabla nueva y la rellena con datos calculados por una consulta. Los datos no se devuelven al cliente, como sucede con un `SELECT`cliente normal. Las columnas de la nueva tabla tienen los nombres y los tipos de datos asociados con las columnas de salida de la `SELECT`.

```
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

#### Parámetros

- `TEMPORARAY` o `TEMP`: Si se especifica, la tabla se crea como una tabla temporal.
- `UNLOGGED:` si se especifica, la tabla se crea como una tabla sin registrar.
- `new_table` El nombre (opcionalmente, calificado por esquemas) de la tabla que se va a crear.

#### Ejemplo

Cree una nueva tabla `films_recent` compuesta únicamente de entradas recientes de la tabla `films`:

```
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRAR

`SHOW` muestra la configuración actual de los parámetros de tiempo de ejecución. Estas variables se pueden configurar usando la `SET` sentencia, editando el archivo de configuración postgresql.conf, a través de la variable `PGOPTIONS` ambiental (al usar libpq o una aplicación basada en libpq) o a través de indicadores de línea de comandos al iniciar el servidor de postgres.

```
SHOW name
```

#### Parámetros

- `name`:
   - `SERVER_VERSION`:: Muestra el número de versión del servidor.
   - `SERVER_ENCODING`:: Muestra la codificación del conjunto de caracteres del lado del servidor. Actualmente, este parámetro se puede mostrar pero no se puede establecer, ya que la codificación se determina en el momento de creación de la base de datos.
   - `LC_COLLATE`:: Muestra la configuración regional de la base de datos para la intercalación (orden de texto). Actualmente, este parámetro se puede mostrar pero no se puede establecer, porque la configuración se determina en el momento de creación de la base de datos.
   - `LC_CTYPE`:: Muestra la configuración regional de la base de datos para la clasificación de caracteres. Actualmente, este parámetro se puede mostrar pero no se puede establecer, porque la configuración se determina en el momento de creación de la base de datos.
      `IS_SUPERUSER`:: True si la función actual tiene privilegios de superusuario.
- `ALL`:: Muestra los valores de todos los parámetros de configuración con descripciones.

#### Ejemplo

Mostrar la configuración actual del parámetro `DateStyle`

```
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### TRANSACCIÓN DE INICIOS

Este comando se analiza y devuelve el comando completado al cliente. Es lo mismo que el `BEGIN` comando.

```
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```
