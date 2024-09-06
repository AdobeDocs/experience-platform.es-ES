---
solution: Experience Platform
title: Extremo de API de trabajos de exportación de segmentos
description: Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener los miembros de segmentos de audiencia en conjuntos de datos. Puede utilizar el extremo /export/job en la API del servicio de segmentación de Adobe Experience Platform, que le permite recuperar, crear y cancelar mediante programación los trabajos de exportación.
role: Developer
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---

# Extremo de trabajos de exportación de segmentos

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener los miembros de segmentos de audiencia en conjuntos de datos. Puede utilizar el extremo `/export/jobs` en la API de segmentación de Adobe Experience Platform, que le permite recuperar, crear y cancelar mediante programación los trabajos de exportación.

>[!NOTE]
>
>Esta guía describe el uso de los trabajos de exportación en [!DNL Segmentation API]. Para obtener información sobre cómo administrar los trabajos de exportación para los datos de [!DNL Real-Time Customer Profile], consulte la guía sobre [trabajos de exportación en la API del perfil](../../profile/api/export-jobs.md)

## Introducción

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperación de una lista de trabajos de exportación {#retrieve-list}

Puede recuperar una lista de todos los trabajos de exportación para su organización realizando una solicitud de GET al extremo `/export/jobs`.

**Formato de API**

El extremo `/export/jobs` admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudar a reducir los costes generales. Si realiza una llamada a este extremo sin parámetros, se recuperarán todos los trabajos de exportación disponibles para su organización. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

+++ Una lista de parámetros de consulta disponibles.

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `limit` | Especifica el número de trabajos de exportación devueltos. | `limit=10` |
| `offset` | Especifica el desplazamiento de las páginas de resultados. | `offset=1540974701302_96` |
| `status` | Filtra los resultados según el estado. Los valores admitidos son &quot;NEW&quot;, &quot;SUCCEEDED&quot; y &quot;FAILED&quot;. | `status=NEW` |

+++

**Solicitud**

La siguiente solicitud recuperará los dos últimos trabajos de exportación dentro de su organización.

+++ Una solicitud de ejemplo para recuperar los trabajos de exportación.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de los trabajos de exportación completados correctamente, según el parámetro de consulta proporcionado en la ruta de solicitud.

+++ Una respuesta de ejemplo al recuperar los trabajos de exportación.

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
                        "status": ["realized"]
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
| `destination` | Información de destino para los datos exportados:<ul><li>`datasetId`: ID del conjunto de datos donde se exportaron los datos.</li><li>`segmentPerBatch`: Valor booleano que muestra si los ID de segmento están consolidados o no. El valor &quot;false&quot; significa que todos los ID de segmento se exportan a un único ID de lote. El valor &quot;true&quot; significa que se exporta un ID de segmento a un ID de lote. **Nota:** Si establece el valor en true, puede afectar al rendimiento de la exportación por lotes.</li></ul> |
| `fields` | Una lista de los campos exportados, separados por comas. |
| `schema.name` | Nombre del esquema asociado al conjunto de datos donde se exportarán los datos. |
| `filter.segments` | Los segmentos que se exportan. Se incluyen los siguientes campos:<ul><li>`segmentId`: ID del segmento al que se exportarán los perfiles.</li><li>`segmentNs`: área de nombres de segmento para el objeto `segmentID` dado.</li><li>`status`: matriz de cadenas que proporciona un filtro de estado para `segmentID`. De manera predeterminada, `status` tendrá el valor `["realized"]`, que representa todos los perfiles que pertenecen al segmento en el momento actual. Los valores posibles incluyen: `realized` y `exited`. Un valor de `realized` significa que el perfil califica para el segmento. Un valor de `exiting` significa que el perfil está saliendo del segmento.</li></ul> |
| `mergePolicy` | Combinar información de directivas para los datos exportados. |
| `metrics.totalTime` | Campo que indica el tiempo total que tardó en ejecutarse el trabajo de exportación. |
| `metrics.profileExportTime` | Campo que indica el tiempo que tardan los perfiles en exportar. |
| `page` | Información sobre la paginación de los trabajos de exportación solicitados. |
| `link.next` | Un vínculo a la página siguiente de los trabajos de exportación. |

+++

## Creación de un nuevo trabajo de exportación {#create}

Puede crear un nuevo trabajo de exportación realizando una solicitud de POST al extremo `/export/jobs`.

**Formato de API**

```http
POST /export/jobs
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de exportación, configurado por los parámetros proporcionados en la carga útil.

+++ Una solicitud de ejemplo para crear un trabajo de exportación.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `fields` | Una lista de los campos exportados, separados por comas. Si se deja en blanco, se exportan todos los campos. |
| `mergePolicy` | Especifica la política de combinación que rige los datos exportados. Incluya este parámetro cuando se exporten varios segmentos. Si no se proporciona, la exportación sigue la misma política de combinación que el segmento dado. |
| `filter` | Un objeto que especifica los segmentos que se van a incluir en el trabajo de exportación por ID, tiempo de calificación o tiempo de ingesta, según las subpropiedades que se enumeran a continuación. Si se deja en blanco, se exportarán todos los datos. |
| `filter.segments` | Especifica los segmentos que se van a exportar. Si se omite este valor, se exportarán todos los datos de todos los perfiles. Acepta una matriz de objetos de segmento, cada uno de los cuales contiene los siguientes campos:<ul><li>`segmentId`: **(obligatorio si se usa `segments`)** ID de segmento para los perfiles que se van a exportar.</li><li>`segmentNs` *(Opcional)* espacio de nombres de segmento para el `segmentID` dado.</li><li>`status` *(Opcional)* Una matriz de cadenas que proporciona un filtro de estado para `segmentID`. De manera predeterminada, `status` tendrá el valor `["realized"]`, que representa todos los perfiles que pertenecen al segmento en el momento actual. Los valores posibles incluyen: `realized` y `exited`.  Un valor de `realized` significa que el perfil califica para el segmento. Un valor de `exiting` significa que el perfil está saliendo del segmento.</li></ul> |
| `filter.segmentQualificationTime` | Filtro basado en el tiempo de calificación de segmentos. Se puede proporcionar la hora de inicio o la hora de finalización. |
| `filter.segmentQualificationTime.startTime` | Hora de inicio de calificación de segmentos para un ID de segmento para un estado determinado. Si no se proporciona, no habrá ningún filtro en la hora de inicio para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339). |
| `filter.segmentQualificationTime.endTime` | Hora de finalización de calificación de segmentos para un ID de segmento para un estado determinado. Si no se proporciona, no habrá ningún filtro en el momento de finalización para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339). |
| `filter.fromIngestTimestamp ` | Limita los perfiles exportados para incluir solo los que se han actualizado después de esta marca de tiempo. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339). <ul><li>`fromIngestTimestamp` para **perfiles**, si se proporciona: incluye todos los perfiles combinados en los que la marca de tiempo actualizada combinada es mayor que la marca de tiempo dada. Admite el operando `greater_than`.</li><li>`fromIngestTimestamp` para **eventos**: todos los eventos introducidos después de esta marca de tiempo se exportarán correspondiente al resultado del perfil resultante. No es la hora del evento en sí, sino la hora de ingesta de los eventos.</li> |
| `filter.emptyProfiles` | Un valor booleano que indica si se filtran los perfiles vacíos. Los perfiles pueden contener registros de perfil, registros de ExperienceEvent o ambos. Los perfiles sin registros de perfil y solo registros de ExperienceEvent se denominan &quot;emptyProfiles&quot;. Para exportar todos los perfiles del almacén de perfiles, incluido &quot;emptyProfiles&quot;, establezca el valor de `emptyProfiles` en `true`. Si `emptyProfiles` se establece en `false`, solo se exportan los perfiles con registros de perfil en el almacén. De forma predeterminada, si el atributo `emptyProfiles` no se incluye, solo se exportan los perfiles que contienen registros de perfil. |
| `additionalFields.eventList` | Controla los campos de eventos de series temporales exportados para los objetos secundarios o asociados proporcionando una o más de las siguientes configuraciones:<ul><li>`fields`: controle los campos que desea exportar.</li><li>`filter`: especifica criterios que limitan los resultados incluidos en los objetos asociados. Espera un valor mínimo requerido para la exportación, normalmente una fecha.</li><li>`filter.fromIngestTimestamp`: filtra los eventos de series temporales a los que se han introducido después de la marca de tiempo proporcionada. No es la hora del evento en sí, sino la hora de ingesta de los eventos.</li><li>`filter.toIngestTimestamp`: filtra la marca de tiempo a aquellas que se han introducido antes de la marca de tiempo proporcionada. No es la hora del evento en sí, sino la hora de ingesta de los eventos.</li></ul> |
| `destination` | **(obligatorio)** Información sobre los datos exportados:<ul><li>`datasetId`: **(obligatorio)** ID del conjunto de datos donde se exportarán los datos.</li><li>`segmentPerBatch`: *(Opcional)* Un valor booleano que, si no se proporciona, toma el valor predeterminado &quot;false&quot;. El valor &quot;false&quot; exporta todos los ID de segmento a un único ID de lote. El valor &quot;true&quot; exporta un ID de segmento a un ID de lote. Tenga en cuenta que configurar el valor como &quot;true&quot; puede afectar al rendimiento de la exportación por lotes.</li></ul> |
| `schema.name` | **(Obligatorio)** El nombre del esquema asociado con el conjunto de datos donde se exportarán los datos. |
| `evaluationInfo.segmentation` | *(opcional)* Un valor booleano que, si no se proporciona, toma el valor predeterminado `false`. El valor `true` indica que es necesario realizar la segmentación en el trabajo de exportación. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del trabajo de exportación recién creado.

+++ Una respuesta de ejemplo al crear un trabajo de exportación.

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
    "imsOrgId": "{ORG_ID}",
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
| `id` | Un valor de solo lectura generado por el sistema que identifica el trabajo de exportación que se acaba de crear. |

Alternativamente, si `destination.segmentPerBatch` se hubiera establecido en `true`, el objeto `destination` de arriba tendría una matriz `batches`, como se muestra a continuación:

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
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

+++

## Recuperación de un trabajo de exportación específico {#get}

Puede recuperar información detallada sobre un trabajo de exportación específico realizando una solicitud al extremo `/export/jobs` y proporcionando el ID del trabajo de GET que desea recuperar en la ruta de solicitud.

**Formato de API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` del trabajo de exportación al que desea acceder. |

**Solicitud**

+++ Una solicitud de ejemplo para recuperar un trabajo de exportación.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el trabajo de exportación especificado.

+++ Una respuesta de ejemplo al recuperar un trabajo de exportación.

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
    "imsOrgId": "{ORG_ID}",
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
| `destination` | Información de destino para los datos exportados:<ul><li>`datasetId`: ID del conjunto de datos donde se exportaron los datos.</li><li>`segmentPerBatch`: Valor booleano que muestra si los ID de segmento están consolidados o no. Un valor de `false` significa que todos los ID de segmento estaban en un único ID de lote. Un valor de `true` significa que se exporta un ID de segmento a un ID de lote.</li></ul> |
| `fields` | Una lista de los campos exportados, separados por comas. |
| `schema.name` | Nombre del esquema asociado al conjunto de datos donde se exportarán los datos. |
| `filter.segments` | Los segmentos que se exportan. Se incluyen los siguientes campos:<ul><li>`segmentId`: ID del segmento para los perfiles que se van a exportar.</li><li>`segmentNs`: área de nombres de segmento para el objeto `segmentID` dado.</li><li>`status`: matriz de cadenas que proporciona un filtro de estado para `segmentID`. De manera predeterminada, `status` tendrá el valor `["realized"]`, que representa todos los perfiles que pertenecen al segmento en el momento actual. Los valores posibles incluyen: `realized` y `exited`.  Un valor de `realized` significa que el perfil califica para el segmento. Un valor de `exiting` significa que el perfil está saliendo del segmento.</li></ul> |
| `mergePolicy` | Combinar información de directivas para los datos exportados. |
| `metrics.totalTime` | Campo que indica el tiempo total que tardó en ejecutarse el trabajo de exportación. |
| `metrics.profileExportTime` | Campo que indica el tiempo que tardan los perfiles en exportar. |
| `totalExportedProfileCounter` | Número total de perfiles exportados en todos los lotes. |

+++

## Cancelar o eliminar un trabajo de exportación específico {#delete}

Puede solicitar que se elimine el trabajo de exportación especificado realizando una solicitud de DELETE al extremo `/export/jobs` y proporcionando el identificador del trabajo de exportación que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | El `id` del trabajo de exportación que desea eliminar. |

**Solicitud**

+++ Una solicitud de ejemplo para eliminar un trabajo de exportación.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 con el siguiente mensaje:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Pasos siguientes

Después de leer esta guía, ahora tiene una mejor comprensión de cómo funcionan los trabajos de exportación.
