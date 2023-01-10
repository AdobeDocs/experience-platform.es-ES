---
keywords: Experience Platform;guía para desarrolladores;punto final;Data Science Workspace;temas populares;perspectivas;api sensei de aprendizaje automático
solution: Experience Platform
title: Punto final de la API de perspectivas
description: Las perspectivas contienen métricas que se utilizan para facultar a un científico de datos para evaluar y elegir modelos ML óptimos mediante la visualización de métricas de evaluación relevantes.
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# Punto final de perspectivas

Las perspectivas contienen métricas que se utilizan para facultar a un científico de datos para evaluar y elegir modelos ML óptimos mediante la visualización de métricas de evaluación relevantes.

## Recuperar una lista de perspectivas

Puede recuperar una lista de perspectivas realizando una única solicitud de GET al extremo de perspectivas.  Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice de [parámetros de consulta para la recuperación de recursos](./appendix.md#query).

**Formato de API**

```http
GET /insights
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye una lista de perspectivas y cada perspectiva tiene un identificador único ( `id` ). Además, recibirá `context` que contiene los identificadores únicos asociados a esa perspectiva en particular, seguidos de los datos de métricas y eventos de Insights.

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID correspondiente a Insight. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |
| `modelId` | Un ID de modelo válido. |

## Recuperar una perspectiva específica

Para buscar una perspectiva en particular, realice una solicitud de GET y proporcione una `{INSIGHT_ID}` en la ruta de solicitud. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice de [parámetros de consulta para la recuperación de recursos](./appendix.md#query).

**Formato de API**

```http
GET /insights/{INSIGHT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{INSIGHT_ID}` | Identificador único de una perspectiva de Sensei. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye el identificador único de perspectivas (`id`). Además, recibirá `context` que contiene los identificadores únicos asociados a la perspectiva en particular que siguen a los eventos de Insights y a los datos de métricas.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID correspondiente a Insight. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |
| `modelId` | Un ID de modelo válido. |

## Añadir una nueva perspectiva de modelo

Puede crear una nueva perspectiva de modelo realizando una solicitud de POST y una carga útil que proporcione contexto, eventos y métricas para la nueva perspectiva de modelo. El campo de contexto utilizado para crear una nueva perspectiva de modelo no es necesario para tener servicios existentes adjuntos, pero puede elegir crear la nueva perspectiva de modelo con servicios existentes proporcionando uno o más de los ID correspondientes:

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
  }
```

**Formato de API**

```http
POST /insights
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**Respuesta**

Una respuesta correcta devolverá una carga útil que tiene una `{INSIGHT_ID}` y cualquier parámetro que haya proporcionado en la solicitud inicial.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Propiedad | Descripción |
| --- | --- |
| `insightId` | ID exclusivo que se crea para esta perspectiva concreta cuando se realiza una solicitud de POST correcta. |

## Recuperar una lista de métricas predeterminadas para algoritmos

Puede recuperar una lista de todas las métricas predeterminadas y del algoritmo realizando una sola solicitud de GET al extremo de la métrica. Para consultar una métrica en particular, realice una solicitud de GET y proporcione una `{ALGORITHM}` en la ruta de solicitud.

**Formato de API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parámetro | Descripción |
| --- | --- |
| `{ALGORITHM}` | Identificador del tipo de algoritmo. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una métrica específica mediante el identificador del algoritmo `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye la variable `algorithm` identificador único y matriz de métricas predeterminadas.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
