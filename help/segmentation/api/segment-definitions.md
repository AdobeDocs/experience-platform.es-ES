---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;definición de segmento;definiciones de segmento;api;API;
solution: Experience Platform
title: Punto final de la API de definiciones de segmentos
topic-legacy: developer guide
description: El extremo de definiciones de segmentos en la API del servicio de segmentación de Adobe Experience Platform le permite administrar mediante programación definiciones de segmentos para su organización.
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 5%

---

# Punto final de definiciones de segmentos

Adobe Experience Platform le permite crear segmentos que definen un grupo de atributos o comportamientos específicos de un grupo de perfiles. Una definición de segmento es un objeto que encapsula una consulta escrita en [!DNL Profile Query Language] (PQL). Este objeto también se denomina predicado PQL. Los predicados de PQL definen las reglas para el segmento en función de las condiciones relacionadas con cualquier registro o serie temporal que proporcione a [!DNL Real-time Customer Profile]. Consulte la [Guía de PQL](../pql/overview.md) para obtener más información sobre cómo escribir consultas PQL.

Esta guía proporciona información que le ayudará a comprender mejor las definiciones de segmentos e incluye ejemplos de llamadas API para realizar acciones básicas mediante la API.

## Primeros pasos

Los extremos utilizados en esta guía forman parte del [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar correctamente llamadas a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de definiciones de segmentos {#list}

Puede recuperar una lista de todas las definiciones de segmentos para su organización IMS realizando una solicitud de GET al `/segment/definitions` punto final.

**Formato de API**

La variable `/segment/definitions` el extremo admite varios parámetros de consulta para ayudar a filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las definiciones de segmento disponibles para su organización. Se pueden incluir varios parámetros separados por el símbolo &quot;et&quot; (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial para las definiciones de segmento devueltas. | `start=4` |
| `limit` | Especifica el número de definiciones de segmento devueltas por página. | `limit=20` |
| `page` | Especifica de qué página comenzarán los resultados de las definiciones de segmentos. | `page=5` |
| `sort` | Especifica por qué campo ordenar los resultados. Está escrito en el siguiente formato: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Especifica si la definición del segmento está habilitada para flujo continuo. | `evaluationInfo.continuous.enabled=true` |

**Solicitud**

La siguiente solicitud recuperará las dos últimas definiciones de segmento publicadas en su organización de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de definiciones de segmento para la organización IMS especificada como JSON.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

Puede crear una nueva definición de segmento realizando una solicitud de POST al `/segment/definitions` punto final.

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schema` | **Requerido.** El esquema asociado a las entidades del segmento. Consiste en una `id` o `name` campo . |
| `expression` | **Requerido.** Una entidad que contiene información de campos sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`: Representación textual de una definición de segmento, según la gramática PQL publicada.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Una descripción de la definición legible en lenguaje natural. |

>[!NOTE]
>
>Una expresión de definición de segmento también puede hacer referencia a un atributo calculado. Para obtener más información, consulte la [guía de extremo de API de atributo calculado](../../profile/computed-attributes/ca-api.md)
>
>La funcionalidad de atributo calculada está en alfa y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién creada.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Un ID generado por el sistema de la definición del segmento recién creada. |
| `evaluationInfo` | Un objeto generado por el sistema que indica qué tipo de evaluación se realizará en la definición del segmento. Puede ser por lotes, continua (también conocida como flujo continuo) o de segmentación sincrónica. |

## Recuperar una definición de segmento específica {#get}

Puede recuperar información detallada sobre una definición de segmento específica realizando una solicitud de GET al `/segment/definitions` y proporcionando el ID de la definición de segmento que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | La variable `id` de la definición del segmento que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrgId": "{ORG_ID}",
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
| `id` | Un ID de solo lectura generado por el sistema de la definición del segmento. |
| `name` | Un nombre único por el cual hacer referencia al segmento. |
| `schema` | El esquema asociado a las entidades del segmento. Consiste en una `id` o `name` campo . |
| `expression` | Una entidad que contiene información de campos sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`: Representación textual de una definición de segmento, según la gramática PQL publicada.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Descripción legible de la definición. |
| `evaluationInfo` | Objeto generado por el sistema que indica qué tipo de evaluación, lote, continuo (también conocido como flujo continuo) o sincrónico se someterá a la definición del segmento. |

## Definiciones de segmentos de recuperación masiva {#bulk-get}

Puede recuperar información detallada sobre varias definiciones de segmento especificadas realizando una solicitud de POST al `/segment/definitions/bulk-get` y proporcionando la variable `id` valores de las definiciones de segmentos en el cuerpo de la solicitud.

**Formato de API**

```http
POST /segment/definitions/bulk-get
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
| `id` | Un ID de solo lectura generado por el sistema de la definición del segmento. |
| `name` | Un nombre único por el cual hacer referencia al segmento. |
| `schema` | El esquema asociado a las entidades del segmento. Consiste en una `id` o `name` campo . |
| `expression` | Una entidad que contiene información de campos sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`: Representación textual de una definición de segmento, según la gramática PQL publicada.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Descripción legible de la definición. |
| `evaluationInfo` | Objeto generado por el sistema que indica qué tipo de evaluación, lote, continuo (también conocido como flujo continuo) o sincrónico se someterá a la definición del segmento. |

## Eliminar una definición de segmento específica {#delete}

Puede solicitar la eliminación de una definición de segmento específica realizando una solicitud de DELETE al `/segment/definitions` y proporcione el ID de la definición de segmento que desea eliminar en la ruta de solicitud.

>[!NOTE]
>
> Usted **not** puede eliminar un segmento que se utilice en una activación de destino.

**Formato de API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | La variable `id` de la definición del segmento que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 sin mensaje.

## Actualizar una definición de segmento específica

Puede actualizar una definición de segmento específica realizando una solicitud de PATCH al `/segment/definitions` y proporcione el ID de la definición del segmento que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | La variable `id` de la definición del segmento que desea actualizar. |

**Solicitud**

La siguiente solicitud actualizará el país de dirección de trabajo de los Estados Unidos a Canadá.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición de segmento recién actualizada. Observe cómo el país de la dirección de trabajo se ha actualizado de EE. UU. (EE. UU.) a Canadá (CA).

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

## Convertir definición de segmento

Puede convertir una definición de segmento entre `pql/text` y `pql/json` o `pql/json` a `pql/text` realizando una solicitud de POST al `/segment/conversion` punto final.

**Formato de API**

```http
POST /segment/conversion
```

**Solicitud**

La siguiente solicitud cambiará el formato de la definición del segmento de `pql/text` a `pql/json`.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién convertido.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Pasos siguientes

Después de leer esta guía, ahora puede comprender mejor cómo funcionan las definiciones de segmentos. Para obtener más información sobre la creación de segmentos, lea la [creación de segmentos](../tutorials/create-a-segment.md) tutorial.
