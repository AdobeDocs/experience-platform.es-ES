---
title: Filtrado de bots mediante estadísticas y aprendizaje automático
description: Aprenda a utilizar las estadísticas de Data Distiller y el aprendizaje automático para identificar y filtrar la actividad de bots y garantizar un análisis preciso y una integridad de datos mejorada.
source-git-commit: a8abbf61bdc646c0834c296a64b27c71c98ea1d3
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Filtrado de bots mediante estadísticas y aprendizaje automático

Las aplicaciones prácticas del filtrado de bots abarcan varias industrias. En el comercio electrónico, mejora la fiabilidad de las métricas de tasa de conversión, los sitios web de noticias pueden beneficiarse de la mitigación de las métricas de participación falsas y las redes de publicidad pueden garantizar una facturación justa. Para mantener análisis precisos y garantizar la integridad de los datos en el flujo de navegación o en los datos del tráfico web, debe abordar la actividad de bots. Puede garantizar datos de análisis de alta calidad mediante el uso de Data Distiller para implementar un filtrado eficaz de bots y eliminar el tráfico no deseado.

Este documento proporciona una guía completa para identificar y filtrar la actividad de bots mediante SQL y técnicas de aprendizaje automático. Presenta una progresión de enfoques complementarios, empezando por el filtrado básico y avanzando hacia la detección y evaluación basada en el aprendizaje automático. Adopte este sólido marco para mejorar la detección de bots y mantener la integridad de los datos.

## Comprender la actividad de bots {#understand-bot-activity}

La actividad de bots se puede identificar detectando picos en las acciones del usuario dentro de intervalos de tiempo específicos. Por ejemplo, un exceso de clics realizados por un solo usuario en un corto periodo de tiempo podría indicar el comportamiento de bots. Los dos atributos clave utilizados en el filtrado de bots son:

- **ECID (ID de visitante de Experience Cloud):** Identificador universal y persistente que identifica a los visitantes.
- **Marca de tiempo:** Fecha y hora en que se produce una actividad en el sitio web.

Los ejemplos siguientes muestran cómo utilizar SQL y las técnicas de aprendizaje automático para identificar, refinar y predecir la actividad de bots. Utilice estos métodos para mejorar la integridad de los datos y garantizar análisis procesables.

## Filtrado de bots basado en SQL {#sql-based-bot-filtering}

Este ejemplo de filtrado de bots basado en SQL muestra cómo utilizar consultas SQL para definir umbrales y detectar actividad de bots basada en reglas predefinidas. Este enfoque fundamental ayuda a identificar anomalías en el tráfico web al eliminar una actividad inusual. Al personalizar las reglas de detección con umbrales e intervalos definidos, puede adaptar de forma eficaz el filtrado de bots para adaptarlo a sus patrones de tráfico específicos.

### Definición de umbrales para la actividad de bots {#define-thresholds}

Comience por analizar el conjunto de datos para identificar y categorizar el comportamiento del usuario. Céntrese en atributos como ECID, timestamp y `webPageDetails.name` (el nombre de la página web visitada) para agrupar las acciones de los usuarios y detectar patrones que indiquen actividad de bots.

La siguiente consulta SQL muestra cómo aplicar el umbral de más de 60 clics en un minuto para identificar actividad sospechosa:

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### Expandir a varios intervalos {#expand-to-multiple-intervals}

A continuación, defina diferentes intervalos de tiempo para los umbrales. Estos intervalos podrían incluir:

- Intervalo de **1 minuto:** hasta 60 clics.
- **Intervalo de 5 minutos:** hasta 300 clics.
- **Intervalo de 30 minutos:** hasta 1800 clics.

La siguiente consulta SQL crea una vista denominada `analytics_events_clicks_count_criteria` para administrar los umbrales en varios intervalos. La instrucción consolida los recuentos de clics para intervalos de 1 minuto, 5 minutos y 30 minutos en un conjunto de datos estructurado y marca la actividad de bots potencial en función de umbrales predefinidos.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

La instrucción combina los datos de `table_count_1_min`, `table_count_5_mins` y `table_count_30_mins` mediante el valor `mcid` y la página web. A continuación, consolida los recuentos de clics de cada usuario en varios intervalos de tiempo para proporcionar una vista completa de la actividad del usuario. Finalmente, la lógica de indicación identifica a los usuarios que exceden los 50 clics en un minuto y los marca como bots (`isBot = 1`).

### Estructura del conjunto de datos salida

El conjunto de datos de salida está estructurado con campos planos y anidados. Esta estructura permite flexibilidad al detectar tráfico anómalo y admite estrategias de filtrado avanzadas que utilizan SQL y aprendizaje automático. Los campos anidados incluyen `count` y `web`, que encapsulan detalles granulares sobre umbrales de actividad y páginas web. La captura de estas métricas significa que las funciones se pueden extraer fácilmente para tareas de aprendizaje y predicción.

