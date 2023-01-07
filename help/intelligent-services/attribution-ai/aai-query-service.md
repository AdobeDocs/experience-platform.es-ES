---
keywords: perspectivas;ai de atribución;perspectivas de ai de atribución;servicio de consulta AAI;consultas de atribución;puntuaciones de atribución
feature: Attribution AI
title: Análisis de puntuaciones de atribución mediante el servicio de consulta
description: Aprenda a utilizar el servicio de consulta de Adobe Experience Platform para analizar las puntuaciones de Attribution AI.
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Análisis de puntuaciones de atribución mediante el servicio de Consulta

Cada fila de los datos representa una conversión, en la que la información de los puntos de contacto relacionados se almacena como una matriz de estructuras en la `touchpointsDetail` para abrir el Navegador.

| Información de Touchpoint | Columna |
| ---------------------- | ------ |
| Nombre del punto de contacto | `touchpointsDetail. touchpointName` |
| Canal de punto de contacto | `touchpointsDetail.touchPoint.mediaChannel` |
| Puntuaciones algorítmicas de Attribution AI de Touchpoint | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Búsqueda de rutas de datos

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo. La variable **[!UICONTROL Conjuntos de datos]** se abre. A continuación, seleccione la **[!UICONTROL Examinar]** y busque el conjunto de datos de salida para sus puntuaciones de Attribution AI.

![Acceso a la instancia](./images/aai-query/datasets_browse.png)

Seleccione el conjunto de datos de salida. Aparece la página de actividad del conjunto de datos.

![página de actividad del conjunto de datos](./images/aai-query/select_preview.png)

En la página de actividad del conjunto de datos, seleccione **[!UICONTROL Vista previa del conjunto de datos]** en la esquina superior derecha para obtener una vista previa de los datos y asegurarse de que se han introducido según lo esperado.

![vista previa del conjunto de datos](./images/aai-query/preview_dataset.JPG)

Después de obtener una vista previa de los datos, seleccione el esquema en el carril derecho. Aparece una ventana emergente con el nombre y la descripción del esquema. Seleccione el hipervínculo del nombre del esquema para redirigir al esquema de puntuación.

![seleccione el esquema](./images/aai-query/select_schema.png)

Con el esquema de puntuación, puede seleccionar o buscar un valor. Una vez seleccionada, la variable **[!UICONTROL Propiedades del campo]** aperturas del carril lateral que permiten copiar la ruta para utilizarla en la creación de consultas.

![copiar la ruta](./images/aai-query/copy_path.png)

## Acceso al servicio de consultas

Para acceder al servicio de consulta desde la interfaz de usuario de Platform, comience por seleccionar **[!UICONTROL Consultas]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Examinar]** pestaña . Se carga una lista de las consultas guardadas anteriormente.

![examinar el servicio de consultas](./images/aai-query/query_tab.png)

A continuación, seleccione **[!UICONTROL Crear consulta]** en la esquina superior derecha. Se carga el Editor de consultas. Con el Editor de consultas puede empezar a crear consultas utilizando los datos de puntuación.

![editor de consultas](./images/aai-query/query_example.png)

Para obtener más información sobre el Editor de consultas, visite [Guía del usuario del Editor de consultas](../../query-service/ui/user-guide.md).

## Plantillas de consulta para análisis de puntuación de atribución

Las consultas siguientes pueden utilizarse como plantilla para distintos escenarios de análisis de puntuación. Debe reemplazar la variable `_tenantId` y `your_score_output_dataset` con los valores adecuados que se encuentran en el esquema de salida de puntuación.

>[!NOTE]
>
> Según la ingesta de sus datos, los valores utilizados a continuación, como `timestamp` puede tener un formato diferente.

### Ejemplos de validación

**Número total de conversiones por evento de conversión (dentro de una ventana de conversión)**

```sql
    SELECT conversionName,
           SUM(scores.firstTouch) as total_conversions,
           SUM(scores.algorithmicSourced) as total_attributed_conversions
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName
                    as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16'
      AND
        conversion_timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

**Número total de eventos de solo conversión (dentro de una ventana de conversión)**

```sql
    SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        COUNT(1) as convOnly_cnt
    FROM
        your_score_output_dataset
    WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

### Ejemplo de análisis de tendencias

**Número de conversiones por día**

```sql
    SELECT conversionName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.firstTouch) as convertion_cnt
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    GROUP BY
        conversionName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, DATE(conversion_timestamp)
    LIMIT 20
```

### Ejemplo de análisis de distribución

**Cantidad de puntos de contacto en rutas de conversión por tipo definido (dentro de una ventana de conversión)**

```sql
    SELECT conversionName,
           touchpointName,
           COUNT(1) as tp_count
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14' AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, tp_count DESC
```

### Ejemplos de generación de perspectiva

**Desglose de unidades incrementales por punto de contacto y fecha de conversión (dentro de una ventana de conversión)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(conversion_timestamp)
```

**Desglose de unidades incrementales por punto de contacto y fecha de punto de contacto (dentro de una ventana de conversión)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(touchpoint.timestamp) as touchpoint_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    LIMIT 20
```

