---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Observability Insights
topic: overview
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c

---


# Información general sobre la capacidad de observación de la plataforma Adobe Experience

Observability Insights es una API de RESTful que le permite exponer las métricas de observabilidad clave en la plataforma de Adobe Experience. Estas métricas proporcionan perspectivas sobre las estadísticas de uso de la Plataforma, las comprobaciones de estado de los servicios de la Plataforma, las tendencias históricas y los indicadores de rendimiento de diversas funcionalidades de la Plataforma.

Este documento muestra una llamada de ejemplo a la API de perspectivas de la observación. Para obtener una lista completa de los extremos de observación, consulte la referencia [de la API de perspectivas de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)observación.

## Primeros pasos

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación. Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../sandboxes/home.md)entorno limitado.

* x-sandbox-name: `{SANDBOX_NAME}`

## Recuperar métricas de observabilidad

Puede recuperar las métricas de observabilidad realizando una solicitud GET al extremo en la API de perspectivas de `/metrics` observación.

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
| `{ID}` | Identificador de un recurso de plataforma concreto cuyas métricas desea exponer. Esta ID puede ser opcional, obligatoria o no aplicable en función de las métricas utilizadas. Para obtener una lista de las métricas disponibles, así como de los ID admitidos (tanto obligatorios como opcionales) para cada métrica, consulte el documento de referencia de las métricas [](metrics.md)disponibles. |
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

Una respuesta correcta devuelve una lista de objetos, cada uno de los cuales contiene una marca de tiempo dentro de los valores proporcionados `dateRange` y correspondientes para las métricas especificadas en la ruta de la solicitud. Si el `id` de un recurso de plataforma se incluye en la ruta de solicitud, los resultados se aplicarán solamente a ese recurso en particular. Si `id` se omite, los resultados se aplicarán a todos los recursos aplicables dentro de la organización de IMS.

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

## Pasos siguientes

Este documento proporcionó una visión general de la API de perspectivas de la observabilidad. Consulte el documento de las métricas [](metrics.md) disponibles para obtener una lista completa de las métricas que se pueden usar en la API.