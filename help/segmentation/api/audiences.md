---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;audiencias;audiencia;API;api;
title: Extremo de API de audiencias
description: El extremo de audiencias de la API del servicio de segmentación de Adobe Experience Platform le permite administrar audiencias de su organización mediante programación.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 5%

---

# Extremo de audiencias

>[!IMPORTANT]
>
>El extremo de audiencia está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Una audiencia es un conjunto de personas que comparten comportamientos o características similares. Estas colecciones de personas se pueden generar mediante Adobe Experience Platform o desde fuentes externas. Puede usar el complemento `/audiences` en la API de segmentación, lo que le permite recuperar, crear, actualizar y eliminar audiencias mediante programación.

## Primeros pasos

Los extremos utilizados en esta guía forman parte del [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API de, incluidos los encabezados obligatorios y cómo leer llamadas de API de ejemplo.

## Recuperación de una lista de audiencias {#list}

Puede recuperar una lista de todas las audiencias de su organización realizando una solicitud de GET a `/audiences` punto final.

**Formato de API**

El `/audiences` el punto de conexión admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir la costosa sobrecarga al enumerar recursos. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las audiencias disponibles para su organización. Se pueden incluir varios parámetros separados por el símbolo et (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Al recuperar una lista de audiencias, se pueden utilizar los siguientes parámetros de consulta:

| Parámetro de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial de las audiencias devueltas. | `start=5` |
| `limit` | Especifica el número máximo de audiencias devueltas por página. | `limit=10` |
| `sort` | Especifica el orden por el que se ordenan los resultados. Esto se escribe con el formato `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Un filtro que le permite especificar audiencias que **exacto** coincide con el valor de un atributo. Esto se escribe con el formato `property=` | `property=audienceId==test-audience-id` |
| `name` | Un filtro que le permite especificar audiencias cuyos nombres **contain** el valor proporcionado. Este valor no distingue entre mayúsculas y minúsculas. | `name=Sample` |
| `description` | Un filtro que le permite especificar audiencias cuyas descripciones **contain** el valor proporcionado. Este valor no distingue entre mayúsculas y minúsculas. | `description=Test Description` |
| `withMetrics` | Filtro que devuelve las métricas además de las audiencias. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>Para las audiencias, las métricas se devuelven en la variable `metrics` y contiene información sobre los recuentos de perfiles, la creación y la actualización de marcas de tiempo.

**Sin métricas**

El siguiente par de solicitud/respuesta se utiliza cuando la variable `withMetrics` el parámetro de consulta no está presente.

**Solicitud**

La siguiente solicitud recupera las últimas cinco audiencias creadas en su organización.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**Respuesta** {#no-metrics}

Una respuesta correcta devuelve el estado HTTP 200 con una lista de audiencias creadas en su organización como JSON.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y muestra solo la primera audiencia devuelta.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| Propiedad | Tipo de audiencia | Descripción |
| -------- | ------------- | ----------- | 
| `id` | Ambas | Un identificador de solo lectura generado por el sistema para la audiencia. |
| `audienceId` | Ambas | Si la audiencia es una audiencia generada por Platform, este es el mismo valor que la `id`. Si la audiencia se genera externamente, el cliente proporciona este valor. |
| `schema` | Ambas | El esquema Experience Data Model (XDM) de la audiencia. |
| `imsOrgId` | Ambas | El ID de la organización a la que pertenece la audiencia. |
| `sandbox` | Ambas | Información sobre la zona protegida a la que pertenece la audiencia. Encontrará más información sobre las zonas protegidas en la [información general sobre zonas protegidas](../../sandboxes/home.md). |
| `name` | Ambas | El nombre de la audiencia. |
| `description` | Ambas | Una descripción de la audiencia. |
| `expression` | Generado por Platform | La expresión de lenguaje de consulta de perfil (PQL) de la audiencia. Puede encontrar más información sobre las expresiones PQL en la [Guía de expresiones PQL](../pql/overview.md). |
| `mergePolicyId` | Generado por Platform | El ID de la política de combinación a la que está asociada la audiencia. Encontrará más información sobre las políticas de combinación en la [guía de políticas de combinación](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Generado por Platform | Muestra cómo se evaluará la audiencia. Los posibles métodos de evaluación incluyen batch, streaming o edge. Encontrará más información sobre los métodos de evaluación en la [resumen de segmentación](../home.md) |
| `dependents` | Ambas | Una matriz de ID de audiencia que dependen de la audiencia actual. Se utilizaría si va a crear una audiencia que sea un segmento de un segmento. |
| `dependencies` | Ambas | Una matriz de ID de audiencia de los que depende la audiencia. Se utilizaría si va a crear una audiencia que sea un segmento de un segmento. |
| `type` | Ambas | Campo generado por el sistema que muestra si la audiencia es generada por Platform o por un público generado externamente. Los valores posibles incluyen `SegmentDefinition` y `ExternalAudience`. A `SegmentDefinition` hace referencia a una audiencia generada en Platform, mientras que un `ExternalAudience` hace referencia a una audiencia que no se generó en Platform. |
| `createdBy` | Ambas | El ID del usuario que creó la audiencia. |
| `labels` | Ambas | Etiquetas de uso de datos a nivel de objeto y de control de acceso basadas en atributos que son relevantes para la audiencia. |
| `namespace` | Ambas | El área de nombres al que pertenece la audiencia. Los valores posibles incluyen `AAM`, `AAMSegments`, `AAMTraits`, y `AEPSegments`. |
| `audienceMeta` | Externo | Metadatos creados externamente desde la audiencia creada externamente. |

**Con métricas**

El siguiente par de solicitud/respuesta se utiliza cuando la variable `withMetrics` el parámetro de consulta está presente.

**Solicitud**

La siguiente solicitud recupera las últimas cinco audiencias, con métricas, creadas en su organización.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de audiencias, con métricas, para la organización especificada como JSON.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y muestra solo la primera audiencia devuelta.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

A continuación se enumeran las propiedades **exclusivo** a la `withMetrics` respuesta. Si desea conocer las propiedades de audiencia estándar, lea la [sección anterior](#no-metrics).

| Propiedad | Descripción |
| -------- | ----------- |
| `metrics.imsOrgId` | El ID de organización de la audiencia. |
| `metrics.sandbox` | La información de la zona protegida relacionada con la audiencia. |
| `metrics.jobId` | El ID del trabajo del segmento que está procesando la audiencia. |
| `metrics.type` | El tipo de trabajo del segmento. Esto puede ser `export` o `batch_segmentation`. |
| `metrics.id` | El ID de la audiencia. |
| `metrics.data` | Métricas relacionadas con la audiencia. Esto incluye información como el número total de perfiles incluidos en la audiencia, el número total de perfiles por área de nombres y el número total de perfiles por estado. |
| `metrics.createEpoch` | Una marca de tiempo que indica cuándo se creó la audiencia. |
| `metrics.updateEpoch` | Una marca de tiempo que indica cuándo se actualizó la audiencia por última vez. |

## Crear una audiencia nueva {#create}

Puede crear una audiencia nueva realizando una solicitud de POST a `/audiences` punto final.

**Formato de API**

```http
POST /audiences
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
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
| `name` | El nombre de la audiencia. |
| `description` | Una descripción de la audiencia. |
| `type` | Campo que muestra si la audiencia es una audiencia generada por Platform o por un generador externo. Los valores posibles incluyen `SegmentDefinition` y `ExternalAudience`. A `SegmentDefinition` hace referencia a una audiencia generada en Platform, mientras que un `ExternalAudience` hace referencia a una audiencia que no se generó en Platform. |
| `expression` | La expresión de lenguaje de consulta de perfil (PQL) de la audiencia. Puede encontrar más información sobre las expresiones PQL en la [Guía de expresiones PQL](../pql/overview.md). |
| `schema` | El esquema Experience Data Model (XDM) de la audiencia. |
| `labels` | Etiquetas de uso de datos a nivel de objeto y de control de acceso basadas en atributos que son relevantes para la audiencia. |

**Respuesta**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Búsqueda de una audiencia especificada {#get}

Puede buscar información detallada sobre una audiencia específica realizando una solicitud de GET a la `/audiences` y proporciona el ID de la audiencia que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Parámetro | Descripción |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | El ID de la audiencia que intenta recuperar. |
| `property=withmetrics==true` | Un parámetro de consulta opcional que puede utilizar si desea recuperar una audiencia especificada con las métricas de audiencia. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la audiencia especificada. La respuesta variará según si la audiencia se genera con Adobe Experience Platform o fuentes externas.

**Generado por Platform**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**Generado externamente**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Actualización de un campo en una audiencia {#update-field}

Puede actualizar los campos de una audiencia específica realizando una solicitud al PATCH de la `/audiences` y proporciona el ID de la audiencia que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{AUDIENCE_ID}` | El ID de la audiencia que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `op` | Para actualizar audiencias, este valor siempre es `add`. |
| `path` | La ruta del campo que desea actualizar. |
| `value` | El valor al que desea actualizar el campo. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la audiencia recién actualizada.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
        "value": "workAddress.country = \"CA\""
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
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Actualización de una audiencia {#put}

Puede actualizar (sobrescribir) una audiencia específica realizando una solicitud de PUT a `/audiences` y proporciona el ID de la audiencia que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PUT /audiences/{AUDIENCE_ID}
```

**Solicitud**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `audienceId` | El ID de la audiencia. Las audiencias externas lo utilizan |
| `name` | El nombre de la audiencia. |
| `namespace` |  |
| `description` | Una descripción de la audiencia. |
| `type` | Campo generado por el sistema que muestra si la audiencia es generada por Platform o por un público generado externamente. Los valores posibles incluyen `SegmentDefinition` y `ExternalAudience`. A `SegmentDefinition` hace referencia a una audiencia generada en Platform, mientras que un `ExternalAudience` hace referencia a una audiencia que no se generó en Platform. |
| `lifecycle` | El estado de la audiencia. Los valores posibles incluyen `draft`, `published`, `inactive`, y `archived`. `draft` representa cuándo se crea la audiencia, `published` cuando se publique la audiencia, `inactive` cuando la audiencia ya no está activa, y `archived` si se elimina la audiencia. |
| `datasetId` | El ID del conjunto de datos en el que se pueden encontrar los datos de audiencia. |
| `labels` | Etiquetas de uso de datos a nivel de objeto y de control de acceso basadas en atributos que son relevantes para la audiencia. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la audiencia recién actualizada. Tenga en cuenta que los detalles de la audiencia variarán según se trate de una audiencia generada por Platform o por un público generado externamente.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Eliminar una audiencia {#delete}

Puede eliminar una audiencia específica realizando una solicitud de DELETE a `/audiences` y proporciona el ID de la audiencia que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{AUDIENCE_ID}` | El ID de la audiencia que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 sin mensaje.
