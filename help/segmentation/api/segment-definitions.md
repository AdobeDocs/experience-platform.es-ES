---
solution: Experience Platform
title: Punto final de API de definiciones de segmento
description: El punto final de las definiciones de segmentos en la API del servicio de segmentación de Adobe Experience Platform le permite administrar mediante programación las definiciones de segmentos de su organización.
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 5f19bd0601770115cae859fd6dc85bd9c9f6e92c
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 3%

---

# Extremo de definiciones de segmento

>[!WARNING]
>
>La creación de audiencias mediante entidades B2B mediante la API del servicio de segmentación está en desuso. Ya no puede crear audiencias con las siguientes entidades B2B: Cuenta, Relación cuenta-persona, Campaña, Miembro de campaña, Lista de marketing, Miembro de lista de marketing, Oportunidad y Relación oportunidad-persona. Para obtener más información, lea la guía sobre [Actualizaciones de la arquitectura de Real-Time CDP B2B edition](../../rtcdp/b2b-architecture-upgrade.md).

Adobe Experience Platform le permite crear definiciones de segmentos que definen un grupo de atributos o comportamientos específicos a partir de un grupo de perfiles. Una definición de segmento es un objeto que encapsula una consulta escrita en [!DNL Profile Query Language] (PQL). Las definiciones de segmentos se aplican a perfiles para crear audiencias. Este objeto (definición de segmento) también se denomina predicado PQL. Los predicados de PQL definen las reglas para la definición del segmento en función de las condiciones relacionadas con cualquier registro o serie temporal que proporcione a [!DNL Real-Time Customer Profile]. Consulte la [guía de PQL](../pql/overview.md) para obtener más información sobre cómo escribir consultas de PQL.

Esta guía proporciona información para ayudarle a comprender mejor las definiciones de segmentos e incluye llamadas de API de ejemplo para realizar acciones básicas mediante la API.

