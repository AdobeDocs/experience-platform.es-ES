---
title: Cálculo de estadísticas de conjuntos de datos
description: Este documento describe cómo calcular las estadísticas de nivel de columna en conjuntos de datos de Azure Data Lake Storage (ADLS) con comandos SQL.
source-git-commit: c7bc395038906e27449c82c518bd33ede05c5691
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Cálculo de estadísticas de conjuntos de datos

Ahora puede calcular las estadísticas de nivel de columna de [!DNL Azure Data Lake Storage] Conjuntos de datos de (ADLS) con `COMPUTE STATISTICS` y `SHOW STATISTICS` Comandos SQL. Los comandos SQL que calculan las estadísticas del conjunto de datos son una extensión del `ANALYZE TABLE` comando. Detalles completos sobre la `ANALYZE TABLE` El comando se encuentra en [Documentación de referencia SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Actualmente, las estadísticas generadas solo son válidas para esa sesión y no son persistentes entre sesiones. No se puede acceder a ellas en diferentes sesiones de PSQL.

Con el `SHOW STATISTICS FOR <alias_name>` , puede ver las estadísticas que se calcularon con el comando `ANALYZE TABLE COMPUTE STATISTICS` comando. Mediante la combinación de estos comandos, ahora puede calcular las estadísticas de columna en todo el conjunto de datos, en un subconjunto de un conjunto de datos, en todas las columnas o en un subconjunto de columnas.

>[!IMPORTANT]
>
>El `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, y `SHOW STATISTICS` los comandos no son compatibles con las tablas de data warehouse. Estas extensiones para `ANALYZE TABLE` Actualmente, los comandos solo son compatibles con tablas ADLS. Para obtener más información, consulte la [SECCIÓN ANALIZAR TABLA](../sql/syntax.md#analyze-table) de la guía de sintaxis SQL.

Esta guía le ayuda a estructurar las consultas para que pueda calcular las estadísticas de columna de un conjunto de datos de ADLS. Con estos comandos, puede ver las estadísticas generadas en la sesión a través de un cliente SQL mediante una consulta SQL.

## Estadísticas de cómputo {#compute-statistics}

Se han añadido construcciones adicionales a `ANALYZE TABLE` comando que le permite **calcular estadísticas para un subconjunto de un conjunto de datos y para determinadas columnas**. Para ello, debe utilizar la variable `ANALYZE TABLE <tableName> COMPUTE STATISTICS` formato.

>[!IMPORTANT]
>
>El comportamiento predeterminado calcula las estadísticas de **conjunto de datos completo** y para **todas las columnas**. Para calcular las estadísticas de todas las columnas, debe utilizar el formato de consulta `ANALYZE TABLE COMPUTE STATISTICS`. Usted es **no** se recomienda utilizarlo en un conjunto de datos de ADLS, ya que el tamaño del conjunto de datos puede ser muy grande (potencialmente petabytes de datos). En su lugar, siempre debe considerar la ejecución del comando analyze mediante `FILTERCONTEXT` y una lista de columnas especificada. Consulte las secciones sobre [limitación de columnas analizadas](#limit-included-columns) y [adición de una condición de filtro](#filter-condition) para obtener más información.

El ejemplo que se muestra a continuación calcula las estadísticas de `adc_geometric` conjunto de datos y para **todo** columnas en el conjunto de datos.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` no admite los tipos de datos array o map. Puede establecer un `skip_stats_for_complex_datatypes` indicador al que notificar o error si el marco de datos de entrada tiene columnas con matrices y tipos de datos de asignación. De forma predeterminada, el indicador se establece en true. Para habilitar las notificaciones o los errores, utilice el siguiente comando: `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

La salida de la consola no muestra las estadísticas en respuesta al comando analyze table compute statistics. En su lugar, la consola mostrará una sola columna de fila de `Statistics ID` con un identificador único universal para hacer referencia a los resultados. También puede elegir **consulta directamente en el`Statistics ID`**. Al finalizar correctamente un `COMPUTE STATISTICS` consulta, los resultados se muestran de la siguiente manera:

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

Puede consultar el resultado de las estadísticas directamente haciendo referencia al `Statistics ID` como se ve a continuación:

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Esta instrucción le permite ver el resultado de forma similar al comando SHOW STATISTICS cuando se utiliza con la instrucción `Statistics ID`.

Puede ver una lista de todas las estadísticas calculadas dentro de la sesión ejecutando el comando SHOW STATISTICS. A continuación se muestra un ejemplo de salida del comando SHOW STATISTICS.

```console
statsId | tableName | columnSet | filterContext | timestamp
-----------+---------------+-----------+---------------------------------------+---------------
adc_geometric_stats_1 |adc_geometric | (age) | | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
```

<!-- Commented out until the <alias_name> feature is released.

To see the output, you must use the `SHOW STATISTICS` command. Instructions on [how to show the statistics](#show-statistics) are provided later in the document. 

-->

## Limitar las columnas incluidas {#limit-included-columns}

Puede calcular las estadísticas de columnas de conjuntos de datos concretos haciendo referencia a ellas por su nombre. Utilice el `FOR COLUMNS (<col1>, <col2>)` sintaxis para dirigirse a columnas específicas. El ejemplo siguiente calcula las estadísticas de las columnas  `commerce`, `id`, y `timestamp` para el conjunto de datos `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Puede calcular las estadísticas de cualquier nivel raíz o columna anidada. En el siguiente ejemplo se muestran estas referencias.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Añadir una condición de filtro de marca de tiempo {#filter-condition}

Puede agregar una condición de filtro de marca de tiempo para centrar el análisis de las columnas. Esto puede utilizarse para filtrar los datos históricos o enfocar el análisis de datos en un periodo específico. El `FILTERCONTEXT` El comando calcula las estadísticas de un subconjunto del conjunto de datos en función de la condición de filtro proporcionada.

En el ejemplo siguiente, las estadísticas se calculan en todas las columnas del conjunto de datos `tableName`, donde la marca de tiempo de la columna tiene valores entre el rango especificado de `2023-04-01 00:00:00` y `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Puede combinar el límite de columnas y el filtro para crear consultas computacionales altamente específicas para las columnas del conjunto de datos. Por ejemplo, la siguiente consulta calcula las estadísticas de las columnas `commerce`, `id`, y `timestamp` para el conjunto de datos `tableName`, donde la marca de tiempo de la columna tiene valores entre el rango especificado de `2023-04-01 00:00:00` y `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- Commented out until the <alias_name> feature is released.
## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. 
-->

<!-- Commented out until the <alias_name> feature is released.

## Show the statistics {#show-statistics}

The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  

Even with a filter condition and a column list, the computation can target a large amount of data. Query Service generates a universally unique identifier for the statistics ID to store this calculated information. You can then use this statistics ID to look up the computed statistics with the `SHOW STATISTICS` command at any time within that session. 

The statistics ID and the statistics generated are only valid for this particular session and cannot be accessed across different PSQL sessions. The computed statistics are not currently persistent. To display the statistics, use the command seen below.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

An output might look similar to the example below. 

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
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

-->

## Pasos siguientes {#next-steps}

Al leer este documento, ahora comprende mejor cómo generar estadísticas de nivel de columna a partir de un conjunto de datos ADLS mediante una consulta SQL. Se recomienda leer el [Guía de sintaxis de SQLl](../sql/syntax.md) para descubrir más características del servicio de consultas de Adobe Experience Platform.
