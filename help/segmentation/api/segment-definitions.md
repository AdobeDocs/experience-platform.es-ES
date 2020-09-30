---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;segment definition;segment definitions;api;API;
solution: Experience Platform
title: Definiciones de segmentos
topic: developer guide
description: Esta guía proporciona información para ayudarle a comprender mejor las definiciones de segmentos e incluye ejemplos de llamadas de API para realizar acciones básicas mediante la API.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 3%

---


# Extremo de definiciones de segmentos

Adobe Experience Platform permite crear segmentos que definen un grupo de atributos o comportamientos específicos a partir de un grupo de perfiles. Una definición de segmento es un objeto que encapsula una consulta escrita en [!DNL Profile Query Language] (PQL). Este objeto también se denomina predicado PQL. Los predicados PQL definen las reglas para el segmento en función de las condiciones relacionadas con cualquier registro o dato de serie temporal que proporcione a [!DNL Real-time Customer Profile]. Consulte la guía [](../pql/overview.md) PQL para obtener más información sobre cómo escribir consultas PQL.

Esta guía proporciona información para ayudarle a comprender mejor las definiciones de segmentos e incluye ejemplos de llamadas de API para realizar acciones básicas mediante la API.

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte la guía [de](./getting-started.md) introducción para obtener información importante que debe conocer a fin de realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de definiciones de segmentos {#list}

Puede recuperar una lista de todas las definiciones de segmentos para su organización de IMS realizando una solicitud de GET al `/segment/definitions` extremo.

**Formato API**

El extremo admite varios parámetros de consulta para ayudar a filtrar los resultados. `/segment/definitions` Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros se recuperarán todas las definiciones de segmentos disponibles para su organización. Se pueden incluir varios parámetros, separados por ampersands (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial para las definiciones de segmento devueltas. | `start=4` |
| `limit` | Especifica el número de definiciones de segmentos devueltas por página. | `limit=20` |
| `page` | Especifica de qué página se inicios los resultados de las definiciones de segmentos. | `page=5` |
| `sort` | Especifica el campo por el que se ordenarán los resultados. Está escrito en el siguiente formato: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Especifica si la definición del segmento está habilitada para flujo continuo. | `evaluationInfo.continuous.enabled=true` |

**Solicitud**

La siguiente solicitud recuperará las dos últimas definiciones de segmentos publicadas en su organización de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de definiciones de segmentos para la organización de IMS especificada como JSON.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Crear una nueva definición de segmento {#create}

Puede crear una nueva definición de segmento haciendo una solicitud de POST al `/segment/definitions` extremo.

**Formato API**

```http
POST /segment/definitions
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | **Requerido.** Un nombre único por el cual hacer referencia al segmento. |
| `schema` | **Requerido.** El esquema asociado a las entidades del segmento. Consiste en un `id` campo o `name` . |
| `expression` | **Requerido.** Entidad que contiene información de campos sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`:: Representación textual de una definición de segmento, según la gramática PQL publicada.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Una expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Una descripción de la definición legible por el usuario. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición de segmento recién creada.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Un ID generado por el sistema de la definición de segmento recién creada. |
| `evaluationInfo` | Objeto generado por el sistema que indica el tipo de evaluación que se someterá a la definición del segmento. Puede ser por lotes, continua (también conocida como flujo continuo) o segmentación sincrónica. |

## Recuperar una definición de segmento específica {#get}

Puede recuperar información detallada sobre una definición de segmento específica realizando una solicitud de GET al extremo y proporcionando el ID de la definición de segmento que desea recuperar en la ruta de solicitud. `/segment/definitions`

**Formato API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | El `id` valor de la definición del segmento que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la definición de segmento especificada.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | ID de solo lectura generada por el sistema de la definición del segmento. |
| `name` | Un nombre único por el cual hacer referencia al segmento. |
| `schema` | El esquema asociado a las entidades del segmento. Consiste en un `id` campo o `name` . |
| `expression` | Entidad que contiene información de campos sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`:: Representación textual de una definición de segmento, según la gramática PQL publicada.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Una expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Una descripción legible de la definición. |
| `evaluationInfo` | Objeto generado por el sistema que indica qué tipo de evaluación, lote, continuo (también conocido como flujo) o sincrónico se someterá a la definición del segmento. |

## Definiciones de segmentos de recuperación masiva {#bulk-get}

Puede recuperar información detallada sobre varias definiciones de segmentos especificadas realizando una solicitud de POST al extremo y proporcionando los `/segment/definitions/bulk-get` valores `id` de las definiciones de segmentos en el cuerpo de la solicitud.

**Formato API**

```http
POST /segment/definitions/bulk-get
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 207 con las definiciones de segmento solicitadas.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | ID de solo lectura generada por el sistema de la definición del segmento. |
| `name` | Un nombre único por el cual hacer referencia al segmento. |
| `schema` | El esquema asociado a las entidades del segmento. Consiste en un `id` campo o `name` . |
| `expression` | Entidad que contiene información de campos sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`:: Representación textual de una definición de segmento, según la gramática PQL publicada.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Una expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Una descripción legible de la definición. |
| `evaluationInfo` | Objeto generado por el sistema que indica qué tipo de evaluación, lote, continuo (también conocido como flujo) o sincrónico se someterá a la definición del segmento. |

## Eliminar una definición de segmento específica {#delete}

Puede solicitar la eliminación de una definición de segmento específica realizando una solicitud de DELETE al extremo y proporcionando el ID de la definición de segmento que desea eliminar en la ruta de la solicitud. `/segment/definitions`

**Formato API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | El `id` valor de la definición del segmento que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 sin mensaje.

## Actualizar una definición de segmento específica

Puede actualizar una definición de segmento específica realizando una solicitud de PATCH al extremo y proporcionando el ID de la definición de segmento que desea actualizar en la ruta de la solicitud. `/segment/definitions`

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | El `id` valor de la definición del segmento que desea actualizar. |

**Solicitud**

La siguiente solicitud actualizará el país de la dirección de trabajo de los Estados Unidos a Canadá.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién actualizada. Observe cómo el país de la dirección de trabajo se ha actualizado de EE.UU. (EE.UU.) a Canadá (CA).

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## Pasos siguientes

Después de leer esta guía, ahora podrá comprender mejor cómo funcionan las definiciones de segmentos. Para obtener más información sobre la creación de un segmento, lea el tutorial sobre la [creación de un segmento](../tutorials/create-a-segment.md) .