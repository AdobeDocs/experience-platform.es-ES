---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;trabajos de segmento;trabajo de segmento;API;api;
solution: Experience Platform
title: Punto final de la API de trabajos de segmento
topic-legacy: developer guide
description: El extremo de trabajos de segmentos en la API del servicio de segmentación de Adobe Experience Platform le permite administrar mediante programación los trabajos de segmentos de su organización.
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# Punto final de trabajos de segmentos

Un trabajo de segmento es un proceso asincrónico que crea un nuevo segmento de audiencia. Hace referencia a una [definición de segmento](./segment-definitions.md), así como a las [políticas de combinación](../../profile/api/merge-policies.md) que controlan cómo [!DNL Real-time Customer Profile] combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmento se completa correctamente, puede recopilar información variada sobre el segmento, como los errores que puedan haberse producido durante el procesamiento y el tamaño definitivo de la audiencia.

Esta guía proporciona información para ayudarle a comprender mejor los trabajos de los segmentos e incluye ejemplos de llamadas a la API para realizar acciones básicas con la API.

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de trabajos de segmentos {#retrieve-list}

Puede recuperar una lista de todos los trabajos de segmentos para su organización IMS realizando una solicitud de GET al extremo `/segment/jobs` .

**Formato de API**

El extremo `/segment/jobs` admite varios parámetros de consulta para ayudar a filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todos los trabajos de exportación disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo &quot;`&`&quot;.

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `start` | Especifica el desplazamiento inicial para los trabajos de segmento devueltos. | `start=1` |
| `limit` | Especifica el número de trabajos de segmento devueltos por página. | `limit=20` |
| `status` | Filtra los resultados según el estado. Los valores admitidos son NUEVO, EN COLA, PROCESANDO, CORRECTO, FALLIDO, CANCELAR, CANCELADO | `status=NEW` |
| `sort` | Solicita los trabajos del segmento devueltos. Se escribe con el formato `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtra los trabajos de segmentos y obtiene coincidencias exactas para el filtro dado. Puede escribirse en cualquiera de los siguientes formatos: <ul><li>`[jsonObjectPath]==[value]` - filtrado en la clave del objeto</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtrado dentro de la matriz</li></ul> | `property=segments~segmentId==workInUS` |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de trabajos de segmento para la organización IMS especificada como JSON. La siguiente respuesta devuelve una lista de todos los trabajos de segmentos correctos para la organización IMS.

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
| `id` | Identificador de solo lectura generado por el sistema para el trabajo del segmento. |
| `status` | Estado actual del trabajo del segmento. Los posibles valores para el estado incluyen &quot;NUEVO&quot;, &quot;PROCESAMIENTO&quot;, &quot;CANCELACIÓN&quot;, &quot;CANCELADO&quot;, &quot;FALLIDO&quot; y &quot;SUCCEDIDO&quot;. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento devueltas dentro del trabajo de segmento. |
| `segments.segment.id` | ID de la definición del segmento. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |
| `metrics` | Un objeto que contiene información de diagnóstico sobre el trabajo del segmento. |
| `metrics.totalTime` | Un objeto que contiene información sobre las veces que se inició y finalizó el trabajo de segmentación, así como el tiempo total necesario. |
| `metrics.profileSegmentationTime` | Un objeto que contiene información sobre las veces que se inició y finalizó la evaluación de la segmentación, así como el tiempo total necesario. |
| `metrics.segmentProfileCounter` | Número de perfiles clasificados por segmento. |
| `metrics.segmentedProfileByNamespaceCounter` | Número de perfiles cualificados para cada área de nombres de identidad por segmento. |
| `metrics.segmentProfileByStatusCounter` | Recuento de perfiles para cada estado. Se admiten los tres estados siguientes: <ul><li>&quot;realizada&quot;: el número de perfiles nuevos que se han introducido en el segmento.</li><li>&quot;existente&quot; : el número de perfiles que siguen existiendo en el segmento.</li><li>&quot;Salido&quot;: el número de segmentos de perfil que ya no existen en el segmento.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Número total de perfiles combinados por directiva de combinación. |

## Crear un nuevo trabajo de segmento {#create}

Puede crear un nuevo trabajo de segmento realizando una solicitud de POST al extremo `/segment/jobs` e incluyendo en el cuerpo el ID de la definición del segmento desde la que desea crear una nueva audiencia.

**Formato de API**

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
| `segmentId` | El ID de la definición de segmento para la que desea crear un trabajo de segmento. Estas definiciones de segmento pueden pertenecer a distintas políticas de combinación. Puede encontrar más información sobre las definiciones de segmentos en la [guía de extremo de definición de segmento](./segment-definitions.md). |

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
| `segments` | Un objeto que contiene información sobre las definiciones de segmento para las que se está ejecutando este trabajo de segmento. |
| `segments.segment.id` | El ID de la definición de segmento que ha proporcionado. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |

## Recuperar un trabajo de segmento específico {#get}

Puede recuperar información detallada sobre un trabajo de segmento específico realizando una solicitud de GET al extremo `/segment/jobs` y proporcionando el ID del trabajo de segmento que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | El valor `id` del trabajo del segmento que desea recuperar. |

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
| `id` | Identificador de solo lectura generado por el sistema para el trabajo del segmento. |
| `status` | Estado actual del trabajo del segmento. Los posibles valores para el estado incluyen &quot;NUEVO&quot;, &quot;PROCESAMIENTO&quot;, &quot;CANCELACIÓN&quot;, &quot;CANCELADO&quot;, &quot;FALLIDO&quot; y &quot;SUCCEDIDO&quot;. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento devueltas dentro del trabajo de segmento. |
| `segments.segment.id` | ID de la definición del segmento. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |
| `metrics` | Un objeto que contiene información de diagnóstico sobre el trabajo del segmento. |

## Trabajos de recuperación masiva de segmentos {#bulk-get}

Puede recuperar información detallada sobre varios trabajos de segmentos realizando una solicitud de POST al extremo `/segment/jobs/bulk-get` y proporcionando los valores `id` de los trabajos de segmentos en el cuerpo de la solicitud.

**Formato de API**

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
>La siguiente respuesta se ha truncado para el espacio y solo se muestran detalles parciales de cada trabajo de segmento. La respuesta completa enumerará los detalles completos de los trabajos de segmento solicitados.

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
| `id` | Identificador de solo lectura generado por el sistema para el trabajo del segmento. |
| `status` | Estado actual del trabajo del segmento. Los posibles valores para el estado incluyen &quot;NUEVO&quot;, &quot;PROCESAMIENTO&quot;, &quot;CANCELACIÓN&quot;, &quot;CANCELADO&quot;, &quot;FALLIDO&quot; y &quot;SUCCEDIDO&quot;. |
| `segments` | Un objeto que contiene información sobre las definiciones de segmento devueltas dentro del trabajo de segmento. |
| `segments.segment.id` | ID de la definición del segmento. |
| `segments.segment.expression` | Un objeto que contiene información sobre la expresión de la definición del segmento, escrita en PQL. |

## Cancelar o eliminar un trabajo de segmento específico {#delete}

Puede eliminar un trabajo de segmento específico realizando una solicitud de DELETE al extremo `/segment/jobs` y proporcionando el ID del trabajo de segmento que desea eliminar en la ruta de solicitud.

>[!NOTE]
>
>La respuesta de API a la solicitud de eliminación es inmediata. Sin embargo, la eliminación real del trabajo del segmento es asíncrona. En otras palabras, existe una diferencia horaria entre el momento en que se realiza la solicitud de eliminación en el trabajo del segmento y el momento en que se aplica.

**Formato de API**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | El valor `id` del trabajo del segmento que desea eliminar. |

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

Después de leer esta guía, ahora puede comprender mejor cómo funcionan los trabajos de los segmentos.
