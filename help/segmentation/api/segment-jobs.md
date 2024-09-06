---
solution: Experience Platform
title: Extremo de API de trabajos de segmento
description: El extremo de trabajos de segmento de la API del servicio de segmentación de Adobe Experience Platform le permite administrar mediante programación los trabajos de segmento de su organización.
role: Developer
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: f35fb6aae6aceb75391b1b615ca067a72918f4cf
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 2%

---

# Extremo de trabajos de segmento

Un trabajo de segmentación es un proceso asincrónico que crea un segmento de audiencia bajo demanda. Hace referencia a una [definición de segmento](./segment-definitions.md), así como a cualquier [política de combinación](../../profile/api/merge-policies.md) que controla cómo [!DNL Real-Time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmentación se completa correctamente, puede recopilar información diversa acerca del segmento, como los errores que se hayan podido producir durante el procesamiento y el tamaño final de la audiencia.

Esta guía proporciona información para ayudarle a comprender mejor los trabajos de los segmentos e incluye llamadas de API de muestra para realizar acciones básicas mediante la API.

## Introducción

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperación de una lista de trabajos de segmentos {#retrieve-list}

Puede recuperar una lista de todos los trabajos de segmentos de su organización realizando una solicitud de GET al extremo `/segment/jobs`.

**Formato de API**

El extremo `/segment/jobs` admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Si realiza una llamada a este extremo sin parámetros, se recuperarán todos los trabajos de exportación disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

+++ Una lista de parámetros de consulta disponibles.

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial para los trabajos de segmento devueltos. | `start=1` |
| `limit` | Especifica el número de trabajos de segmento devueltos por página. | `limit=20` |
| `status` | Filtra los resultados según el estado. Los valores admitidos son NEW, QUEUED, PROCESSING, SUCCEEDED, FAILED, CANCELING, CANCELED | `status=NEW` |
| `sort` | Ordena los trabajos de segmento devueltos. Está escrito en el formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtra los trabajos de segmento y obtiene coincidencias exactas para el filtro dado. Se puede escribir en cualquiera de los siguientes formatos: <ul><li>`[jsonObjectPath]==[value]` - filtrado en la clave del objeto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtrado dentro de la matriz</li></ul> | `property=segments~segmentId==workInUS` |

+++

**Solicitud**

+++ Una solicitud de ejemplo para ver una lista de trabajos de segmentos.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de trabajos de segmento para la organización especificada como JSON. Sin embargo, la respuesta será diferente, según el número de definiciones de segmentos dentro del trabajo de segmentación.

>[!BEGINTABS]

>[!TAB Definiciones de segmentos inferiores o iguales a 1500 en su trabajo de segmentación]

Si tiene menos de 1500 definiciones de segmento en ejecución en su trabajo de segmentación, se mostrará una lista completa de todas las definiciones de segmento dentro del atributo `children.segments`.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y solo mostrará el primer trabajo devuelto.

+++ Una respuesta de ejemplo al recuperar una lista de trabajos de segmentos.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

+++

>[!TAB Más de 1500 definiciones de segmento]

Si tiene más de 1500 definiciones de segmento en ejecución en su trabajo de segmento, el atributo `children.segments` mostrará `*`, lo que indica que se están evaluando todas las definiciones de segmento.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y solo mostrará el primer trabajo devuelto.

+++ Una respuesta de ejemplo al ver una lista de trabajos de segmentos.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "*",
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador de solo lectura generado por el sistema para el trabajo de segmentación. |
| `status` | El estado actual del trabajo de segmentación. Los valores potenciales para el estado incluyen &quot;NUEVO&quot;, &quot;PROCESANDO&quot;, &quot;CANCELANDO&quot;, &quot;CANCELADO&quot;, &quot;FALLIDO&quot; y &quot;CORRECTO&quot;. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento devueltas en el trabajo de segmentación. |
| `segments.segment.id` | El ID de la definición del segmento. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |
| `metrics` | Un objeto que contiene información de diagnóstico sobre el trabajo de segmentación. |
| `metrics.totalTime` | Un objeto que contiene información sobre las veces que se inició y finalizó el trabajo de segmentación, así como el tiempo total empleado. |
| `metrics.profileSegmentationTime` | Un objeto que contiene información sobre las veces que se inició y finalizó la evaluación de la segmentación, así como el tiempo total empleado. |
| `metrics.segmentProfileCounter` | El número de perfiles cualificados por segmento. |
| `metrics.segmentedProfileByNamespaceCounter` | El número de perfiles cualificados para cada área de nombres de identidad por definición de segmento. |
| `metrics.segmentProfileByStatusCounter` | Recuento de perfiles para cada estado. Se admiten los tres estados siguientes: <ul><li>&quot;realizado&quot;: número de perfiles que cumplen los requisitos para la definición del segmento.</li><li>&quot;saliente&quot;: el número de perfiles que ya no existen en la definición del segmento.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Número total de perfiles combinados por política de combinación. |

+++

>[!ENDTABS]

## Creación de un nuevo trabajo de segmentación {#create}

Puede crear un nuevo trabajo de segmento realizando una solicitud de POST al extremo `/segment/jobs` e incluyendo en el cuerpo el ID de la definición del segmento a partir de la cual desea crear una nueva audiencia.

**Formato de API**

```http
POST /segment/jobs
```

Al crear un nuevo trabajo de segmento, la solicitud y la respuesta diferirán según el número de definiciones de segmento dentro del trabajo de segmento.

>[!BEGINTABS]

>[!TAB Menos o igual a 1500 segmentos en su trabajo de segmentación]

**Solicitud**

+++Una solicitud de ejemplo para crear un nuevo trabajo de segmentación

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `segmentId` | El ID de la definición del segmento para el que desea crear un trabajo de segmento. Estas definiciones de segmentos pueden pertenecer a distintas políticas de combinación. Encontrará más información sobre las definiciones de segmentos en la [guía de extremo de definición de segmento](./segment-definitions.md). |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre el trabajo de segmento recién creado.

+++ Una respuesta de ejemplo al crear un nuevo trabajo de segmentación.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Un identificador de solo lectura generado por el sistema para el trabajo de segmentación recién creado. |
| `status` | El estado actual del trabajo de segmentación. Dado que el trabajo de segmentación es recién creado, el estado siempre será &quot;NUEVO&quot;. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento para las que se ejecuta este trabajo de segmento. |
| `segments.segment.id` | El ID de la definición de segmento proporcionada. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |

+++

>[!TAB Más de 1500 definiciones de segmento en su trabajo de segmentación]

**Solicitud**

>[!NOTE]
>
>Aunque puede crear un trabajo de segmento con más de 1500 definiciones de segmento, esto es **altamente no recomendado**.

+++ Una solicitud de ejemplo para crear un trabajo de segmentación.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "segments": [
        {
            "segmentId": "*"
        }
    ]
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schema.name` | Nombre del esquema para las definiciones de segmentos. |
| `segments.segmentId` | Al ejecutar un trabajo de segmentación con más de 1500 segmentos, deberá pasar `*` como ID del segmento para que indique que desea ejecutar un trabajo de segmentación con todos los segmentos. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del trabajo de segmento recién creado.

+++ Una respuesta de ejemplo al crear un trabajo de segmentación.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Un identificador de solo lectura generado por el sistema para el trabajo de segmentación recién creado. |
| `status` | El estado actual del trabajo de segmentación. Dado que el trabajo de segmentación es recién creado, el estado siempre será `NEW`. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento para las que se ejecuta este trabajo de segmento. |
| `segments.segment.id` | `*` significa que este trabajo de segmento se está ejecutando para todas las definiciones de segmento de su organización. |

+++

>[!ENDTABS]


## Recuperar un trabajo de segmento específico {#get}

GET Puede recuperar información detallada sobre un trabajo de segmento específico realizando una solicitud al extremo `/segment/jobs` y proporcionando el ID del trabajo de segmento que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | El valor `id` del trabajo de segmentación que desea recuperar. |

**Solicitud**

+++ Una solicitud de ejemplo para recuperar un trabajo de segmentación.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el trabajo de segmento especificado.  Sin embargo, la respuesta variará según el número de definiciones de segmentos dentro del trabajo de segmentación.

>[!BEGINTABS]

>[!TAB Definiciones de segmentos inferiores o iguales a 1500 en su trabajo de segmentación]

Si tiene menos de 1500 definiciones de segmento en ejecución en su trabajo de segmentación, se mostrará una lista completa de todas las definiciones de segmento dentro del atributo `children.segments`.

+++ Una respuesta de ejemplo para recuperar un trabajo de segmentación.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

+++

>[!TAB Más de 1500 definiciones de segmento]

Si tiene más de 1500 definiciones de segmento en ejecución en su trabajo de segmento, el atributo `children.segments` mostrará `*`, lo que indica que se están evaluando todas las definiciones de segmento.

+++ Una respuesta de ejemplo para recuperar un trabajo de segmentación.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador de solo lectura generado por el sistema para el trabajo de segmentación. |
| `status` | El estado actual del trabajo de segmentación. Los valores potenciales para el estado incluyen &quot;NUEVO&quot;, &quot;PROCESANDO&quot;, &quot;CANCELANDO&quot;, &quot;CANCELADO&quot;, &quot;FALLIDO&quot; y &quot;CORRECTO&quot;. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento devueltas en el trabajo de segmentación. |
| `segments.segment.id` | El ID de la definición del segmento. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |
| `metrics` | Un objeto que contiene información de diagnóstico sobre el trabajo de segmentación. |

+++

>[!ENDTABS]

## Recuperar trabajos de segmentos por lotes {#bulk-get}

Puede recuperar información detallada sobre varios trabajos de segmento realizando una solicitud de POST al extremo `/segment/jobs/bulk-get` y proporcionando los valores `id` de los trabajos de segmento en el cuerpo de la solicitud.

**Formato de API**

```http
POST /segment/jobs/bulk-get
```

**Solicitud**

+++ Una solicitud de ejemplo para utilizar el extremo de recuperación masiva.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 207 con los trabajos de segmento solicitados. Sin embargo, el valor del atributo `children.segments` difiere según si el trabajo de segmento se está ejecutando para más de 1500 definiciones de segmento.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio, y solo muestra detalles parciales de cada trabajo de segmento. La respuesta completa enumerará los detalles completos para los trabajos de segmento solicitados.

+++ Una respuesta de ejemplo al utilizar la respuesta de obtención masiva.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "*"
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador de solo lectura generado por el sistema para el trabajo de segmentación. |
| `status` | El estado actual del trabajo de segmentación. Los valores potenciales para el estado incluyen &quot;NUEVO&quot;, &quot;PROCESANDO&quot;, &quot;CANCELANDO&quot;, &quot;CANCELADO&quot;, &quot;FALLIDO&quot; y &quot;CORRECTO&quot;. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento devueltas en el trabajo de segmentación. |
| `segments.segment.id` | El ID de la definición del segmento. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |

+++

## Cancelar o eliminar un trabajo de segmento específico {#delete}

Puede eliminar un trabajo de segmento específico realizando una solicitud de DELETE al extremo `/segment/jobs` y proporcionando el ID del trabajo de segmento que desea eliminar en la ruta de solicitud.

>[!NOTE]
>
>La respuesta de la API a la solicitud de eliminación es inmediata. Sin embargo, la eliminación real del trabajo de segmentación es asíncrona. En otras palabras, existe una diferencia horaria entre el momento en el que se realiza la solicitud de eliminación al trabajo del segmento y el momento en el que se aplica.

**Formato de API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | El valor `id` del trabajo de segmentación que desea eliminar. |

**Solicitud**

+++ Una solicitud de ejemplo para eliminar un trabajo de segmentación.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 con un cuerpo de respuesta vacío.

## Pasos siguientes

Después de leer esta guía, ahora tiene una mejor comprensión de cómo funcionan los trabajos de segmentos.
