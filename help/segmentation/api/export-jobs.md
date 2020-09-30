---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;export jobs;api;
solution: Experience Platform
title: Extremo de trabajos de exportación
topic: developer guide
description: Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener a los miembros del segmento de audiencia en conjuntos de datos. Puede utilizar el extremo /export/Jobs en la API de segmentación de Adobe Experience Platform, que le permite recuperar, crear y cancelar trabajos de exportación mediante programación.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 2%

---


# Extremo de trabajos de exportación

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener a los miembros del segmento de audiencia en conjuntos de datos. Puede utilizar el extremo en la API de segmentación de Adobe Experience Platform, que le permite recuperar, crear y cancelar trabajos de exportación mediante programación. `/export/jobs`

>[!NOTE]
>
>Esta guía cubre el uso de trabajos de exportación en el [!DNL Segmentation API]. Para obtener información sobre cómo administrar los trabajos de exportación de [!DNL Real-time Customer Profile] datos, consulte la guía sobre los trabajos de [exportación en la API de Perfil](../../profile/api/export-jobs.md)

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte la guía [de](./getting-started.md) introducción para obtener información importante que debe conocer a fin de realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperar una lista de trabajos de exportación {#retrieve-list}

Puede recuperar una lista de todos los trabajos de exportación para su organización de IMS mediante una solicitud de GET al `/export/jobs` extremo.

**Formato API**

El extremo admite varios parámetros de consulta para ayudar a filtrar los resultados. `/export/jobs` Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todos los trabajos de exportación disponibles para su organización. Se pueden incluir varios parámetros, separados por ampersands (`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{LIMIT}` | Especifica el número de trabajos de exportación devueltos. |
| `{OFFSET}` | Especifica el desplazamiento de las páginas de resultados. |
| `{STATUS}` | Filtros los resultados en función del estado. Los valores admitidos son &quot;NEW&quot;, &quot;SUCCEEDED&quot; y &quot;FAILED&quot;. |

**Solicitud**

La siguiente solicitud recuperará los dos últimos trabajos de exportación dentro de la organización de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de trabajos de exportación completados correctamente, según el parámetro de consulta proporcionado en la ruta de la solicitud.

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
        },
        {
            "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
            "errors": [
                {
                    "code": "0090000009",
                    "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
                },
                {
                    "code": "unknown",
                    "msg": "Job aborted.",
                    "callStack": "org.apache.spark.SparkException: Job aborted."
                }
            ],
            "jobType": "BATCH",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized", "existing"]
                    }
                ]
            },
            "id": 722,
            "schema": {
                "name": "_xdm.context.profile"
            },
            "mergePolicy": {
                "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
                "version": 1
            },
            "status": "FAILED",
            "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
            "computeGatewayJobId": {
                "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
            },
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1538573416687,
                    "endTimeInMs": 1538573922551,
                    "totalTimeInMs": 505864
                },
                "profileExportTime": {
                    "startTimeInMs": 1538573872211,
                    "endTimeInMs": 1538573918809,
                    "totalTimeInMs": 46598
                }
            },
            "destination": {
                "datasetId": "5bb4c46757920712f924a3eb",
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `destination` | Información de destino de los datos exportados:<ul><li>`datasetId`:: ID del conjunto de datos donde se exportaron los datos.</li><li>`segmentPerBatch`:: Un valor booleano que muestra si los ID de segmento están consolidados o no. Un valor &quot;false&quot; significa que todos los ID de segmento se exportan en un único ID de lote. Un valor &quot;true&quot; significa que un ID de segmento se exporta a un ID de lote. **Nota:** La configuración del valor en true puede afectar al rendimiento de exportación de lotes.</li></ul> |
| `fields` | Lista de los campos exportados, separados por comas. |
| `schema.name` | Nombre del esquema asociado con el conjunto de datos donde se exportan los datos. |
| `filter.segments` | Los segmentos que se exportan. Se incluyen los siguientes campos:<ul><li>`segmentId`:: ID del segmento al que se exportarán los perfiles.</li><li>`segmentNs`:: Área de nombres de segmentos para el `segmentID`.</li><li>`status`:: Matriz de cadenas que proporciona un filtro de estado para el `segmentID`. De forma predeterminada, `status` tendrá el valor `["realized", "existing"]` que representa todos los perfiles que entran en el segmento en el momento actual. Los valores posibles incluyen: &quot;realizado&quot;, &quot;existente&quot; y &quot;salido&quot;.</li></ul> |
| `mergePolicy` | Combinar información de directiva para los datos exportados. |
| `metrics.totalTime` | Campo que indica el tiempo total que tardó en ejecutarse el trabajo de exportación. |
| `metrics.profileExportTime` | Campo que indica el tiempo que tardan los perfiles en exportarse. |
| `page` | Información sobre la paginación de los trabajos de exportación solicitados. |
| `link.next` | Vínculo a la siguiente página de trabajos de exportación. |

## Crear un nuevo trabajo de exportación {#create}

Puede crear un nuevo trabajo de exportación realizando una solicitud de POST al `/export/jobs` extremo.

**Formato API**

```http
POST /export/jobs
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de exportación, configurado con los parámetros proporcionados en la carga útil.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `fields` | Lista de los campos exportados, separados por comas. Si se deja en blanco, se exportarán todos los campos. |
| `mergePolicy` | Especifica la directiva de combinación que regirá los datos exportados. Incluya este parámetro cuando se exporten varios segmentos. Si no se proporciona, la exportación tendrá la misma directiva de combinación que el segmento dado. |
| `filter` | Objeto que especifica los segmentos que se van a incluir en el trabajo de exportación por ID, tiempo de cualificación o tiempo de ingesta, según las subpropiedades que se indican a continuación. Si se deja en blanco, se exportarán todos los datos. |
| `filter.segments` | Especifica los segmentos que se van a exportar. Si se omite este valor, se exportarán todos los datos de todos los perfiles. Acepta una matriz de objetos de segmento, cada uno de los cuales contiene los campos siguientes:<ul><li>`segmentId`:: **(Necesario si se utiliza`segments`)** ID de segmento para la exportación de perfiles.</li><li>`segmentNs` *(Opcional)* Área de nombres de segmentos para el `segmentID`.</li><li>`status` *(Opcional)* Matriz de cadenas que proporciona un filtro de estado para el `segmentID`. De forma predeterminada, `status` tendrá el valor `["realized", "existing"]` que representa todos los perfiles que entran en el segmento en el momento actual. Possible values include: `"realized"`, `"existing"`, and `"exited"`.</li></ul> |
| `filter.segmentQualificationTime` | Filtrar según el tiempo de calificación del segmento. Se puede proporcionar la hora de inicio y/o la hora de finalización. |
| `filter.segmentQualificationTime.startTime` | Tiempo de inicio de calificación de segmentos para un ID de segmento para un estado determinado. No se proporciona, no habrá ningún filtro en el tiempo de inicio para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | Hora de finalización de la calificación del segmento para un ID de segmento para un estado determinado. No se proporciona, no habrá ningún filtro en la hora de finalización para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | Limita los perfiles exportados a incluir solo aquellos que se hayan actualizado después de esta marca de tiempo. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` en el caso de **perfiles**, en su caso: Incluye todos los perfiles combinados en los que la marca de tiempo actualizada combinada es buena que la marca de tiempo dada. Admite `greater_than` operando.</li><li>`fromIngestTimestamp` para **eventos**: Todos los eventos ingeridos después de esta marca de tiempo se exportarán según el resultado de perfil resultante. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos.</li> |
| `filter.emptyProfiles` | Valor booleano que indica si se va a filtrar por perfiles vacíos. Los perfiles pueden contener registros de perfiles, registros de ExperienceEvent o ambos. Los perfiles sin registros de perfil y solo los registros de ExperienceEvent se denominan &quot;emptyProfiles&quot;. Para exportar todos los perfiles del almacén de perfiles, incluido &quot;emptyProfiles&quot;, establezca el valor de `emptyProfiles` en `true`. Si `emptyProfiles` se establece en `false`, solo se exportan los perfiles con registros de perfil en el almacén. De forma predeterminada, si no se incluye `emptyProfiles` el atributo, solo se exportan los perfiles que contienen registros de perfil. |
| `additionalFields.eventList` | Controla los campos de evento de la serie temporal exportados para objetos secundarios o asociados proporcionando una o varias de las siguientes opciones:<ul><li>`fields`:: Controle los campos que desea exportar.</li><li>`filter`:: Especifica criterios que limitan los resultados incluidos de los objetos asociados. Espera un valor mínimo necesario para la exportación, normalmente una fecha.</li><li>`filter.fromIngestTimestamp`:: Filtros eventos de series temporales a los que se han ingerido después de la marca de tiempo proporcionada. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos.</li><li>`filter.toIngestTimestamp`:: Filtros la marca de tiempo a las que se han ingerido antes de la marca de tiempo proporcionada. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos.</li></ul> |
| `destination` | **(Requerido)** Información sobre los datos exportados:<ul><li>`datasetId`:: **(Requerido)** El ID del conjunto de datos en el que se exportan los datos.</li><li>`segmentPerBatch`:: *(Opcional)* Un valor booleano que, si no se proporciona, toma el valor predeterminado &quot;false&quot;. Un valor &quot;false&quot; exporta todos los ID de segmento en un único ID de lote. Un valor &quot;true&quot; exporta un ID de segmento en un ID de lote. Tenga en cuenta que la configuración del valor como &quot;true&quot; puede afectar al rendimiento de exportación de lotes.</li></ul> |
| `schema.name` | **(Requerido)** El nombre del esquema asociado con el conjunto de datos donde se exportan los datos. |
| `evaluationInfo.segmentation` | *(Opcional)* Un valor booleano que, si no se proporciona, toma como valor predeterminado `false`. Un valor de `true` indica que la segmentación debe realizarse en el trabajo de exportación. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del trabajo de exportación recién creado.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Valor de sólo lectura generado por el sistema que identifica el trabajo de exportación que se acaba de crear. |

Como alternativa, si `destination.segmentPerBatch` se hubiera establecido en `true`, el `destination` objeto de arriba tendría una `batches` matriz, como se muestra a continuación:

```json
    "destination": {
        "dataSetId" : "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches" : [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

## Recuperar un trabajo de exportación específico {#get}

Puede recuperar información detallada sobre un trabajo de exportación específico haciendo una solicitud de GET al extremo y proporcionando el ID del trabajo de exportación que desea recuperar en la ruta de la solicitud. `/export/jobs`

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | El `id` del trabajo de exportación al que desea acceder. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el trabajo de exportación especificado.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `destination` | Información de destino de los datos exportados:<ul><li>`datasetId`:: ID del conjunto de datos en el que se exportaron los datos.</li><li>`segmentPerBatch`:: Un valor booleano que muestra si los ID de segmento están consolidados o no. Un valor de `false` significa que todos los ID de segmento se han incluido en un único ID de lote. Un valor de `true` significa que un ID de segmento se exporta a un ID de lote.</li></ul> |
| `fields` | Lista de los campos exportados, separados por comas. |
| `schema.name` | Nombre del esquema asociado con el conjunto de datos donde se exportan los datos. |
| `filter.segments` | Los segmentos que se exportan. Se incluyen los siguientes campos:<ul><li>`segmentId`:: ID del segmento para perfiles que se van a exportar.</li><li>`segmentNs`:: Área de nombres de segmentos para el `segmentID`.</li><li>`status`:: Matriz de cadenas que proporciona un filtro de estado para el `segmentID`. De forma predeterminada, `status` tendrá el valor `["realized", "existing"]` que representa todos los perfiles que entran en el segmento en el momento actual. Los valores posibles incluyen: &quot;realizado&quot;, &quot;existente&quot; y &quot;salido&quot;.</li></ul> |
| `mergePolicy` | Combinar información de directiva para los datos exportados. |
| `metrics.totalTime` | Campo que indica el tiempo total que tardó en ejecutarse el trabajo de exportación. |
| `metrics.profileExportTime` | Campo que indica el tiempo que tardan los perfiles en exportarse. |
| `totalExportedProfileCounter` | Número total de perfiles exportados en todos los lotes. |

## Cancelar o eliminar un trabajo de exportación específico {#delete}

Puede solicitar la eliminación del trabajo de exportación especificado realizando una solicitud de DELETE al extremo y proporcionando el ID del trabajo de exportación que desea eliminar en la ruta de la solicitud. `/export/jobs`

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | El `id` del trabajo de exportación que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 con el siguiente mensaje:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Pasos siguientes

Después de leer esta guía, ahora podrá comprender mejor cómo funcionan los trabajos de exportación.