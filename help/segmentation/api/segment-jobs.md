---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;segment jobs;segment job;API;api;
solution: Experience Platform
title: Trabajos de segmentos
topic: developer guide
description: Esta guía proporciona información para ayudarle a comprender mejor los trabajos de segmentos e incluye ejemplos de llamadas a API para realizar acciones básicas mediante la API.
translation-type: tm+mt
source-git-commit: 8c5c3aed4d46c8b3873009ab9f17ff9bca93302c
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 2%

---


# Extremo de trabajos de segmento

Un trabajo de segmento es un proceso asincrónico que crea un nuevo segmento de audiencia. Hace referencia a una definición [de](./segment-definitions.md)segmento, así como a cualquier directiva [de](../../profile/api/merge-policies.md) combinación que controle cómo [!DNL Real-time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmento se completa correctamente, puede recopilar información diversa sobre el segmento, como los errores que se hayan producido durante el procesamiento y el tamaño final de la audiencia.

Esta guía proporciona información para ayudarle a comprender mejor los trabajos de segmentos e incluye ejemplos de llamadas a API para realizar acciones básicas mediante la API.

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte la guía [de](./getting-started.md) introducción para obtener información importante que debe conocer a fin de realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de trabajos de segmentos {#retrieve-list}

Puede recuperar una lista de todos los trabajos de segmentos para su organización de IMS realizando una solicitud de GET al `/segment/jobs` extremo.

**Formato API**

El extremo admite varios parámetros de consulta para ayudar a filtrar los resultados. `/segment/jobs` Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todos los trabajos de exportación disponibles para su organización. Se pueden incluir varios parámetros, separados por ampersands (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial de los trabajos de segmento devueltos. | `start=1` |
| `limit` | Especifica el número de trabajos de segmento devueltos por página. | `limit=20` |
| `status` | Filtros los resultados en función del estado. Los valores admitidos son NEW, QUEUED, PROCESSING, SUCCEEDED, FAILED, CANCELING, CANCELATION | `status=NEW` |
| `sort` | Ordena los trabajos del segmento devueltos. Se escribe en el formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtros segmenta los trabajos y obtiene coincidencias exactas para el filtro dado. Se puede escribir en cualquiera de los siguientes formatos: <ul><li>`[jsonObjectPath]==[value]` - filtrado en la clave de objeto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtrado dentro de la matriz</li></ul> | `property=segments~segmentId==workInUS` |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de trabajos de segmentos para la organización de IMS especificada como JSON. La siguiente respuesta devuelve una lista de todos los trabajos de segmentos exitosos para la organización de IMS.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y solo mostrará el primer trabajo devuelto.

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
                        "existing":10,
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
| `id` | Identificador de solo lectura generado por el sistema para el trabajo de segmento. |
| `status` | Estado actual del trabajo del segmento. Los valores posibles para el estado incluyen &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; y &quot;SUCCED&quot;. |
| `segments` | Objeto que contiene información sobre las definiciones de segmentos devueltas dentro del trabajo de segmentos. |
| `segments.segment.id` | ID de la definición del segmento. |
| `segments.segment.expression` | Objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |
| `metrics` | Objeto que contiene información de diagnóstico sobre el trabajo del segmento. |
| `metrics.totalTime` | Objeto que contiene información sobre las horas en que se inició y finalizó el trabajo de segmentación, así como el tiempo total que se ha tardado. |
| `metrics.profileSegmentationTime` | Objeto que contiene información sobre los tiempos en que se inició y finalizó la evaluación de segmentación, así como el tiempo total que se ha tardado. |
| `metrics.segmentProfileCounter` | Número de perfiles cualificados por segmento. |
| `metrics.segmentedProfileByNamespaceCounter` | Número de perfiles cualificados para cada Área de nombres de identidad por segmento. |
| `metrics.segmentProfileByStatusCounter` | Recuento de fragmentos **de** perfil para cada estado. Se admiten los tres estados siguientes: <ul><li>&quot;realizado&quot;: el número de nuevos perfiles que ingresaron al segmento.</li><li>&quot;existente&quot;: el número de perfiles que siguen existiendo en el segmento.</li><li>&quot;Salido&quot;: el número de segmentos de perfil que ya no existen en el segmento.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Número total de perfiles combinados por directiva de combinación. |

## Crear un nuevo trabajo de segmento {#create}

Puede crear un nuevo trabajo de segmento haciendo una solicitud de POST al extremo e incluyendo en el cuerpo el ID de la definición del segmento desde el cual desea crear una nueva audiencia. `/segment/jobs`

**Formato API**

```http
POST /segment/jobs
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `segmentId` | ID de la definición de segmento para la que desea crear un trabajo de segmento. Estas definiciones de segmentos pueden pertenecer a distintas directivas de combinación. Encontrará más información sobre las definiciones de segmentos en la guía de punto final de definición de [segmento](./segment-definitions.md). |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del trabajo de segmento recién creado.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
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
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador de solo lectura generado por el sistema para el trabajo de segmento recién creado. |
| `status` | Estado actual del trabajo del segmento. Dado que el trabajo del segmento se acaba de crear, el estado siempre será &quot;NUEVO&quot;. |
| `segments` | Objeto que contiene información sobre las definiciones de segmentos para las que se está ejecutando este trabajo de segmento. |
| `segments.segment.id` | ID de la definición de segmento proporcionada. |
| `segments.segment.expression` | Objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |

## Recuperar un trabajo de segmento específico {#get}

Puede recuperar información detallada sobre un trabajo de segmento específico realizando una solicitud de GET al extremo y proporcionando el ID del trabajo de segmento que desea recuperar en la ruta de solicitud. `/segment/jobs`

**Formato API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | El `id` valor del trabajo de segmento que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el trabajo de segmento especificado.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
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

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador de solo lectura generado por el sistema para el trabajo de segmento. |
| `status` | Estado actual del trabajo del segmento. Los valores posibles para el estado incluyen &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; y &quot;SUCCED&quot;. |
| `segments` | Objeto que contiene información sobre las definiciones de segmentos devueltas dentro del trabajo de segmentos. |
| `segments.segment.id` | ID de la definición del segmento. |
| `segments.segment.expression` | Objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |
| `metrics` | Objeto que contiene información de diagnóstico sobre el trabajo del segmento. |

## Trabajos de recuperación masiva de segmentos {#bulk-get}

Puede recuperar información detallada sobre varios trabajos de segmentos haciendo una solicitud de POST al extremo y proporcionando los `/segment/jobs/bulk-get` valores `id` de los trabajos de segmentos en el cuerpo de la solicitud.

**Formato API**

```http
POST /segment/jobs/bulk-get
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 207 con los trabajos de segmento solicitados.

>[!NOTE]
>
>La siguiente respuesta se ha truncado para el espacio y solo muestra detalles parciales de cada trabajo de segmento. La respuesta completa lista los detalles completos de los trabajos de segmento solicitados.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
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
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
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
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador de solo lectura generado por el sistema para el trabajo de segmento. |
| `status` | Estado actual del trabajo del segmento. Los valores posibles para el estado incluyen &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; y &quot;SUCCED&quot;. |
| `segments` | Objeto que contiene información sobre las definiciones de segmentos devueltas dentro del trabajo de segmentos. |
| `segments.segment.id` | ID de la definición del segmento. |
| `segments.segment.expression` | Objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |

## Cancelar o eliminar un trabajo de segmento específico {#delete}

Puede eliminar un trabajo de segmento específico realizando una solicitud de DELETE al extremo y proporcionando el ID del trabajo de segmento que desea eliminar en la ruta de la solicitud. `/segment/jobs`

>[!NOTE]
>
>La respuesta de la API a la solicitud de eliminación es inmediata. Sin embargo, la eliminación real del trabajo del segmento es asincrónica. En otras palabras, existe una diferencia horaria entre cuándo se realiza la solicitud de eliminación en el trabajo del segmento y cuándo se aplica.

**Formato API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | El `id` valor del trabajo de segmento que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 con la siguiente información.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Pasos siguientes

Después de leer esta guía, ahora podrá comprender mejor cómo funcionan los trabajos de segmentos.