**Puntuaciones agregadas para un determinado tipo de punto de contacto para todos los modelos de puntuación (dentro de una ventana de conversión)**

```sql
    SELECT
           conversionName,
           touchpointName,
           SUM(scores.algorithmicSourced) as total_incremental_units,
           SUM(scores.algorithmicInfluenced) as total_influenced_units,
           SUM(scores.uShape) as total_uShape_units,
           SUM(scores.decayUnits) as total_decay_units,
           SUM(scores.linear) as total_linear_units,
           SUM(scores.lastTouch) as total_lastTouch_units,
           SUM(scores.firstTouch) as total_firstTouch_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName = 'display'
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, touchpointName
```

**Avanzado: análisis de longitud de ruta**

Obtenga una distribución de longitud de ruta para cada tipo de evento de conversión:

```sql
    WITH agg_path AS (
          SELECT
            _tenantId.your_score_output_dataset.conversionName as conversionName,
            sum(size(_tenantId.your_score_output_dataset.touchpointsDetail)) as path_length
          FROM
            your_score_output_dataset
          WHERE
            _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
            timestamp >= '2020-07-16' AND
            timestamp <  '2020-10-14'
          GROUP BY
            _tenantId.your_score_output_dataset.conversionName,
            eventMergeId
    )
    SELECT
        conversionName,
        path_length,
        count(1) as conversionPath_count
    FROM
        agg_path
    GROUP BY
        conversionName, path_length
    ORDER BY
        conversionName, path_length
```

**Avanzado : número distinto de puntos de contacto en el análisis de rutas de conversión**

Obtenga la distribución del número de puntos de contacto diferentes en una ruta de conversión para cada tipo de evento de conversión:

```sql
    WITH agg_path AS (
      SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        size(array_distinct(flatten(collect_list(_tenantId.your_score_output_dataset.touchpointsDetail.touchpointName)))) as num_dist_tp
      FROM
        your_score_output_dataset
      WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
      GROUP BY
        _tenantId.your_score_output_dataset.conversionName,
        eventMergeId
    )
    SELECT
        conversionName,
        num_dist_tp,
        count(1) as conversionPath_count
    FROM
     agg_path
    GROUP BY
        conversionName, num_dist_tp
    ORDER BY
        conversionName, num_dist_tp
```

### Ejemplo de aplanamiento y explosión de esquema

Esta consulta aplana la columna de estructura en varias columnas singulares y explota las matrices en varias filas. Esto ayuda a transformar las puntuaciones de atribución en un formato CSV. El resultado de esta consulta tiene una conversión y uno de los puntos de contacto correspondientes a esa conversión en cada fila.

>[!TIP]
>
> En este ejemplo, debe reemplazar `{COLUMN_NAME}` además de `_tenantId` y `your_score_output_dataset`. La variable `COLUMN_NAME` puede utilizar los valores de los nombres de columna opcionales (columnas de informes) que se añadieron durante la configuración de la instancia de Attribution AI. Revise el esquema de salida de puntuación para encontrar la variable `{COLUMN_NAME}` valores necesarios para completar esta consulta.

```sql
SELECT 
  segmentation,
  conversionName,
  scoreCreatedTime,
  aaid, _id, eventMergeId,
  conversion.eventType as conversion_eventType,
  conversion.quantity as conversion_quantity,
  conversion.eventSource as conversion_eventSource,
  conversion.priceTotal as conversion_priceTotal,
  conversion.timestamp as conversion_timestamp,
  conversion.geo as conversion_geo,
  conversion.receivedTimestamp as conversion_receivedTimestamp,
  conversion.dataSource as conversion_dataSource,
  conversion.productType as conversion_productType,
  conversion.passThrough.{COLUMN_NAME} as conversion_passThru_column,
  conversion.skuId as conversion_skuId,
  conversion.product as conversion_product,
  touchpointName,
  touchPoint.campaignGroup as tp_campaignGroup, 
  touchPoint.mediaType as tp_mediaType,
  touchPoint.campaignTag as tp_campaignTag,
  touchPoint.timestamp as tp_timestamp,
  touchPoint.geo as tp_geo,
  touchPoint.receivedTimestamp as tp_receivedTimestamp,
  touchPoint.passThrough.{COLUMN_NAME} as tp_passThru_column,
  touchPoint.campaignName as tp_campaignName,
  touchPoint.mediaAction as tp_mediaAction,
  touchPoint.mediaChannel as tp_mediaChannel,
  touchPoint.eventid as tp_eventid,
  scores.*
FROM (
  SELECT
        _tenantId.your_score_output_dataset.segmentation,
        _tenantId.your_score_output_dataset.conversionName,
        _tenantId.your_score_output_dataset.scoreCreatedTime,
        _tenantId.your_score_output_dataset.conversion,
        _id,
        eventMergeId,
        map_values(identityMap)[0][0].id as aaid,
        inline(_tenantId.your_score_output_dataset.touchpointsDetail)
  FROM
        your_score_output_dataset
)
```
