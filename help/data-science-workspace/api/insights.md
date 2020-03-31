---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Perspectivas
topic: Developer guide
translation-type: tm+mt
source-git-commit: 71e257c85790a96b5017dea314b757ec4ee07bed

---


# Perspectivas

Las perspectivas contienen métricas que se utilizan para facultar a un científico de datos para evaluar y elegir modelos ML óptimos mediante la visualización de métricas de evaluación relevantes.

## Recuperar una lista de perspectivas

Puede recuperar una lista de perspectivas realizando una sola solicitud GET al extremo de perspectivas.  Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de la solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](appendix.md#query)de recursos.

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

Una respuesta correcta devuelve una carga útil que incluye una lista de perspectivas y cada perspectiva tiene un identificador único ( `id` ). Además, recibirá `context` que contiene los identificadores únicos asociados con esa perspectiva en particular después de los datos de métricas y eventos de perspectivas.

```json
{
    "children": [
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
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
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
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

Para buscar una perspectiva en particular, realice una solicitud GET y proporcione un valor válido `{INSIGHT_ID}` en la ruta de solicitud. Para ayudar a filtrar los resultados, puede especificar parámetros de consulta en la ruta de la solicitud. Para obtener una lista de las consultas disponibles, consulte la sección del apéndice sobre los parámetros de [consulta para la recuperación](appendix.md#query)de recursos.

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
  https://platform.adobe.io/data/sensei/insights/{INSIGHT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye el identificador único de perspectivas (`id`). Además, recibirá `context` los identificadores únicos asociados con la perspectiva particular que sigue a los datos de métricas y eventos de perspectivas.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
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

Puede crear una nueva perspectiva de modelo realizando una solicitud POST y una carga útil que proporcione contexto, eventos y métricas para la nueva perspectiva de modelo. El campo de contexto utilizado para crear una nueva perspectiva del modelo no es necesario para tener servicios existentes adjuntos, pero puede elegir crear la nueva perspectiva del modelo con los servicios existentes proporcionando uno o varios de los ID correspondientes:

```json
"context": {
    "clientId": "{CLIENT_ID}",
    "notebookId": "{NOTEBOOK_ID}",
    "experimentId": "{EXPERIMENT_ID}",
    "engineId": "{ENGINE_ID}",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "modelId": "{MODEL_ID}",
    "dataSetId": "{DATASET_ID}"
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
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
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

Una respuesta correcta devolverá una carga útil que tenga un `{INSIGHT_ID}` y todos los parámetros proporcionados en la solicitud inicial.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
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
| `insightId` | ID única que se crea para esta perspectiva en particular cuando se realiza una solicitud POST correcta. |

## Recuperar una lista de métricas predeterminadas para algoritmos

Puede recuperar una lista de todas las métricas predeterminadas y del algoritmo realizando una sola solicitud GET al extremo de las métricas. Para consulta de una métrica en particular, realice una solicitud GET y proporcione un valor válido `{ALGORITHM}` en la ruta de solicitud.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una carga útil que incluye el identificador único y una matriz de métricas predeterminadas. `algorithm`

```json
{
    "children": [
        {
            "algorithm": "{ALGORITHM}",
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
