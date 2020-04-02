---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definiciones de segmentos
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Guía para desarrolladores de definiciones de segmentos

Adobe Experience Platform permite crear segmentos que definen un grupo de atributos o comportamientos específicos a partir de un grupo de perfiles.

Esta guía para desarrolladores proporciona instrucciones sobre las siguientes áreas para definiciones de segmentos:

- [Recuperar una lista de definiciones de segmentos](#retrieve-a-list-of-segment-definitions)
- [Crear una nueva definición de segmento](#create-a-new-segment-definition)
- [Recuperar una definición de segmento específica](#retrieve-a-specific-segment-definition)
- [Eliminar una definición de segmento específica](#delete-a-specific-segment-definition)
- [Actualizar una definición de segmento específica](#update-a-specific-segment-definition)

## Primeros pasos

Los extremos de API que se utilizan en esta guía forman parte de la API de segmentación. Antes de continuar, consulte la guía para desarrolladores [de Segmentación](./getting-started.md).

En particular, la sección [de](./getting-started.md#getting-started) introducción de la guía para desarrolladores de Segmentación incluye vínculos a temas relacionados, una guía para leer las llamadas de la API de muestra en el documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas exitosas a cualquier API de la plataforma de experiencia.

## Recuperar una lista de definiciones de segmentos

Puede recuperar una lista de todas las definiciones de segmentos para su organización de IMS haciendo una solicitud GET al `/segment/definitions` extremo.

**Formato API**

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:: (*Opcional*) Se han agregado parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por ampersands (`&`). Los parámetros disponibles se enumeran a continuación.

**Parámetros de Consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar las definiciones de segmentos. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros se recuperarán todas las definiciones de segmentos disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `start` | ??? |
| `limit` | Especifica el número de definiciones de segmentos devueltas por página. |
| `page` | Especifica de qué página se inicios los resultados de las definiciones de segmentos. |
| `sort` | Se especificó el campo por el que se ordenarán los resultados. |
| `evaluationInfo.continuous.enabled` | Especifica si la definición del segmento está habilitada para flujo continuo. |

**Solicitud**

```shell
cur -X GET https://platform.adobe.io/data/core/ups/segment/definitions?QUERY \
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
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
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
                "value": "{\"nodeType\":\"select\",\"variables\":[{\"nodeType\":\"varDecl\",\"varName\":\"_Checkouts1\",\"from\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"xEvent\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}},\"where\":{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"eventType\",\"object\":{\"nodeType\":\"varRef\",\"varName\":\"_Checkouts1\"}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"commerce.checkouts\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":true}]}}]}"
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
        ... ,
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"and\",\"params\":[{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"points\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"Double\",\"nodeType\":\"literal\",\"value\":2}]},{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"testLoyaltyID\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":false}]}]}"
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
        "totalCount": 4,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 4,
        "limit": 100
    },
    "link": {}
}
```

## Crear una nueva definición de segmento

Puede crear una nueva definición de segmento haciendo una solicitud POST al `/segment/definitions` extremo.

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
 -d '
 {
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
  "ttlInDays": 60,
  "creationTime": 0,
  "updateTime": 0,
  "updateEpoch": 0
}
 '
```

explicar cuerpo

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

explicar cuerpo y encabezados

## Recuperar una definición de segmento específica

Puede recuperar información detallada sobre una definición de segmento específica realizando una solicitud GET al extremo y proporcionando el valor de la definición del segmento en la ruta de la solicitud `/segment/definitions` y proporcionando el valor `id` de la definición del segmento.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`:: El `id` valor de la definición del segmento que desea recuperar.

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
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
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

## Eliminar una definición de segmento específica

Puede solicitar la eliminación de una definición de segmento especificada realizando una solicitud ELIMINAR al extremo y proporcionando el valor de la definición `/segment/definitions` `id` del segmento en la ruta de la solicitud.

**Formato API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}` El `id` valor de la definición del segmento que desea eliminar.

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

Puede actualizar una definición de segmento especificada realizando una solicitud PATCH al extremo y proporcionando el valor de la definición del `/segment/definitions` segmento en la ruta de acceso `id` de la solicitud.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`:: El `id` valor de la definición del segmento que desea actualizar.

**Solicitud**

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
        "value": "workAddress.country = \"US\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}
'
```

explicar cuerpo

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién actualizada.

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
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

explicar cuerpo y encabezado

## Pasos siguientes
