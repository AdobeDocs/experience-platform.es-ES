---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Trabajos de exportación
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# Trabajos de exportación

intro

- Recuperar una lista de trabajos de exportación
- Crear un nuevo trabajo de exportación
- Recuperar un trabajo de exportación específico
- Cancelar o eliminar un trabajo de exportación específico

## Primeros pasos

Los extremos de API que se utilizan en esta guía forman parte de la API de segmentación. Antes de continuar, consulte la guía para desarrolladores [de Segmentación](./getting-started.md).

En particular, la sección [de](./getting-started.md#getting-started) introducción de la guía para desarrolladores de Segmentación incluye vínculos a temas relacionados, una guía para leer las llamadas de la API de muestra en el documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas exitosas a cualquier API de la plataforma de experiencia.

## Recuperar una lista de trabajos de exportación

Puede recuperar una lista de todos los trabajos de exportación para su organización de IMS mediante una solicitud GET al `/export/jobs` extremo.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:: (*Opcional*) Se han agregado parámetros a la ruta de solicitud que configuran los resultados devueltos en la respuesta. Se pueden incluir varios parámetros, separados por ampersands (`&`). Los parámetros disponibles se enumeran a continuación.

**Parámetros de Consulta**

A continuación se muestra una lista de los parámetros de consulta disponibles para enumerar los trabajos de exportación. Todos estos parámetros son opcionales. Al realizar una llamada a este extremo sin parámetros, se recuperarán todos los trabajos de exportación disponibles para su organización.

| Parámetro | Descripción |
| --------- | ----------- |
| `limit` | Especifica el número de trabajos de exportación devueltos. |
| `offset` | Especifica el desplazamiento de las páginas de resultados. |
| `status` | Filtros los resultados en función del estado. Los valores admitidos son `NEW`, `SUCCEEDED`y `FAILED`. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de trabajos de exportación para la organización de IMS especificada como JSON. La siguiente respuesta devuelve una lista de todos los trabajos de exportación correctos para la organización de IMS.

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
        "batches": {
          "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
          "segmentNs": "ups",
          "status": [
            "realized"
          ],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        }
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
            "fromIngestTimestamp": "2018-01-01T00:00:00Z"
          }
        }
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
        "aCPDatasetWriteTime": {
          "startTimeInMs": 123456789000,
          "endTimeInMs": 123456799000,
          "totalTimeInMs": 10000
        }
      },
      "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
        "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "creationTime": 1538615973895,
      "updateTime": 1538616233239,
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
    }
  ],
  "page": {
    "sortField": "createdTime",
    "sort": "desc",
    "pageOffset": "1540974701302_96",
    "pageSize": 10
  },
  "link": {
    "next": "string"
  }
}
```

## Crear un nuevo trabajo de exportación

Puede crear un nuevo trabajo de exportación realizando una solicitud POST al `/export/jobs` extremo.

**Formato API**

```http
POST /export/jobs
```

**Solicitud**

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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
  },
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df"
  },
  "schema": {
    "name": "_xdm.context.profile"
  }
 }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `fields` | Opcional. lista de los campos exportados, separados por comas. Si se deja en blanco, se exportarán todos los campos. |
| `mergePolicy` | Opcional. Si no se proporciona, la exportación tendrá la misma directiva de combinación que el segmento dado. |
| `filter` | Opcional. Si se deja en blanco, se exportarán todos los datos. |
| `filter.segments` | Opcional. filtros de segmento para el trabajo de exportación. |
| `filter.segmentQualificationTime` | Opcional. Un filtro para el tiempo de calificación del segmento. Se puede proporcionar el inicio y/o la hora de finalización. |
| `filter.fromIngestTimestamp` | Opcional. Marca de hora con formato RFC-3339. |
| `destination.datasetId` | Requerido. El `id` valor del conjunto de datos al que se exportan los datos. |
| `segments.segmentId` | Requerido. El `id` valor del segmento que se está exportando. |
| `segments.sgementNs` | Opcional. El `namespace` para el segmento dado. |



**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del trabajo de exportación recién creado.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## Recuperar un trabajo de exportación específico

Puede recuperar información detallada sobre un trabajo de exportación específico realizando una solicitud GET al extremo y proporcionando el valor del trabajo de exportación en la ruta de acceso de la solicitud `/export/jobs` y el valor `id` del trabajo de exportación.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`:: El `id` valor del trabajo de exportación que desea recuperar.

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el trabajo de exportación especificado.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## Cancelar o eliminar un trabajo de exportación específico

Puede solicitar la eliminación de un trabajo de exportación especificado realizando una solicitud ELIMINAR al extremo y proporcionando el valor del trabajo de exportación en la ruta de acceso de la solicitud `/export/jobs` `id` .

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`:: El `id` valor del trabajo de exportación que desea eliminar.

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el siguiente mensaje:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Pasos siguientes