El siguiente diagrama de esquema describe la estructura del conjunto de datos resultante y destaca cómo se pueden utilizar los campos anidados y planos para un procesamiento eficaz y la detección de bots.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### El conjunto de datos de salida que se utilizará para la formación.

El resultado de esta expresión puede ser similar a la tabla que se muestra a continuación. En la tabla, la columna `isBot` actúa como una etiqueta que distingue entre actividad de bots y actividad que no es de bots.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## Funciones estadísticas avanzadas para filtrado de bots {#statistical-functions-for-bot-filtering}

Este segundo ejemplo se basa en el filtrado SQL básico mediante la incorporación de técnicas de aprendizaje automático para refinar los umbrales y mejorar la precisión del filtrado. Mediante el uso de funciones estadísticas avanzadas, como el análisis de regresión o los algoritmos de agrupación, este enfoque introduce capacidades predictivas que se pueden utilizar para desarrollar modelos para gestionar conjuntos de datos complejos con mayor precisión.

### Crear un conjunto de datos de formación {#build-a-training-dataset}

En primer lugar, prepare un conjunto de datos con estructuras planas y anidadas que el modelo de aprendizaje automático pueda utilizar (como se ha descrito anteriormente). Encontrará más instrucciones sobre cómo hacerlo en la [Documentación sobre trabajar con estructuras de datos anidadas](../../key-concepts/nested-data-structures.md). Agrupe los datos por marca de tiempo, ID de usuario y nombre de página web para identificar patrones en la actividad de bots.

### Utilizar las cláusulas TRANSFORM y OPTIONS para la creación de modelos {#transform-and-preprocess}

Para transformar su conjunto de datos y configurar su modelo de aprendizaje automático de forma eficaz, siga los pasos a continuación. Los pasos detallan cómo gestionar valores nulos, preparar funciones y definir los parámetros del modelo para un rendimiento óptimo.

>[!TIP]
>
>Para obtener más información sobre cómo usar transformaciones y preprocesar los datos, consulte la [documentación sobre técnicas de transformación de características](../feature-transformation.md).

1. Para rellenar valores nulos en columnas numéricas, de cadena y booleanas, use las funciones `numeric_imputer`, `string_imputer` y `boolean_imputer` respectivamente. Este paso garantiza que el algoritmo de aprendizaje automático pueda procesar los datos sin errores.
2. Aplique transformaciones de funciones para preparar los datos para el modelado. Aplique `binarized`, `quantile_discretizer` o `string_indexer` para categorizar o estandarizar las columnas. A continuación, agregue el resultado de los imputadores (`numeric_imputer` y `string_imputer`) en transformadores subsiguientes como `string_indexer` o `quantile_discretizer` para crear características significativas.
3. Utilice la función `vector_assembler` para combinar las columnas transformadas en una sola columna de característica. Luego escale las características usando `min_max_scaler` para normalizar los valores y obtener un mejor rendimiento del modelo. Nota: En el ejemplo de SQL, la última transformación mencionada dentro de la cláusula TRANSFORM se convierte en la columna de función utilizada por el modelo de aprendizaje automático.
4. Especifique el tipo de modelo y cualquier otro hiperparámetro en la cláusula de OPTIONS. Por ejemplo, `decision_tree_classifier` se eligió aquí debido a que se trata de un problema de clasificación. Otros parámetros como `max_depth` se han ajustado (`MAX_DEPTH=4`) para ajustar el modelo y obtener un mejor rendimiento.
5. Combine características y etiquete los datos de salida. Utilice la cláusula SELECT para especificar el conjunto de datos para aprendizaje. Esta cláusula debe incluir las columnas de características (`count_per_id`, `web`, `id`) y la columna de etiqueta (`isBot`), que indica si es probable que una acción sea un bot.

Su instrucción puede tener un aspecto similar al ejemplo siguiente.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**Resultado**

En los resultados que se muestran a continuación, el modelo `bot_filtering_model` se ha creado correctamente con un identificador, un nombre y una versión únicos. Este resultado sirve como referencia para el seguimiento y la administración de modelos. Utilice estas referencias para identificar la configuración y la versión exactas que se requieren para las predicciones o evaluaciones.

