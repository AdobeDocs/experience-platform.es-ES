---
keywords: Experience Platform;guía para desarrolladores;punto final;Área de trabajo de ciencias de datos;temas populares;perspectivas;API de aprendizaje del equipo sensei
solution: Experience Platform
title: Punto final de la API de perspectivas
topic: Developer guide
description: Las perspectivas contienen métricas que se utilizan para facultar a un científico de datos para evaluar y elegir modelos ML óptimos mediante la visualización de métricas de evaluación relevantes.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---


# Extremo de perspectivas

Las perspectivas contienen métricas que se utilizan para facultar a un científico de datos para evaluar y elegir modelos ML óptimos mediante la visualización de métricas de evaluación relevantes.

## Recuperar una lista de perspectivas

Puede recuperar una lista de perspectivas realizando una sola solicitud de GET al extremo de perspectivas.  Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [parámetros de consulta para la recuperación de activos](./appendix.md#query).

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye una lista de perspectivas y cada perspectiva tiene un identificador único ( `id` ). Además, recibirá `context`, que contiene los identificadores únicos asociados con esa perspectiva en particular después de los datos de métricas y eventos de perspectivas.

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
| `id` | ID correspondiente a la perspectiva. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |
| `modelId` | Un ID de modelo válido. |

## Recuperar una perspectiva específica

Para buscar una perspectiva en particular, realice una solicitud de GET y proporcione un `{INSIGHT_ID}` válido en la ruta de solicitud. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre [parámetros de consulta para la recuperación de activos](./appendix.md#query).

**Formato de API**

```http
GET /insights/{INSIGHT_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{INSIGHT_ID}` | Identificador único de una perspectiva Sensei. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye el identificador único de perspectivas (`id`). Además, recibirá `context`, que contiene los identificadores únicos asociados con la perspectiva particular que sigue a los datos de métricas y eventos de perspectivas.

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
| `id` | ID correspondiente a la perspectiva. |
| `experimentId` | Un ID de experimento válido. |
| `experimentRunId` | Un ID de ejecución de experimento válido. |
| `modelId` | Un ID de modelo válido. |

## Añadir una nueva perspectiva de modelo

Puede crear una nueva perspectiva de modelo realizando una solicitud de POST y una carga útil que proporcione contexto, eventos y métricas para la nueva perspectiva de modelo. El campo de contexto utilizado para crear una nueva perspectiva del modelo no es necesario para tener servicios existentes adjuntos, pero puede elegir crear la nueva perspectiva del modelo con los servicios existentes proporcionando uno o varios de los ID correspondientes:

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una respuesta correcta devolverá una carga útil que tenga un `{INSIGHT_ID}` y cualquier parámetro que haya proporcionado en la solicitud inicial.

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
| `insightId` | ID única que se crea para esta perspectiva en particular cuando se realiza una solicitud de POST correcta. |

## Recuperar una lista de métricas predeterminadas para algoritmos

Puede recuperar una lista de todas las métricas predeterminadas y del algoritmo realizando una sola solicitud de GET al extremo de la métrica. Para consulta de una métrica en particular, realice una solicitud de GET y proporcione un `{ALGORITHM}` válido en la ruta de la solicitud.

**Formato de API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parámetro | Descripción |
| --- | --- |
| `{ALGORITHM}` | Identificador del tipo de algoritmo. |

**Solicitud**

La siguiente solicitud contiene una consulta y recupera una métrica específica mediante el identificador de algoritmo `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye el identificador único `algorithm` y una matriz de métricas predeterminadas.

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
