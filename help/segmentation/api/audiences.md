---
title: Extremo de API de audiencias
description: Utilice el extremo de audiencias en la API del servicio de segmentación de Adobe Experience Platform para crear, administrar y actualizar audiencias de su organización mediante programación.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 9c50ca0db55ce4b21978273d7b4d1de9b5f9338d
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 3%

---

# Extremo de audiencias

Una audiencia es un conjunto de personas que comparten comportamientos o características similares. Estas colecciones de personas se pueden generar mediante Adobe Experience Platform o desde fuentes externas. Puede usar el extremo `/audiences` en la API de segmentación, que le permite recuperar, crear, actualizar y eliminar audiencias mediante programación.

## Introducción

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperación de una lista de audiencias {#list}

Puede recuperar una lista de todas las audiencias de su organización realizando una solicitud de GET al extremo `/audiences`.

**Formato de API**

El extremo `/audiences` admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir la costosa sobrecarga al enumerar recursos. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las audiencias disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

>[!NOTE]
>
>Si usa este extremo sin parámetros de consulta, se devolverán las audiencias inactivas **no**. Sin embargo, si usa este extremo junto con el parámetro de consulta `property=audienceId`, se devolverán las audiencias inactivas **will**.

Al recuperar una lista de audiencias, se pueden utilizar los siguientes parámetros de consulta:

| Parámetro de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial de las audiencias devueltas. | `start=5` |
| `limit` | Especifica el número máximo de audiencias devueltas por página. | `limit=10` |
| `sort` | Especifica el orden por el que se ordenan los resultados. Esto se escribe con el formato `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Filtro que le permite especificar audiencias que **exactamente** coinciden con el valor de un atributo. Esto se escribe con el formato `property=` | `property=audienceId==test-audience-id` |
| `name` | Filtro que le permite especificar audiencias cuyos nombres **contienen** el valor proporcionado. Este valor no distingue entre mayúsculas y minúsculas. | `name=Sample` |
| `description` | Filtro que le permite especificar audiencias cuyas descripciones **contienen** el valor proporcionado. Este valor no distingue entre mayúsculas y minúsculas. | `description=Test Description` |

**Solicitud**

La siguiente solicitud recupera las dos últimas audiencias creadas en su organización.

+++Solicitud de ejemplo para recuperar una lista de audiencias.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de audiencias creadas en su organización como JSON.

+++Una respuesta de ejemplo que contiene las dos últimas audiencias creadas que pertenecen a su organización

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
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
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "pageSize": 2,
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| Propiedad | Tipo de público | Descripción |
| -------- | ------------- | ----------- | 
| `id` | Ambos | Un identificador de solo lectura generado por el sistema para la audiencia. |
| `audienceId` | Ambos | Si la audiencia es una audiencia generada por Platform, este es el mismo valor que `id`. Si la audiencia se genera externamente, el cliente proporciona este valor. |
| `schema` | Ambos | El esquema Experience Data Model (XDM) de la audiencia. |
| `imsOrgId` | Ambos | El ID de la organización a la que pertenece la audiencia. |
| `sandbox` | Ambos | Información sobre la zona protegida a la que pertenece la audiencia. Encontrará más información sobre las zonas protegidas en la [descripción general de las zonas protegidas](../../sandboxes/home.md). |
| `name` | Ambos | Nombre de la audiencia. |
| `description` | Ambos | Una descripción de la audiencia. |
| `expression` | Generado por Platform | La expresión Profile Query Language (PQL) de la audiencia. Encontrará más información sobre las expresiones PQL en la [guía de expresiones PQL](../pql/overview.md). |
| `mergePolicyId` | Generado por Platform | El ID de la política de combinación a la que está asociada la audiencia. Encontrará más información sobre las políticas de combinación en la [guía de políticas de combinación](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Generado por Platform | Muestra cómo se evaluará la audiencia. Los posibles métodos de evaluación incluyen por lotes, sincrónico (streaming) o continuo (edge). Encontrará más información sobre los métodos de evaluación en la [descripción general de la segmentación](../home.md) |
| `dependents` | Ambos | Una matriz de ID de audiencia que dependen de la audiencia actual. Se utilizaría si va a crear una audiencia que sea un segmento de un segmento. |
| `dependencies` | Ambos | Una matriz de ID de audiencia de los que depende la audiencia. Se utilizaría si va a crear una audiencia que sea un segmento de un segmento. |
| `type` | Ambos | Campo generado por el sistema que muestra si la audiencia es generada por Platform o por un público generado externamente. Los valores posibles incluyen `SegmentDefinition` y `ExternalSegment`. Un `SegmentDefinition` hace referencia a una audiencia que se generó en Platform, mientras que un `ExternalSegment` hace referencia a una audiencia que no se generó en Platform. |
| `originName` | Ambos | Campo que hace referencia al nombre del origen de la audiencia. Para audiencias generadas por Platform, este valor será `REAL_TIME_CUSTOMER_PROFILE`. Para las audiencias generadas en Audience Orchestration, este valor será `AUDIENCE_ORCHESTRATION`. Para las audiencias generadas en Adobe Audience Manager, este valor será `AUDIENCE_MANAGER`. Para otras audiencias generadas externamente, este valor será `CUSTOM_UPLOAD`. |
| `createdBy` | Ambos | El ID del usuario que creó la audiencia. |
| `labels` | Ambos | Etiquetas de uso de datos a nivel de objeto y de control de acceso basadas en atributos que son relevantes para la audiencia. |
| `namespace` | Ambos | El área de nombres al que pertenece la audiencia. Los valores posibles incluyen `AAM`, `AAMSegments`, `AAMTraits` y `AEPSegments`. |
| `linkedAudienceRef` | Ambos | Un objeto que contiene identificadores de otros sistemas relacionados con la audiencia. |

+++

## Crear una audiencia nueva {#create}

Puede crear una audiencia nueva realizando una solicitud de POST al extremo `/audiences`.

**Formato de API**

```http
POST /audiences
```

**Solicitud**

+++ Una solicitud de ejemplo para crear una audiencia generada por Platform

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "AEPSegments",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `name` | Nombre de la audiencia. |
| `description` | Una descripción de la audiencia. |
| `type` | Campo que muestra si la audiencia es una audiencia generada por Platform o por un generador externo. Los valores posibles incluyen `SegmentDefinition` y `ExternalSegment`. Un `SegmentDefinition` hace referencia a una audiencia que se generó en Platform, mientras que un `ExternalSegment` hace referencia a una audiencia que no se generó en Platform. |
| `expression` | La expresión Profile Query Language (PQL) de la audiencia. Encontrará más información sobre las expresiones PQL en la [guía de expresiones PQL](../pql/overview.md). |
| `schema` | El esquema Experience Data Model (XDM) de la audiencia. |
| `labels` | Etiquetas de uso de datos a nivel de objeto y de control de acceso basadas en atributos que son relevantes para la audiencia. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la audiencia recién creada.

+++Una respuesta de ejemplo al crear una audiencia generada por Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Búsqueda de una audiencia especificada {#get}

Puede buscar información detallada sobre una audiencia específica realizando una solicitud de GET al extremo `/audiences` y proporcionando el ID de la audiencia que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | El ID de la audiencia que intenta recuperar. Tenga en cuenta que este es el campo `id` y es **no** el campo `audienceId`. |

**Solicitud**

+++Una solicitud de ejemplo para recuperar una audiencia.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la audiencia especificada.

+++Respuesta de ejemplo al recuperar una audiencia generada por Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Actualización de una audiencia {#put}

Puede actualizar (sobrescribir) una audiencia específica realizando una solicitud de PUT al extremo `/audiences` y proporcionando el ID de la audiencia que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{AUDIENCE_ID}` | El ID de la audiencia que desea actualizar. Tenga en cuenta que este es el campo `id` y es **no** el campo `audienceId`. |

**Solicitud**

+++Una solicitud de ejemplo para actualizar una audiencia completa.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-platform-audience-id",
    "name": "New Platform audience",
    "namespace": "AEPSegments",
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `audienceId` | El ID de la audiencia. Para audiencias generadas externamente, este valor lo puede proporcionar el usuario. |
| `name` | Nombre de la audiencia. |
| `namespace` | El área de nombres de la audiencia. |
| `description` | Una descripción de la audiencia. |
| `type` | Campo generado por el sistema que muestra si la audiencia es generada por Platform o por un público generado externamente. Los valores posibles incluyen `SegmentDefinition` y `ExternalSegment`. Un `SegmentDefinition` hace referencia a una audiencia que se generó en Platform, mientras que un `ExternalSegment` hace referencia a una audiencia que no se generó en Platform. |
| `lifecycleState` | El estado de la audiencia. Los valores posibles incluyen `draft`, `published` y `inactive`. `draft` representa cuándo se creó la audiencia, `published` cuándo se publicó la audiencia y `inactive` cuándo la audiencia ya no está activa. |
| `datasetId` | El ID del conjunto de datos en el que se pueden encontrar los datos de audiencia. |
| `labels` | Etiquetas de uso de datos a nivel de objeto y de control de acceso basadas en atributos que son relevantes para la audiencia. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la audiencia recién actualizada. Tenga en cuenta que los detalles de la audiencia variarán según se trate de una audiencia generada por Platform o por un público generado externamente.

+++Una respuesta de ejemplo al actualizar una audiencia completa.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-platform-audience-id",
    "name": "New Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Eliminar una audiencia {#delete}

Puede eliminar una audiencia específica realizando una solicitud de DELETE al extremo `/audiences` y proporcionando el ID de la audiencia que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{AUDIENCE_ID}` | El ID de la audiencia que desea eliminar. Tenga en cuenta que este es el campo `id` y es **no** el campo `audienceId`. |

**Solicitud**

+++ Una solicitud de ejemplo para eliminar una audiencia.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 sin mensaje.

## Recuperar varias audiencias {#bulk-get}

Puede recuperar varias audiencias realizando una solicitud de POST al extremo `/audiences/bulk-get` y proporcionando los ID de las audiencias que desea recuperar.

**Formato de API**

```http
POST /audiences/bulk-get
```

**Solicitud**

+++ Una solicitud de ejemplo para recuperar varias audiencias.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 207 con información sobre las audiencias solicitadas.

+++ Una respuesta de ejemplo al recuperar varias audiencias.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## Pasos siguientes

Después de leer esta guía, ahora comprende mejor cómo crear, administrar y eliminar audiencias mediante la API de Adobe Experience Platform. Para obtener más información acerca de la administración de audiencias mediante la interfaz de usuario, lea la [guía de segmentación de la interfaz de usuario](../ui/overview.md).