```console
           Created Model ID           |       Created Model       | Version
--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### Evaluar el modelo entrenado {#evaluate-trained-model}

Después de crear el modelo, utilice el comando `MODEL_EVALUATE` para evaluar su rendimiento. Este paso garantiza que el modelo cumpla los requisitos de precisión y rendimiento para detectar la actividad de bots.

Utilice los siguientes argumentos en el comando SQL para evaluar el modelo:

1. Especifique el nombre del modelo (`bot_filtering_model`) para indicar qué modelo evaluar. Este nombre debe coincidir con el que creó anteriormente con el comando `CREATE MODEL`.
2. Proporcione la versión del modelo (`1`) en el segundo argumento para especificar la versión del modelo que desea evaluar. Si existen varias versiones, esto garantiza que se utilice la versión correcta.
3. Incluya el conjunto de datos de evaluación para definir el conjunto de datos para la evaluación. Asegúrese de que el conjunto de datos incluya las mismas columnas de características (`count_per_id`, `web`, `id`) y la columna de etiqueta (`isBot`) utilizadas durante la formación.

>[!NOTE]
>
>Las transformaciones aplicadas durante la formación del modelo se aplican automáticamente durante la evaluación.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**Resultado**

La respuesta incluye métricas como precisión, precisión, recuperación y AUC-ROC. Los resultados confirman si el modelo tuvo un buen desempeño o no.

>[!NOTE]
>
>Los valores en el rango 0-1 representan proporciones o probabilidades, con 1,0 que indica un rendimiento perfecto.

```console
auc_roc | accuracy | precision | recall
---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **Métrica** | **Descripción** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | Esta métrica indica la eficacia con la que el modelo puede clasificar bots y no bots. Se utiliza ampliamente para evaluar modelos de clasificación. |
| `accuracy` | El porcentaje de predicciones correctas realizadas por el modelo. |
| `precision` | La proporción de predicciones verdaderas de bots entre todos los bots predichos. |
| `recall` | La proporción de bots reales detectados de todos los bots reales. |

>[!TIP]
>
>Para su uso en entornos limitados de producción, considere la posibilidad de evaluar el modelo en conjuntos de datos de prueba para garantizar que se generalice de forma eficaz.

### Predecir actividad de bots {#predict-bot-activity}

Utilice el comando `MODEL_PREDICT` con el modelo entrenado para identificar qué usuarios (`id`) son bots. Siga los pasos a continuación para generar predicciones sobre la identificación de la actividad de bots:

1. Utilice el nombre del modelo (`bot_filtering_model`) en el primer argumento para especificar el modelo que se va a utilizar para las predicciones.
2. Especifique la versión del modelo (`1`) en el segundo argumento para asegurarse de que se utiliza la versión correcta del modelo.
3. Para proporcionar los datos correctos para las predicciones, utilice una instrucción SELECT para especificar las columnas de características (`count_per_id`, `web`, `id`). No incluya la columna de etiqueta (`isBot`) porque el modelo generará predicciones para este campo.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**Resultado**

La respuesta incluye predicciones para cada usuario (`id`) junto con detalles sobre su actividad y el resultado de clasificación del modelo. Este resultado permite un examen detallado del comportamiento del usuario y la clasificación del modelo de la actividad de bots.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

La siguiente tabla explica cada métrica:

| Nombre de columna | Descripción |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | El identificador único de cada usuario. |
| `count.one_minute` | Los recuentos de clics agregados para intervalos de 1 minuto. |
| `count.five_minute` | Los recuentos de clics agregados para intervalos de 5 minutos. |
| `count.thirty_minute` | El número de clics agregados corresponde a intervalos de 30 minutos. |
| `web.webpagedetails.name` | Nombre de la página web visitada. Esto proporciona contexto para la actividad del usuario. |
| `prediction` | La predicción del modelo. Un resultado de `1.0` indica que el usuario está marcado como bot según sus patrones de actividad. |

## Administrar los modelos {#manage-models}

Para administrar los modelos de aprendizaje automático, utilice las palabras clave SQL que se indican en la sección siguiente.

### Lista de modelos disponibles {#list-available-models}

Administre y revise los modelos de forma eficaz con el comando `SHOW MODELS;`. Este comando enumera todos los modelos de aprendizaje automático que se han creado en el espacio de trabajo actual. El resultado proporciona una descripción general de los modelos disponibles e incluye sus nombres, versiones y otros metadatos.

```sql
SHOW MODELS;
```

### Eliminar modelos {#delete-models}

Para liberar recursos y asegurarse de que solo se mantienen los modelos relevantes, utilice el comando `DROP MODEL` para quitar los modelos obsoletos o innecesarios. Este comando elimina cualquier modelo de aprendizaje automático especificado después de las palabras clave. En el ejemplo siguiente, `bot_filtering_model` se quita del sistema.

```sql
DROP MODEL bot_filtering_model;
```

## Pasos siguientes

Al leer este documento, ha aprendido a identificar y filtrar la actividad de bots mediante SQL y técnicas de aprendizaje automático mediante métodos de Data Distiller. A continuación, aplique estos conceptos a sus conjuntos de datos y automatice el reciclaje del modelo para una mejora continua.
