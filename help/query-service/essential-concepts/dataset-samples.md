---
title: Muestras de conjuntos de datos
description: Los conjuntos de datos de ejemplo del servicio de consulta le permiten realizar consultas exploratorias sobre grandes datos con un tiempo de procesamiento considerablemente reducido al coste de la precisión de la consulta. Esta guía proporciona información sobre cómo administrar los ejemplos para el procesamiento aproximado de consultas
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Ejemplos de conjuntos de datos (versión limitada)

>[!IMPORTANT]
>
>La función de muestras de conjuntos de datos se encuentra actualmente en una versión limitada y no está disponible para todos los clientes.

El servicio de consulta de Adobe Experience Platform proporciona conjuntos de datos de ejemplo como parte de sus capacidades aproximadas de procesamiento de consultas. Los conjuntos de datos de ejemplo se crean con muestras aleatorias uniformes de [!DNL Azure Data Lake Storage] (ADLS) conjuntos de datos que utilizan solo un porcentaje de registros del original. Este porcentaje se conoce como tasa de muestreo. Ajustar la tasa de muestreo para controlar el equilibrio de precisión y tiempo de procesamiento le permite realizar consultas exploratorias sobre grandes datos con un tiempo de procesamiento considerablemente menor al coste de la precisión de la consulta.

Como muchos usuarios no necesitan una respuesta exacta para una operación agregada en un conjunto de datos, emitir una consulta aproximada para devolver una respuesta aproximada es más eficiente para consultas exploratorias en conjuntos de datos grandes. Como los conjuntos de datos de ejemplo contienen solo un porcentaje de los datos del conjunto de datos original, le permite intercambiar la precisión de la consulta para mejorar el tiempo de respuesta. En el momento de la lectura, el servicio de consulta debe analizar menos filas, lo que produce resultados más rápido que si tuviera que consultar todo el conjunto de datos.

Para ayudarle a administrar los ejemplos para el procesamiento aproximado de consultas, Query Service admite las siguientes operaciones para muestras de conjuntos de datos:

- [Cree un ejemplo de conjunto de datos aleatorio uniforme.](#create-a-sample)
- [Vea la lista de ejemplos para una tabla ADLS.](#view-list-of-samples)
- [Consulte directamente los conjuntos de datos de ejemplo.](#query-sample-datasets)
- [Elimine una muestra.](#delete-a-sample)
- Elimine las muestras asociadas cuando se suelte la tabla ADLS original.

## Primeros pasos

Para utilizar las capacidades aproximadas de procesamiento de consultas detalladas arriba, debe establecer el indicador de sesión en `true`. Desde la línea de comandos del Editor de consultas o de su cliente PSQL, introduzca la variable `SET aqp=true;` comando.

>[!NOTE]
>
>Debe habilitar el indicador de sesión cada vez que inicie sesión en Platform.

![El Editor de consultas con el comando &#39;SET aqp=true;&#39; resaltado.](../images/essential-concepts/set-session-flag.png)

## Crear un ejemplo de conjunto de datos aleatorio uniforme {#create-a-sample}

Utilice la variable `ANALYZE TABLE` con un nombre de conjunto de datos para crear una muestra aleatoria uniforme a partir de ese conjunto de datos.

La tasa de muestra es el porcentaje de registros tomados del conjunto de datos original. Puede controlar la velocidad de muestreo utilizando la variable `TABLESAMPLE SAMPLERATE` palabras clave. En este ejemplo, el valor de 5,0 equivale a una frecuencia de muestra del 50 %. Un valor de 2,5 equivaldría al 25 % y así sucesivamente.

>[!IMPORTANT]
>
>El sistema permite un máximo de cinco muestras para cada conjunto de datos. Si intenta crear un sexto conjunto de datos de muestra, aparece un mensaje de error en la pantalla que indica que se ha alcanzado el límite de muestra.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Ver la lista de ejemplos {#view-list-of-samples}

Utilice la variable `sample_meta()` para ver la lista de muestras asociadas con una tabla ADLS.

```sql
SELECT sample_meta('example_dataset_name')
```

La lista de ejemplos de conjuntos de datos se muestra en el formato del ejemplo siguiente.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Consultar el conjunto de datos de ejemplo {#query-sample-datasets}

Utilice la variable `{EXAMPLE_DATASET_NAME}` para consultar directamente las tablas de ejemplo. Como alternativa, agregue la variable `WITHAPPROXIMATE` al final de una consulta y Query Service utiliza automáticamente la muestra creada más recientemente.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Eliminar muestras de conjuntos de datos {#delete-a-sample}

La operación de eliminación le permite crear nuevos ejemplos una vez que se ha alcanzado el límite máximo de cinco muestras de conjuntos de datos.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Si tiene varios conjuntos de datos de ejemplo derivados de un conjunto de datos ADLS original, cuando se suelta el original, también se eliminan todos los ejemplos asociados.
