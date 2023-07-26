---
title: Cálculo de estadísticas de conjuntos de datos
description: Este documento describe cómo calcular las estadísticas de nivel de columna en conjuntos de datos de Azure Data Lake Storage (ADLS) con comandos SQL.
source-git-commit: 66354932ee42137ca98e7033d942556f13c64de1
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Cálculo de estadísticas de conjuntos de datos

Ahora puede calcular las estadísticas de nivel de columna de [!DNL Azure Data Lake Storage] Conjuntos de datos de (ADLS) con `COMPUTE STATISTICS` y `SHOW STATISTICS` Comandos SQL. Los comandos SQL que calculan las estadísticas del conjunto de datos son una extensión del `ANALYZE TABLE` comando. Detalles completos sobre la `ANALYZE TABLE` El comando se encuentra en [Documentación de referencia SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Las estadísticas calculadas se almacenan en tablas temporales que tienen persistencia en el nivel de sesión. Puede acceder a los resultados de los cálculos en cualquier momento durante esa sesión. No se puede acceder a ellas en diferentes sesiones de PSQL.

Para ver las estadísticas que se calcularon con `ANALYZE TABLE COMPUTE STATISTICS` , puede utilizar una consulta SELECT en el nombre del alias o el ID de estadísticas. También puede limitar el ámbito del análisis estadístico a todo el conjunto de datos, a un subconjunto de un conjunto de datos, a todas las columnas o a un subconjunto de columnas.

>[!IMPORTANT]
>
>El `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, y `SHOW STATISTICS` los comandos no son compatibles con las tablas de data warehouse. Estas extensiones para `ANALYZE TABLE` Actualmente, los comandos solo son compatibles con tablas ADLS. Para obtener más información, consulte la [SECCIÓN ANALIZAR TABLA](../sql/syntax.md#analyze-table) de la guía de sintaxis SQL.

Esta guía le ayuda a estructurar las consultas para que pueda calcular las estadísticas de columna de un conjunto de datos de ADLS. Con estos comandos, puede ver las estadísticas generadas en la sesión a través de un cliente SQL mediante una consulta SQL.

## Estadísticas de cómputo {#compute-statistics}

Se han añadido construcciones adicionales a `ANALYZE TABLE` que le permite **calcular estadísticas para un subconjunto de un conjunto de datos y para determinadas columnas**. Para calcular las estadísticas del conjunto de datos, debe utilizar el `ANALYZE TABLE <tableName> COMPUTE STATISTICS` formato.

>[!IMPORTANT]
>
>El comportamiento predeterminado calcula las estadísticas de **conjunto de datos completo** y para **todas las columnas**. Para calcular las estadísticas de todas las columnas, debe utilizar el formato de consulta `ANALYZE TABLE COMPUTE STATISTICS`. Usted es **no** se recomienda utilizar la variable `COMPUTE STATISTICS` sin filtros en un conjunto de datos ADLS, ya que el tamaño del conjunto de datos puede ser muy grande (potencialmente petabytes de datos). En su lugar, siempre debe considerar la ejecución del comando analyze mediante `FILTERCONTEXT` y una lista de columnas especificada. Consulte las secciones sobre [limitación de columnas analizadas](#limit-included-columns) y [adición de una condición de filtro](#filter-condition) para obtener más información.

El ejemplo que se muestra a continuación calcula las estadísticas de `adc_geometric` conjunto de datos y para **todo** columnas en el conjunto de datos.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>El `COMPUTE STATISTICS` El comando no admite los tipos de datos de matriz o asignación. Puede establecer un `skip_stats_for_complex_datatypes` indicador que debe notificarse o que debe descartarse si el marco de datos de entrada tiene columnas con matrices y tipos de datos de asignación. De forma predeterminada, el indicador se establece en true. Para habilitar las notificaciones o los errores, utilice el siguiente comando: `SET skip_stats_for_complex_datatypes = false`.

## Creación de un nombre de alias {#alias-name}

Dado que los resultados de los cálculos pueden ser una gran cantidad de datos, no es razonable devolver los datos calculados directamente en la salida de la consola. Aunque los nombres de alias son opcionales, se recomienda utilizarlos como práctica recomendada al calcular las estadísticas. Proporcione un nombre de alias en la instrucción para hacer referencia descriptiva a los resultados en las consultas SQL. Como alternativa, un generado automáticamente `Statistics ID` se genera y utiliza para almacenar la información calculada.

El ejemplo siguiente almacena las estadísticas calculadas de salida en la variable `alias_name` para referencia posterior. El nombre de alias utilizado en la consulta está disponible para referencia en cuanto la variable `ANALYZE TABLE` se ha ejecutado el comando.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

El resultado del ejemplo anterior es `SUCCESSFULLY COMPLETED, alias_name`. La salida de la consola no muestra las estadísticas en la respuesta al comando analyze table compute statistics. Para ver los resultados detallados, debe utilizar una consulta SELECT en el nombre del alias o el ID de estadísticas.

## Ver el resultado de las estadísticas calculadas {#view-output-of-computed-statistics}

Si no proporciona un nombre de alias por adelantado, el Servicio de consultas generará automáticamente un nombre para el `Statistics ID` que sigue el formato de `<tableName_stats_{incremental_number}>`. Si se proporciona un nombre de alias, este aparece en la `Statistics ID` columna.

Ejemplo de salida de un `COMPUTE STATISTICS` La consulta es la siguiente:

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

Puede hacer lo siguiente **consultar las estadísticas calculadas directamente** haciendo referencia al `Statistics ID`. La instrucción de ejemplo siguiente le permite ver el resultado en su totalidad cuando se utiliza con el `Statistics ID` o el nombre del alias.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

El resultado de las estadísticas calculadas puede ser similar al ejemplo siguiente.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

## Mostrar los metadatos de análisis estadístico {#show-statistics}

Puede usar el complemento `SHOW STATISTICS` para mostrar los metadatos de todas las tablas de estadísticas temporales generadas en la sesión. Este comando puede ayudarle a refinar el ámbito del análisis estadístico.

Un ejemplo de salida de `SHOW STATISTICS` se ve a continuación.

```console
statsId | tableName | columnSet | filterContext | timestamp
--------+-----------+-----------+---------------+---------------
adc_geometric_stats_1 | adc_geometric | (age) |  | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
age_stats | castedtitanic | (age) | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

A continuación se proporciona una descripción de los nombres de las columnas de metadatos.

| El nombre de la columna | Descripción |
|---|---|
| `statsId` | Este ID hace referencia a la tabla de estadísticas temporales generada por el `COMPUTE STATISTICS` comando. |
| `tableName` | La tabla original utilizada para el análisis. |
| `columnSet` | Una lista de las columnas elegidas específicamente para el análisis. Un valor vacío indica que se analizaron todas las columnas. Consulte la sección sobre [limitar columnas](#limit-included-columns) para obtener más información. |
| `filterContext` | Una lista de los filtros aplicados al análisis. |
| `timestamp` | Cualquier filtro cronológico aplicado al análisis de datos para centrarse en un periodo específico. Consulte la [sección condición de filtro de marca de tiempo](#filter-condition) para obtener más información. |

Puede utilizar el ID de estadísticas o el nombre de alias para buscar las estadísticas calculadas con una instrucción SELECT en cualquier momento dentro de esa sesión. El ID de estadísticas y las estadísticas generadas solo son válidas para esta sesión en particular y no se puede acceder a ellas desde distintas sesiones de PSQL. Las estadísticas calculadas no son persistentes actualmente. Consulte la sección sobre cómo [ver el resultado de las estadísticas calculadas](#view-output-of-computed-statistics) para obtener más información.

## Limitar las columnas incluidas {#limit-included-columns}

Para enfocar el análisis, puede calcular las estadísticas de columnas de conjuntos de datos concretas haciendo referencia a ellas por su nombre. Utilice el `FOR COLUMNS (<col1>, <col2>)` sintaxis para dirigirse a columnas específicas. El ejemplo siguiente calcula las estadísticas de las columnas  `commerce`, `id`, y `timestamp` para el conjunto de datos `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Puede calcular las estadísticas de cualquier nivel raíz o columna anidada. En el siguiente ejemplo se muestran estas referencias.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Añadir una condición de filtro de marca de tiempo {#filter-condition}

Para enfocar el análisis de las columnas según la cronología, puede agregar una condición de filtro de marca de tiempo. Esta condición se puede utilizar para filtrar los datos históricos o enfocar el análisis de datos en un período específico. El `FILTERCONTEXT` El comando calcula las estadísticas de un subconjunto del conjunto de datos en función de la condición de filtro proporcionada.

En el ejemplo siguiente, las estadísticas se calculan en todas las columnas del conjunto de datos `tableName`, donde la marca de tiempo de la columna tiene valores entre el rango especificado de `2023-04-01 00:00:00` y `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Puede combinar el límite de columnas y el filtro para crear consultas computacionales altamente específicas para las columnas del conjunto de datos. Por ejemplo, la siguiente consulta calcula las estadísticas de las columnas `commerce`, `id`, y `timestamp` para el conjunto de datos `tableName`, donde la marca de tiempo de la columna tiene valores entre el rango especificado de `2023-04-01 00:00:00` y `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Pasos siguientes {#next-steps}

Al leer este documento, ahora comprende mejor cómo generar estadísticas de nivel de columna a partir de un conjunto de datos ADLS mediante una consulta SQL. Se recomienda leer el [Guía de sintaxis de SQLl](../sql/syntax.md) para descubrir más características del servicio de consultas de Adobe Experience Platform.