## Introducción

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperación de una lista de definiciones de segmentos {#list}

Puede recuperar una lista de todas las definiciones de segmentos de su organización realizando una petición GET al extremo `/segment/definitions`.

**Formato de API**

El extremo `/segment/definitions` admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Si realiza una llamada a este punto final sin parámetros, recuperará todas las definiciones de segmentos disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

+++ Una lista de parámetros de consulta disponibles.

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial para las definiciones de segmento devueltas. | `start=4` |
| `limit` | Especifica el número de definiciones de segmento devueltas por página. | `limit=20` |
| `page` | Especifica la página desde la que se iniciarán los resultados de las definiciones de segmentos. | `page=5` |
| `sort` | Especifica por qué campo ordenar los resultados. Está escrito en el siguiente formato: `[attributeName]:[desc/asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Especifica si la definición del segmento está habilitada para flujo continuo. | `evaluationInfo.continuous.enabled=true` |

+++

**Solicitud**

La siguiente solicitud recuperará las dos últimas definiciones de segmento publicadas en su organización.

+++ Una solicitud de ejemplo para recuperar una lista de definiciones de segmentos.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de definiciones de segmento para la organización especificada como JSON.

+++ Una respuesta de ejemplo al recuperar una lista de definiciones de segmentos.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

+++

## Crear una nueva definición de segmento {#create}

Puede crear una nueva definición de segmento realizando una petición POST al extremo `/segment/definitions`.

>[!IMPORTANT]
>
>Las definiciones de segmento creadas mediante la API **no se pueden** editar mediante el Generador de segmentos.

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

Al crear una nueva definición de segmento, puede crearla en el formato `pql/text` o `pql/json`.

>[!BEGINTABS]

>[!TAB Usando pql/text]

+++ Una solicitud de ejemplo para crear una definición de segmento.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre único para hacer referencia a la definición del segmento. |
| `description` | (Opcional) Una descripción de la definición del segmento que está creando. |
| `expression` | Una entidad que contiene campos e información sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en el valor. Los valores admitidos son `pql/text` y `pql/json`. |
| `expression.value` | Expresión que se ajusta al tipo indicado en `expression.format`. |
| `evaluationInfo` | (Opcional) El tipo de definición de segmento que está creando. Si desea crear un segmento por lotes, establezca `evaluationInfo.batch.enabled` como verdadero. Si desea crear un segmento de flujo continuo, establezca `evaluationInfo.continuous.enabled` como verdadero. Si desea crear un segmento de Edge, establezca `evaluationInfo.synchronous.enabled` como true. Si se deja vacía, la definición del segmento se creará como un segmento **batch**. |
| `schema` | El esquema asociado a las entidades del segmento. Consta de un campo `id` o `name`. |

+++

>[!TAB Usando pql/json]

+++ Una solicitud de ejemplo para crear una definición de segmento.

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
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string"
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre único para hacer referencia a la definición del segmento. |
| `description` | (Opcional) Una descripción de la definición del segmento que está creando. |
| `evaluationInfo` | (Opcional) El tipo de definición de segmento que está creando. Si desea crear un segmento por lotes, establezca `evaluationInfo.batch.enabled` como verdadero. Si desea crear un segmento de flujo continuo, establezca `evaluationInfo.continuous.enabled` como verdadero. Si desea crear un segmento de Edge, establezca `evaluationInfo.synchronous.enabled` como true. Si se deja vacía, la definición del segmento se creará como un segmento **batch**. |
| `schema` | El esquema asociado a las entidades del segmento. Consta de un campo `id` o `name`. |
| `expression` | Una entidad que contiene campos e información sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en el valor. |
| `expression.value` | Expresión que se ajusta al tipo indicado en `expression.format`. |

+++

>[!ENDTABS]

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién creada.

+++ Una respuesta de ejemplo al crear una definición de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `evaluationInfo` | Un objeto que indica a qué tipo de evaluación se someterá la definición del segmento. Puede ser segmentación por lotes, por secuencias (también conocida como continua) o por perímetros (también conocida como sincrónica). |

+++

## Recuperación de una definición de segmento específica {#get}

Puede recuperar información detallada sobre una definición de segmento específica realizando una petición GET al extremo `/segment/definitions` y proporcionando el ID de la definición de segmento que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | El valor `id` de la definición de segmento que desea recuperar. |

**Solicitud**

+++ Una solicitud de ejemplo para recuperar una definición de segmento.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la definición de segmento especificada.

+++ Una respuesta de ejemplo al recuperar una definición de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `id` | ID de solo lectura generado por el sistema para la definición del segmento. |
| `name` | Un nombre único para hacer referencia a la definición del segmento. |
| `schema` | El esquema asociado a las entidades del segmento. Consta de un campo `id` o `name`. |
| `expression` | Una entidad que contiene campos e información sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en el valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`: una representación textual de una definición de segmento, según la gramática publicada de PQL.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Una descripción de la definición en lenguaje natural. |
| `evaluationInfo` | Objeto que indica a qué tipo de evaluación, lote, flujo (también conocido como continuo) o perímetro (también conocido como sincrónico) se someterá la definición del segmento. |

+++

## Recuperación masiva de definiciones de segmentos {#bulk-get}

Puede recuperar información detallada sobre varias definiciones de segmento especificadas realizando una petición POST al extremo `/segment/definitions/bulk-get` y proporcionando los valores `id` de las definiciones de segmento en el cuerpo de la solicitud.

**Formato de API**

```http
POST /segment/definitions/bulk-get
```

**Solicitud**

+++ Una solicitud de muestra al utilizar el extremo de obtención masiva.

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

| Propiedad | Descripción |
| -------- | ----------- |
| `ids` | Matriz que contiene objetos que indican los ID de las definiciones de segmento que desea recuperar. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 207 con las definiciones de segmento solicitadas.

+++ Una respuesta de muestra al utilizar el extremo de obtención masiva.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
| `id` | ID de solo lectura generado por el sistema para la definición del segmento. |
| `name` | Un nombre único para hacer referencia a la definición del segmento. |
| `schema` | El esquema asociado a las entidades del segmento. Consta de un campo `id` o `name`. |
| `expression` | Una entidad que contiene campos e información sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en el valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`: una representación textual de una definición de segmento, según la gramática publicada de PQL.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Expresión que se ajusta al tipo indicado en `expression.format`. |
| `description` | Una descripción de la definición en lenguaje natural. |
| `evaluationInfo` | Objeto que indica a qué tipo de evaluación, lote, flujo (también conocido como continuo) o perímetro (también conocido como sincrónico) se someterá la definición del segmento. |

+++

## Eliminar una definición de segmento específica {#delete}

Puede solicitar eliminar una definición de segmento específica realizando una petición DELETE al extremo `/segment/definitions` y proporcionando el ID de la definición de segmento que desea eliminar en la ruta de solicitud.

>[!NOTE]
>
> No se puede eliminar una definición de segmento utilizada en una activación de destino **1}.**

**Formato de API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | El valor `id` de la definición de segmento que desea eliminar. |

**Solicitud**

+++ Una solicitud de ejemplo para eliminar una definición de segmento.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 sin mensaje.

## Actualizar una definición de segmento específica

Puede actualizar una definición de segmento específica realizando una petición PATCH al extremo `/segment/definitions` y proporcionando el ID de la definición de segmento que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_ID}` | El valor `id` de la definición de segmento que desea actualizar. |

**Solicitud**

La siguiente solicitud actualizará la dirección de trabajo del país de EE. UU. a Canadá.

>[!NOTE]
>
>Dado que esta llamada de API **reemplaza** el contenido de la definición del segmento, asegúrese de **que todos** los campos que desea conservar se incluyan como parte del cuerpo de la solicitud.

+++ Una solicitud de ejemplo para actualizar una definición de segmento.

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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién actualizada.

+++ Una respuesta de ejemplo al actualizar una definición de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

+++

## Convertir definición del segmento

Puede convertir una definición de segmento entre `pql/text` y `pql/json` o `pql/json` a `pql/text` realizando una petición POST al extremo `/segment/conversion`.

**Formato de API**

```http
POST /segment/conversion
```

**Solicitud**

La siguiente solicitud cambiará el formato de la definición del segmento de `pql/text` a `pql/json`.

+++ Una solicitud de ejemplo para convertir la definición del segmento.

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
        "payloadSchema": "string"
    }'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién convertida.

+++ Una respuesta de ejemplo al convertir la definición del segmento.

```json
{
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

+++

## Próximos pasos

Después de leer esta guía, ahora tiene una mejor comprensión de cómo funcionan las definiciones de segmentos. Para obtener más información sobre cómo crear un segmento, lea el tutorial [crear un segmento](../tutorials/create-a-segment.md).
