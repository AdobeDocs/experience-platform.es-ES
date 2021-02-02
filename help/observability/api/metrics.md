---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Extremo de métricas
topic: developer guide
description: Obtenga información sobre cómo recuperar métricas de observabilidad en Experience Platform mediante la API de perspectivas de observación.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 2%

---


# Extremo de métricas

Las métricas de capacidad de observación proporcionan perspectivas sobre las estadísticas de uso, las tendencias históricas y los indicadores de rendimiento para diversas funciones de Adobe Experience Platform. El extremo `/metrics` en [!DNL Observability Insights API] le permite recuperar mediante programación los datos de métricas para la actividad de su organización en [!DNL Platform].

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de API de muestra en este documento e información importante sobre los encabezados necesarios que se necesitan para realizar llamadas exitosas a cualquier API [!DNL Experience Platform].

## Recuperar métricas de observabilidad

Existen dos métodos admitidos para recuperar datos de métricas mediante la API:

* [Versión 1](#v1): Especifique las métricas mediante parámetros de consulta.
* [Versión 2](#v2): Especifique y aplique filtros a las métricas mediante una carga útil JSON.

### Versión 1 {#v1}

Puede recuperar datos de métricas realizando una solicitud de GET al extremo `/metrics`, especificando las métricas mediante el uso de parámetros de consulta.

**Formato API**

Se debe proporcionar al menos una métrica en el parámetro `metric`. Otros parámetros de consulta son opcionales para filtrar los resultados.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parámetro | Descripción |
| --- | --- |
| `{METRIC}` | La métrica que desee exponer. Al combinar varias métricas en una sola llamada, debe utilizar un símbolo de unión (`&`) para separar métricas individuales. Por ejemplo, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | El identificador de un recurso [!DNL Platform] concreto cuyas métricas desea exponer. Esta ID puede ser opcional, obligatoria o no aplicable en función de las métricas utilizadas. Consulte el [apéndice](#available-metrics) para obtener una lista de las métricas disponibles, incluidos los ID admitidos (tanto obligatorios como opcionales) para cada métrica. |
| `{DATE_RANGE}` | El intervalo de fechas de las métricas que desea exponer, en formato ISO 8601 (por ejemplo, `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de objetos, cada uno de los cuales contiene una marca de tiempo dentro de la `dateRange` proporcionada y los valores correspondientes para las métricas especificadas en la ruta de la solicitud. Si se incluye el `id` de un recurso [!DNL Platform] en la ruta de solicitud, los resultados se aplicarán solamente a ese recurso en particular. Si se omite `id`, los resultados se aplicarán a todos los recursos aplicables dentro de la organización de IMS.

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### Versión 2 {#v2}

Puede recuperar datos de métricas realizando una solicitud de POST al extremo `/metrics`, especificando las métricas que desee recuperar en la carga útil.

**Formato API**

```http
POST /metrics
```

**Solicitud**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `start` | La fecha y hora más temprana desde la cual se recuperan los datos de métricas. |
| `end` | Fecha y hora más recientes desde las cuales recuperar datos de métricas. |
| `granularity` | Campo opcional que indica el intervalo de tiempo por el que dividir los datos de métricas. Por ejemplo: un valor de `DAY` devuelve métricas por cada día entre la fecha `start` y la fecha `end`, mientras que un valor de `MONTH` agruparía los resultados de la métrica por mes. Al utilizar este campo, también se debe proporcionar una propiedad `downsample` correspondiente para indicar la función de agregación mediante la cual se agrupan los datos. |
| `metrics` | Matriz de objetos, una para cada métrica que desee recuperar. |
| `name` | Nombre de una métrica reconocida por Perspectivas de la Observabilidad. Consulte el [apéndice](#available-metrics) para obtener una lista completa de los nombres de métricas aceptados. |
| `filters` | Campo opcional que permite filtrar métricas por conjuntos de datos específicos. El campo es una matriz de objetos (uno para cada filtro), con cada objeto con las siguientes propiedades: <ul><li>`name`:: Tipo de entidad con la que se filtran las métricas. Actualmente, solo se admite `dataSets`.</li><li>`value`:: ID de uno o varios conjuntos de datos. Se pueden proporcionar varios ID de conjuntos de datos como una sola cadena, con cada ID separado por caracteres de barras verticales (`|`).</li><li>`groupBy`:: Cuando se establece en true, indica que el correspondiente  `value` representa varios conjuntos de datos cuyos resultados de métricas deben devolverse por separado. Si se establece en false, los resultados de las métricas para esos conjuntos de datos se agrupan.</li></ul> |
| `aggregator` | Especifica la función de agregación que debe utilizarse para agrupar varios registros de series temporales en resultados únicos. Para obtener información detallada sobre los agregadores disponibles, consulte la [documentación de OpenTSDB](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html). |
| `downsample` | Campo opcional que permite especificar una función de agregación para reducir la tasa de muestreo de datos de métricas mediante la ordenación de campos en intervalos (o &quot;bloques&quot;). El intervalo para la disminución de resolución se determina mediante la propiedad `granularity`. Para obtener información detallada sobre la disminución de resolución, consulte la [documentación de OpenTSDB](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html). |

**Respuesta**

Una respuesta correcta devuelve los puntos de datos resultantes para las métricas y filtros especificados en la solicitud.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `metricResponses` | Matriz cuyos objetos representan cada una de las métricas especificadas en la solicitud. Cada objeto contiene información sobre la configuración del filtro y los datos de métricas devueltos. |
| `metric` | Nombre de una de las métricas proporcionadas en la solicitud. |
| `filters` | Configuración del filtro para la métrica especificada. |
| `datapoints` | Una matriz cuyos objetos representan los resultados de la métrica y los filtros especificados. El número de objetos de la matriz depende de las opciones de filtro proporcionadas en la solicitud. Si no se proporcionaron filtros, la matriz sólo contendrá un único objeto que represente todos los conjuntos de datos. |
| `groupBy` | Si se especificaron varios conjuntos de datos en la propiedad `filter` de una métrica y la opción `groupBy` se estableció en true en la solicitud, este objeto contendrá el ID del conjunto de datos al que se aplica la propiedad `dps` correspondiente.<br><br>Si este objeto aparece vacío en la respuesta, la  `dps` propiedad correspondiente se aplica a todos los conjuntos de datos proporcionados en la  `filters` matriz (o a todos los conjuntos de datos en  [!DNL Platform] caso de que no se hayan proporcionado filtros). |
| `dps` | Los datos devueltos para la métrica, el filtro y el intervalo de tiempo determinados. Cada clave de este objeto representa una marca de tiempo con un valor correspondiente para la métrica especificada. El período de tiempo entre cada punto de datos depende del valor `granularity` especificado en la solicitud. |

## Apéndice

La siguiente sección contiene información adicional sobre cómo trabajar con el extremo `/metrics`.

### Métricas disponibles {#available-metrics}

Las siguientes tablas lista todas las métricas expuestas por [!DNL Observability Insights], desglosadas por el servicio [!DNL Platform]. Cada métrica incluye una descripción y un parámetro de consulta de ID aceptado.

>[!NOTE]
>
>Todos los parámetros de consulta de ID enumerados son opcionales a menos que se indique lo contrario.

#### [!DNL Data Ingestion] {#ingestion}

La siguiente tabla describe las métricas de Adobe Experience Platform [!DNL Data Ingestion]. Las métricas de **negrita** están transmitiendo métricas de inserción.

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Número total de conjuntos de datos creados. | N/D |
| timeseries.ingestion.dataset.size | Tamaño acumulado de todos los datos ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.ingestion.dataset.dailysize | Tamaño de los datos ingestados en base al uso diario para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.ingestion.dataset.batchfailed.count | Número de lotes en los que se ha producido un error en un conjunto de datos o en todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.ingestion.dataset.batchsuccess.count | Número de lotes ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.ingestion.dataset.recordsuccess.count | Número de registros ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.total.messages.rate** | Número total de mensajes para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.valid.messages.rate** | Número total de mensajes válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.Invalid.messages.rate** | Número total de mensajes no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.type.count** | Número total de mensajes de &quot;tipo&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.range.count** | Número total de mensajes de &quot;intervalo&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.format.count** | Número total de mensajes de &quot;formato&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.pattern.count** | Número total de mensajes de &quot;patrón&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.presence.count** | Número total de mensajes de &quot;presencia&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.enum.count** | Número total de mensajes &quot;enum&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.unclassi.count** | Número total de mensajes &quot;no clasificados&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.validation.categoría.unknown.count** | Número total de mensajes &quot;desconocidos&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| **timeseries.data.collection.inlet.total.messages.received** | Número total de mensajes recibidos para una entrada de datos o para todas las entradas de datos. | ID de entrada |
| **timeseries.data.collection.inlet.total.messages.size.received** | Tamaño total de los datos recibidos para una entrada de datos o para todas las entradas de datos. | ID de entrada |
| **timeseries.data.collection.inlet.success** | Número total de llamadas HTTP correctas a una entrada de datos o a todas las entradas de datos. | ID de entrada |
| **timeseries.data.collection.inlet.fail** | Número total de llamadas HTTP fallidas a una entrada de datos o a todas las entradas de datos. | ID de entrada |

#### [!DNL Identity Service] {#identity}

La siguiente tabla describe las métricas de Adobe Experience Platform [!DNL Identity Service].

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Número de registros escritos en su fuente de datos por [!DNL Identity Service], para un conjunto de datos o todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.identity.dataset.recordfailed.count | El número de registros falló por [!DNL Identity Service], para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Número de registros de identidad que se han ingerido correctamente para una Área de nombres. | ID de Área de nombres (**Requerido**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Número de registros de identidad con error de una Área de nombres. | ID de Área de nombres (**Requerido**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidad omitidos por una Área de nombres. | ID de Área de nombres (**Requerido**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de una Área de nombres. | ID de Área de nombres (**Requerido**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Número de identidades gráficas únicas almacenadas en el gráfico de identidad de su organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS para una intensidad de gráfico determinada (&quot;desconocida&quot;, &quot;débil&quot; o &quot;fuerte&quot;). | Intensidad del gráfico (**Requerido**) |

#### [!DNL Privacy Service] {#privacy}

La siguiente tabla describe las métricas de Adobe Experience Platform [!DNL Privacy Service].

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Número total de trabajos creados a partir del RGPD. | ENV (**Requerido**) |
| timeseries.gdpr.jobs.completedjobs.count | Número total de trabajos completados del RGPD. | ENV (**Requerido**) |
| timeseries.gdpr.jobs.errorjobs.count | Número total de trabajos de error del RGPD. | ENV (**Requerido**) |

#### [!DNL Query Service] {#query}

La siguiente tabla describe las métricas de Adobe Experience Platform [!DNL Query Service].

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Número total de consultas programadas no recurrentes. | N/D |
| timeseries.queryservice.query.scheduledrecurring.count | Número total de consultas programadas recurrentes. | N/D |
| timeseries.queryservice.query.batchquery.count | Número total de consultas por lotes ejecutadas. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Número total de consultas programadas ejecutadas. | N/D |
| timeseries.queryservice.query.interactivequery.count | Número total de consultas interactivas ejecutadas. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Número total de consultas por lotes ejecutadas desde PSQL. | N/D |

#### [!DNL Real-time Customer Profile] {#profile}

La siguiente tabla describe las métricas de [!DNL Real-time Customer Profile].

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Número de registros leídos desde [!DNL Data Lake] por [!DNL Profile], para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros escritos en su fuente de datos por [!DNL Profile], para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.recordfailed.count | El número de registros falló por [!DNL Profile], para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.batchsuccess.count | Número de [!DNL Profile] lotes ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.batchfailed.count | El número de lotes [!DNL Profile] falló para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| platform.ups.ingest.streaming.request.m1_rate | Tasa de solicitud entrante. | Organización IMS (**Requerida**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Tasa de éxito de inserción. | Organización IMS (**Requerida**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Tasa de nuevos registros ingeridos para un conjunto de datos. | Id. de conjunto de datos (**Requerido**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Tasa de registros con marca de hora desordenada para crear solicitudes para un conjunto de datos. | Id. de conjunto de datos (**Requerido**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Marca de hora para la última solicitud de registro de creación de un conjunto de datos. | Id. de conjunto de datos (**Requerido**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Tasa de registros con marca de hora desordenada para la solicitud de actualización de un conjunto de datos. | Id. de conjunto de datos (**Requerido**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Marca de hora para la última solicitud de registro de actualización de un conjunto de datos. | Id. de conjunto de datos (**Requerido**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Tamaño promedio del registro. | Organización IMS (**Requerida**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Tasa de solicitudes de actualización para registros ingestados para un conjunto de datos. | Id. de conjunto de datos (**Requerido**) |

### Mensajes de error

Las respuestas del extremo `/metrics` pueden devolver mensajes de error bajo ciertas condiciones. Estos mensajes de error se devuelven en el siguiente formato:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `title` | Una cadena que contiene el mensaje de error y el posible motivo por el que se ha producido. |
| `report` | Contiene información contextual sobre el error, incluido el simulador de pruebas y la organización de IMS que se está utilizando en la operación que lo activó. |

La siguiente tabla lista los distintos códigos de error que puede devolver la API:

| Código de error | Título | Descripción |
| --- | --- | --- |
| `INSGHT-1000-400` | Carga útil de solicitud incorrecta | Se produjo un error en la carga útil de la solicitud. Asegúrese de que coincide exactamente con el formato de carga útil como se muestra [por encima](#v2). Cualquiera de las posibles razones puede provocar el déclencheur de este error:<ul><li>Faltan campos obligatorios como `aggregator`</li><li>Métricas no válidas</li><li>La solicitud contiene un agregador no válido</li><li>Una fecha de inicio se produce después de una fecha de finalización</li></ul> |
| `INSGHT-1001-400` | Error en la consulta de métricas | Se produjo un error al intentar realizar la consulta de la base de datos de métricas, debido a una solicitud incorrecta o a que la consulta misma no se puede analizar. Asegúrese de que la solicitud tiene el formato correcto antes de intentarlo de nuevo. |
| `INSGHT-1001-500` | Error en la consulta de métricas | Se produjo un error al intentar consulta de la base de datos de métricas, debido a un error del servidor. Intente la solicitud de nuevo y, si el problema persiste, póngase en contacto con el servicio de soporte técnico de Adobe. |
| `INSGHT-1002-500` | Error de servicio | No se pudo procesar la solicitud debido a un error interno. Intente la solicitud de nuevo y, si el problema persiste, póngase en contacto con el servicio de soporte técnico de Adobe. |
| `INSGHT-1003-401` | Error de validación del Simulador para pruebas | No se pudo procesar la solicitud debido a un error de validación del simulador para pruebas. Asegúrese de que el nombre del simulador para pruebas proporcionado en el encabezado `x-sandbox-name` representa un simulador para pruebas válido y habilitado para su organización de IMS antes de intentar la solicitud de nuevo. |
