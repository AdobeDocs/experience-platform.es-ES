---
title: Ejemplos de conjuntos de datos
description: Los conjuntos de datos de ejemplo del servicio de consultas le permiten realizar consultas exploratorias de big data con un tiempo de procesamiento muy reducido a costa de la precisión de la consulta. Esta guía proporciona información sobre cómo administrar los ejemplos para el procesamiento aproximado de consultas
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# Ejemplos de conjuntos de datos

El servicio de consulta de Adobe Experience Platform proporciona conjuntos de datos de ejemplo como parte de sus capacidades aproximadas de procesamiento de consultas. Los conjuntos de datos de muestra se crean con muestras aleatorias uniformes de conjuntos de datos de [!DNL Azure Data Lake Storage] (ADLS) existentes que utilizan solo un porcentaje de registros del original. Este porcentaje se conoce como tasa de muestreo. Ajustar la tasa de muestreo para controlar el equilibrio de precisión y el tiempo de procesamiento le permite realizar consultas exploratorias de big data con un tiempo de procesamiento muy reducido a costa de la precisión de la consulta.

Dado que muchos usuarios no necesitan una respuesta exacta para una operación de agregado sobre un conjunto de datos, emitir una consulta aproximada para devolver una respuesta aproximada es más eficiente para consultas exploratorias en conjuntos de datos grandes. Como los conjuntos de datos de ejemplo contienen solo un porcentaje de los datos del conjunto de datos original, le permite intercambiar la precisión de la consulta para un tiempo de respuesta mejorado. En tiempo de lectura, el servicio de consultas debe analizar menos filas, lo que produce resultados más rápidos que si se consultara todo el conjunto de datos.

Para ayudarle a administrar los ejemplos para un procesamiento de consultas aproximado, el Servicio de consultas admite las siguientes operaciones para ejemplos de conjuntos de datos:

- [Ejemplos de conjuntos de datos](#dataset-samples)
   - [Introducción {#get-started}](#getting-started-get-started)
   - [Crear una muestra de conjunto de datos aleatorio uniforme {#create-a-sample}](#create-a-uniform-random-dataset-sample-create-a-sample)
   - [Opcionalmente, especifique un criterio de filtro {#optional-filter-criteria}](#optionally-specify-a-filter-criteria-optional-filter-criteria)
   - [Ver la lista de muestras {#view-list-of-samples}](#view-the-list-of-samples-view-list-of-samples)
   - [Consultar el conjunto de datos de ejemplo {#query-sample-datasets}](#query-the-sample-dataset-query-sample-datasets)
   - [Eliminar muestras del conjunto de datos {#delete-a-sample}](#delete-dataset-samples-delete-a-sample)

## Introducción {#get-started}

Para utilizar las capacidades de procesamiento de consultas de creación y eliminación detalladas en este documento, debe establecer el indicador de sesión en `true`. Desde la línea de comandos del Editor de consultas o del cliente PSQL, escriba el comando `SET aqp=true;`.

>[!NOTE]
>
>Debe habilitar el indicador de sesión cada vez que inicie sesión en Experience Platform.

![Se resaltó el Editor de consultas con el comando &#39;SET aqp=true;&#39;.](../images/key-concepts/set-session-flag.png)

## Crear una muestra de conjunto de datos aleatorio uniforme {#create-a-sample}

Utilice el comando `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` con un nombre de conjunto de datos para crear una muestra aleatoria uniforme a partir de ese conjunto de datos.

La velocidad de muestreo es el porcentaje de registros tomados del conjunto de datos original. Puede controlar la velocidad de muestreo utilizando las palabras clave `TABLESAMPLE SAMPLERATE`. En este ejemplo, el valor de 5,0 equivale a una velocidad de muestreo del 50 %. Un valor de 2,5 equivaldría a 25 %, etc.

>[!IMPORTANT]
>
>El sistema permite un máximo de cinco muestras para cada conjunto de datos. Si intenta crear un sexto conjunto de datos de ejemplo, aparece un mensaje de error en la pantalla que indica que se ha alcanzado el límite de muestra.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Especificar opcionalmente un criterio de filtro {#optional-filter-criteria}

Puede optar por especificar un criterio de filtro para las muestras aleatorias uniformes. Esto le permite crear una muestra basada en el subconjunto filtrado de la tabla analizada.

Al crear una muestra, primero se aplica el filtro opcional y, a continuación, la muestra se crea a partir de la vista filtrada del conjunto de datos. Un ejemplo de conjunto de datos con un filtro aplicado sigue el siguiente formato de consulta:

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

A continuación, se muestran ejemplos prácticos de este tipo de conjunto de datos de muestra filtrado:

```sql
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

En los ejemplos proporcionados, el nombre de tabla es `large_table`, la condición de filtro en la tabla original es `month(to_timestamp(timestamp)) in ('8', '9')` y la tasa de muestreo es (X% de los datos filtrados), en este caso, `10`.

## Ver la lista de muestras {#view-list-of-samples}

Utilice la función `sample_meta()` para ver la lista de ejemplos asociados a una tabla ADLS.

```sql
SELECT sample_meta('example_dataset_name')
```

La lista de ejemplos de conjuntos de datos se muestra con el formato del ejemplo siguiente.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Consultar el conjunto de datos de ejemplo {#query-sample-datasets}

Use `{EXAMPLE_DATASET_NAME}` para consultar directamente las tablas de ejemplo. Como alternativa, agregue la palabra clave `WITHAPPROXIMATE` al final de una consulta y el servicio de consultas utilizará automáticamente el ejemplo creado más recientemente.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Eliminar muestras de conjuntos de datos {#delete-a-sample}

La operación de eliminación permite crear nuevas muestras una vez que se ha alcanzado el límite máximo de cinco muestras de conjuntos de datos.

```sql
DROP TABLESAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Si tiene varios conjuntos de datos de ejemplo derivados de un conjunto de datos ADLS original, cuando se suelta el original, también se eliminan todas las muestras asociadas.
