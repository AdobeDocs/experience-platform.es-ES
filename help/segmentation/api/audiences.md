---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;audiencias;audiencia;API;api;
title: Punto final de la API de audiencias
description: El punto final de audiencias en la API del servicio de segmentación de Adobe Experience Platform le permite administrar audiencias mediante programación para su organización.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 5%

---

# Punto final de audiencia

>[!IMPORTANT]
>
>El extremo de audiencia está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Una audiencia es una colección de personas que comparten comportamientos y/o características similares. Estas colecciones de personas se pueden generar mediante Adobe Experience Platform o desde fuentes externas. Puede usar la variable `/audiences` en la API de segmentación, que le permite recuperar, crear, actualizar y eliminar audiencias mediante programación.

## Primeros pasos

Los extremos utilizados en esta guía forman parte del [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar correctamente llamadas a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de audiencias {#list}

Puede recuperar una lista de todas las audiencias de su organización realizando una solicitud de GET al `/audiences` punto final.

**Formato de API**

La variable `/audiences` el extremo admite varios parámetros de consulta para ayudar a filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales cuando se incluyen recursos. Si realiza una llamada a este extremo sin parámetros, se recuperarán todas las audiencias disponibles para su organización. Se pueden incluir varios parámetros separados por el símbolo &quot;et&quot; (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Los siguientes parámetros de consulta se pueden utilizar al recuperar una lista de audiencias:

| Parámetro de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial para las audiencias devueltas. | `start=5` |
| `limit` | Especifica el número máximo de audiencias devueltas por página. | `limit=10` |
| `sort` | Especifica el orden por el que se ordenarán los resultados. Esto se escribe en el formato `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Un filtro que le permite especificar audiencias que **Exactamente** coincide con el valor de un atributo. Esto se escribe en el formato `property=` | `property=audienceId==test-audience-id` |
| `name` | Filtro que permite especificar audiencias cuyos nombres **contain** el valor proporcionado. Este valor no distingue entre mayúsculas y minúsculas. | `name=Sample` |
| `description` | Filtro que permite especificar audiencias cuyas descripciones **contain** el valor proporcionado. Este valor no distingue entre mayúsculas y minúsculas. | `description=Test Description` |
| `withMetrics` | Filtro que devuelve las métricas además de las audiencias. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>Para las audiencias, las métricas se devuelven en la sección `metrics` y contiene información sobre recuentos de perfiles, creación y actualización de marcas de tiempo.

**Sin métricas**

Se utiliza el siguiente par de solicitud/respuesta cuando se usa la variable `withMetrics` El parámetro de consulta no está presente.

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

Una respuesta correcta devuelve el estado HTTP 200 con una lista de audiencias que se crearon en su organización como JSON.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y solo muestra la primera audiencia devuelta.

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
| `id` | Ambas | Identificador de solo lectura generado por el sistema para la audiencia. |
| `audienceId` | Ambas | Si la audiencia es una audiencia generada por plataforma, es el mismo valor que la variable `id`. Si la audiencia se genera externamente, el cliente proporciona este valor. |
| `schema` | Ambas | Esquema del Modelo de datos de experiencia (XDM) de la audiencia. |
| `imsOrgId` | Ambas | El ID de la organización a la que pertenece la audiencia. |
| `sandbox` | Ambas | Información sobre el entorno limitado al que pertenece la audiencia. Encontrará más información sobre los entornos limitados en [información general sobre los entornos limitados](../../sandboxes/home.md). |
| `name` | Ambas | El nombre de la audiencia. |
| `description` | Ambas | Descripción de la audiencia. |
| `expression` | Generado por la plataforma | Expresión del lenguaje de consulta de perfil (PQL) de la audiencia. Puede encontrar más información sobre las expresiones PQL en la [Guía de expresiones PQL](../pql/overview.md). |
| `mergePolicyId` | Generado por la plataforma | El ID de la política de combinación a la que está asociada la audiencia. Puede encontrar más información sobre las políticas de combinación en la sección [guía de políticas de combinación](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Generado por la plataforma | Muestra cómo se evaluará la audiencia. Los métodos de evaluación posibles incluyen el lote, la transmisión o el borde. Encontrará más información sobre los métodos de evaluación en la [información general sobre segmentación](../home.md) |
| `dependents` | Ambas | Matriz de ID de audiencia que dependen de la audiencia actual. Se utilizaría si está creando una audiencia que es un segmento de un segmento. |
| `dependencies` | Ambas | Matriz de ID de audiencia de la que depende la audiencia. Se utilizaría si está creando una audiencia que es un segmento de un segmento. |
| `type` | Ambas | Campo generado por el sistema que muestra si la audiencia es generada por Platform o si es una audiencia generada externamente. Los valores posibles incluyen `SegmentDefinition` y `ExternalAudience`. A `SegmentDefinition` hace referencia a una audiencia que se generó en Platform, mientras que una `ExternalAudience` hace referencia a una audiencia que no se generó en Platform. |
| `createdBy` | Ambas | ID del usuario que creó la audiencia. |
| `labels` | Ambas | Etiquetas de control de acceso basadas en atributos y uso de datos a nivel de objeto que son relevantes para la audiencia. |
| `namespace` | Ambas | El espacio de nombres al que pertenece la audiencia. Los valores posibles incluyen `AAM`, `AAMSegments`, `AAMTraits`y `AEPSegments`. |
| `audienceMeta` | Externo | Metadatos creados externamente a partir de la audiencia creada externamente. |

**Con métricas**

Se utiliza el siguiente par de solicitud/respuesta cuando se usa la variable `withMetrics` está presente el parámetro de consulta .

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
>La siguiente respuesta se ha truncado para el espacio y solo muestra la primera audiencia devuelta.

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
                        "realized": 11400769
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

Las siguientes listas contienen propiedades **exclusivo** a `withMetrics` respuesta. Si desea conocer las propiedades de audiencia estándar, lea la [sección anterior](#no-metrics).

| Propiedad | Descripción |
| -------- | ----------- |
| `metrics.imsOrgId` | ID de organización de la audiencia. |
| `metrics.sandbox` | La información del entorno limitado relacionada con la audiencia. |
| `metrics.jobId` | El ID del trabajo del segmento que está procesando la audiencia. |
| `metrics.type` | El tipo de trabajo del segmento. Esto puede ser `export` o `batch_segmentation`. |
| `metrics.id` | El ID de la audiencia. |
| `metrics.data` | Métricas relacionadas con la audiencia. Esto incluye información como el número total de perfiles incluidos en la audiencia, el número total de perfiles por espacio de nombres y el número total de perfiles por estado. |
| `metrics.createEpoch` | Marca de tiempo que muestra cuándo se creó la audiencia. |
| `metrics.updateEpoch` | Marca de tiempo que muestra la última actualización de la audiencia. |

## Crear una audiencia nueva {#create}

Puede crear una audiencia nueva realizando una solicitud de POST al `/audiences` punto final.

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
| `description` | Descripción de la audiencia. |
| `type` | Campo que muestra si la audiencia se genera en la plataforma o si es una audiencia generada externamente. Los valores posibles incluyen `SegmentDefinition` y `ExternalAudience`. A `SegmentDefinition` hace referencia a una audiencia que se generó en Platform, mientras que una `ExternalAudience` hace referencia a una audiencia que no se generó en Platform. |
| `expression` | Expresión del lenguaje de consulta de perfil (PQL) de la audiencia. Puede encontrar más información sobre las expresiones PQL en la [Guía de expresiones PQL](../pql/overview.md). |
| `schema` | Esquema del Modelo de datos de experiencia (XDM) de la audiencia. |
| `labels` | Etiquetas de control de acceso basadas en atributos y uso de datos a nivel de objeto que son relevantes para la audiencia. |

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

## Buscar una audiencia específica {#get}

Puede consultar información detallada sobre una audiencia específica realizando una solicitud de GET al `/audiences` y proporcionando el ID de la audiencia que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Parámetro | Descripción |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | ID de la audiencia que intenta recuperar. |
| `property=withmetrics==true` | Un parámetro de consulta opcional que puede usar si desea recuperar una audiencia específica con las métricas de audiencia. |

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

**Generado por la plataforma**

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

## Actualizar un campo en una audiencia {#update-field}

Puede actualizar los campos de una audiencia específica realizando una solicitud de PATCH al `/audiences` y proporcionando el ID de la audiencia que desea actualizar en la ruta de solicitud.

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
| `path` | Ruta del campo que desea actualizar. |
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

## Actualizar una audiencia {#put}

Puede actualizar (sobrescribir) una audiencia específica realizando una solicitud de PUT al `/audiences` y proporcionando el ID de la audiencia que desea actualizar en la ruta de solicitud.

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
| `audienceId` | ID de la audiencia. La utilizan audiencias externas |
| `name` | El nombre de la audiencia. |
| `namespace` |  |
| `description` | Descripción de la audiencia. |
| `type` | Campo generado por el sistema que muestra si la audiencia es generada por Platform o si es una audiencia generada externamente. Los valores posibles incluyen `SegmentDefinition` y `ExternalAudience`. A `SegmentDefinition` hace referencia a una audiencia que se generó en Platform, mientras que una `ExternalAudience` hace referencia a una audiencia que no se generó en Platform. |
| `lifecycle` | El estado de la audiencia. Los valores posibles incluyen `draft`, `published`, `inactive`y `archived`. `draft` representa cuándo se crea la audiencia, `published` cuando se publique la audiencia, `inactive` cuando la audiencia ya no está activa, y `archived` si se elimina la audiencia. |
| `datasetId` | El ID del conjunto de datos con el que se pueden encontrar los datos de audiencia. |
| `labels` | Etiquetas de control de acceso basadas en atributos y uso de datos a nivel de objeto que son relevantes para la audiencia. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la audiencia recién actualizada. Tenga en cuenta que los detalles de la audiencia variarán según si se trata de una audiencia generada por la plataforma o una audiencia generada externamente.

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

Puede eliminar una audiencia específica realizando una solicitud de DELETE al `/audiences` y proporcionando el ID de la audiencia que desea eliminar en la ruta de solicitud.

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
