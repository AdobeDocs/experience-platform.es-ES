---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Métricas disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# Extremo de métricas

Las métricas de capacidad de observación proporcionan perspectivas sobre las estadísticas de uso, las tendencias históricas y los indicadores de rendimiento para diversas funciones de Adobe Experience Platform. El `/metrics` punto final del [!DNL Observability Insights API] permite recuperar mediante programación datos de métricas para la actividad de su organización en [!DNL Platform].

## Primeros pasos

El punto final de API utilizado en esta guía forma parte de la [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Antes de continuar, consulte la guía [de](./getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Recuperar métricas de observabilidad

Puede recuperar métricas de observabilidad realizando una solicitud de GET al `/metrics` extremo en la [!DNL Observability Insights] API.

**Formato API**

Cuando se utiliza el extremo, se debe proporcionar al menos un parámetro de solicitud de métrica. `/metrics` Otros parámetros de consulta son opcionales para filtrar los resultados.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parámetro | Descripción |
| --- | --- |
| `{METRIC}` | La métrica que desee exponer. Al combinar varias métricas en una sola llamada, debe utilizar un símbolo (`&`) para separar métricas individuales. Por ejemplo, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | Identificador de un recurso concreto [!DNL Platform] cuyas métricas desea exponer. Esta ID puede ser opcional, obligatoria o no aplicable en función de las métricas utilizadas. Consulte el [apéndice](#available-metrics) para ver una lista de las métricas disponibles, así como los ID admitidos (tanto obligatorios como opcionales) para cada métrica. |
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

Una respuesta correcta devuelve una lista de objetos, cada uno de los cuales contiene una marca de tiempo dentro de los valores proporcionados `dateRange` y correspondientes para las métricas especificadas en la ruta de la solicitud. Si la ruta `id` de solicitud incluye el nombre de un [!DNL Platform] recurso, los resultados se aplicarán solamente a ese recurso en particular. Si `id` se omite, los resultados se aplicarán a todos los recursos aplicables dentro de la organización de IMS.

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

## Apéndice

La siguiente sección contiene información adicional sobre cómo trabajar con el `/metrics` punto final.

### Métricas disponibles {#available-metrics}

Las siguientes tablas lista todas las métricas expuestas por [!DNL Observability Insights], desglosadas por [!DNL Platform] servicio. Cada métrica incluye una descripción y un parámetro de consulta de ID aceptado.

>[!NOTE]
>
>Todos los parámetros de consulta de ID enumerados son opcionales a menos que se indique lo contrario.

#### [!DNL Data Ingestion] {#ingestion}

La siguiente tabla describe las métricas de Adobe Experience Platform [!DNL Data Ingestion]. Las métricas en **negrita** son métricas de ingesta de flujo continuo.

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
| timeseries.identity.dataset.recordsuccess.count | Número de registros escritos en la fuente de datos por [!DNL Identity Service], para un conjunto de datos o todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.identity.dataset.recordfailed.count | Número de registros con errores por [!DNL Identity Service], para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Número de registros de identidad que se han ingerido correctamente para una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Número de registros de identidad con error de una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidad omitidos por una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Número de identidades gráficas únicas almacenadas en el gráfico de identidad de su organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS para una intensidad de gráfico determinada (&quot;desconocida&quot;, &quot;débil&quot; o &quot;fuerte&quot;). | Intensidad del gráfico (**obligatoria**) |

#### [!DNL Privacy Service] {#privacy}

La siguiente tabla describe las métricas de Adobe Experience Platform [!DNL Privacy Service].

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Número total de trabajos creados a partir del RGPD. | ENV (**requerido**) |
| timeseries.gdpr.jobs.completedjobs.count | Número total de trabajos completados del RGPD. | ENV (**requerido**) |
| timeseries.gdpr.jobs.errorjobs.count | Número total de trabajos de error del RGPD. | ENV (**requerido**) |

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
| timeseries.profiles.dataset.recordread.count | Número de registros leídos desde el [!DNL Data Lake] por, [!DNL Profile]para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros escritos en la fuente de datos por [!DNL Profile], para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.recordfailed.count | Número de registros con errores por [!DNL Profile], para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.batchsuccess.count | Número de [!DNL Profile] lotes ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos |
| timeseries.profiles.dataset.batchfailed.count | Número de [!DNL Profile] lotes en los que se ha producido un error en un conjunto de datos o en todos los conjuntos de datos. | Id. de conjunto de datos |
| platform.ups.ingest.streaming.request.m1_rate | Tasa de solicitud entrante. | Organización IMS (**obligatoria**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Tasa de éxito de inserción. | Organización IMS (**obligatoria**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Tasa de nuevos registros ingeridos para un conjunto de datos. | Id. de conjunto de datos (**requerido**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Tasa de registros con marca de hora desordenada para crear solicitudes para un conjunto de datos. | Id. de conjunto de datos (**requerido**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Marca de hora para la última solicitud de registro de creación de un conjunto de datos. | Id. de conjunto de datos (**requerido**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Tasa de registros con marca de hora desordenada para la solicitud de actualización de un conjunto de datos. | Id. de conjunto de datos (**requerido**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Marca de hora para la última solicitud de registro de actualización de un conjunto de datos. | Id. de conjunto de datos (**requerido**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Tamaño promedio del registro. | Organización IMS (**obligatoria**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Tasa de solicitudes de actualización para registros ingestados para un conjunto de datos. | Id. de conjunto de datos (**requerido**) |