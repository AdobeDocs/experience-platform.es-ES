---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 'Trabajos de exportación: API de Perfil del cliente en tiempo real'
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 2%

---


# Extremo de trabajos de exportación

[!DNL Real-time Customer Profile] le permite crear una sola vista de clientes individuales al reunir datos de varias fuentes, incluidos datos de atributos y datos de comportamiento. Los datos disponibles dentro de [!DNL Profile] se pueden exportar a un conjunto de datos para su posterior procesamiento. Por ejemplo, los segmentos de audiencia de [!DNL Profile] datos se pueden exportar para su activación y los atributos de perfil se pueden exportar para su sistema de informes.

Este documento proporciona instrucciones paso a paso para crear y administrar trabajos de exportación mediante la API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)Perfil.

>[!NOTE]
>
>Esta guía cubre el uso de trabajos de exportación en el [!DNL Profile API]. Para obtener información sobre cómo administrar los trabajos de exportación para el servicio de segmentación de Adobe Experience Platform, consulte la guía sobre los trabajos de [exportación en la API](../../profile/api/export-jobs.md)de segmentación.

Además de crear un trabajo de exportación, también puede acceder a [!DNL Profile] los datos mediante el `/entities` punto final, también conocido como &quot;[!DNL Profile Access]&quot;. See the [entities endpoint guide](./entities.md) for more information. Para ver los pasos sobre cómo acceder a [!DNL Profile] los datos mediante la interfaz de usuario, consulte la guía [del](../ui/user-guide.md)usuario.

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte de la [!DNL Real-time Customer Profile] API. Antes de continuar, consulte la guía [de](getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Crear un trabajo de exportación

La exportación [!DNL Profile] de datos requiere primero crear un conjunto de datos en el que se exportarán los datos y, a continuación, iniciar un nuevo trabajo de exportación. Estos dos pasos se pueden realizar mediante API de Experience Platform, mientras que el primero utiliza la API de servicio de catálogo y el segundo utiliza la API de Perfil de cliente en tiempo real. Las instrucciones detalladas para completar cada paso se describen en las secciones siguientes.

### Creación de un conjunto de datos de destinatario

Al exportar [!DNL Profile] datos, primero se debe crear un conjunto de datos de destinatario. Es importante que el conjunto de datos se configure correctamente para garantizar que la exportación se realiza correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de muestra de API que se muestra a continuación). Para exportar datos de perfil, el conjunto de datos debe basarse en el Esquema de [!DNL XDM Individual Profile] Unión (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de sólo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase. En este caso, esa es la [!DNL XDM Individual Profile] clase. Para obtener más información sobre los esquemas de vista de unión, consulte la sección de [unión en los conceptos básicos de la guía](../../xdm/schema/composition.md#union)de composición de esquemas.

Los pasos siguientes en este tutorial describen cómo crear un conjunto de datos que haga referencia al Esquema de [!DNL XDM Individual Profile] Unión mediante la [!DNL Catalog] API. También puede utilizar la interfaz de usuario para crear un conjunto de datos que haga referencia al esquema de unión. [!DNL Platform] Los pasos para utilizar la interfaz de usuario se describen en [este tutorial de la interfaz de usuario para exportar segmentos](../../segmentation/tutorials/create-dataset-export-segment.md) , pero también se pueden aplicar aquí. Una vez completado, puede volver a este tutorial para continuar con los pasos para [iniciar un nuevo trabajo](#initiate)de exportación.

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso para [iniciar un nuevo trabajo](#initiate)de exportación.

**Formato API**

```http
POST /dataSets
```

**Solicitud**

La siguiente solicitud crea un nuevo conjunto de datos, que proporciona parámetros de configuración en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        }
      }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre descriptivo para el conjunto de datos. |
| `schemaRef.id` | ID de la vista de unión (esquema) con la que se asociará el conjunto de datos. |
| `fileDescription.persisted` | Un valor booleano que cuando se establece en `true`, permite que el conjunto de datos persista en la vista de unión. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene la ID única, generada por el sistema y de sólo lectura del conjunto de datos recién creado. Se requiere un ID de conjunto de datos configurado correctamente para exportar correctamente los datos de Perfil.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Iniciar trabajo de exportación {#initiate}

Una vez que tenga un conjunto de datos que mantenga la unión, puede crear un trabajo de exportación para conservar los datos de Perfil en el conjunto de datos realizando una solicitud de POST al extremo en la API de Perfil de cliente en tiempo real y proporcionando los detalles de los datos que desea exportar en el cuerpo de la solicitud. `/export/jobs`

**Formato API**

```http
POST /export/jobs
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de exportación, proporcionando parámetros de configuración en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| Propiedad | Descripción |
| -------- | ----------- |
| `fields` | *(Opcional)* Limita los campos de datos que se van a incluir en la exportación solo a los proporcionados en este parámetro. Si se omite este valor, todos los campos se incluirán en los datos exportados. |
| `mergePolicy` | *(Opcional)* Especifica la directiva de combinación que regirá los datos exportados. Incluya este parámetro cuando se exporten varios segmentos. |
| `mergePolicy.id` | ID de la directiva de combinación. |
| `mergePolicy.version` | Versión específica de la directiva de combinación que se va a utilizar. Si se omite este valor, se pasará de forma predeterminada a la versión más reciente. |
| `additionalFields.eventList` | *(Opcional)* Controla los campos de evento de la serie temporal exportados para objetos secundarios o asociados proporcionando una o varias de las siguientes opciones de configuración:<ul><li>`eventList.fields`:: Controle los campos que desea exportar.</li><li>`eventList.filter`:: Especifica criterios que limitan los resultados incluidos de los objetos asociados. Espera un valor mínimo necesario para la exportación, normalmente una fecha.</li><li>`eventList.filter.fromIngestTimestamp`:: Filtros eventos de series temporales a los que se han ingerido después de la marca de tiempo proporcionada. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos.</li></ul> |
| `destination` | **(Requerido)** Información de destino de los datos exportados:<ul><li>`destination.datasetId`:: **(Requerido)** El ID del conjunto de datos en el que se exportan los datos.</li><li>`destination.segmentPerBatch`:: *(Opcional)* Un valor booleano que, si no se proporciona, toma como valor predeterminado `false`. Un valor de `false` exporta todos los ID de segmento en un único ID de lote. Un valor de `true` exporta un ID de segmento en un ID de lote. Tenga en cuenta que la configuración del valor que se va a definir `true` puede afectar al rendimiento de exportación de lotes.</li></ul> |
| `schema.name` | **(Requerido)** El nombre del esquema asociado con el conjunto de datos donde se exportan los datos. |

>[!NOTE]
>
>Para exportar solo datos de Perfil y no incluir datos de series temporales relacionados, elimine el objeto &quot;extraFields&quot; de la solicitud.

**Respuesta**

Una respuesta correcta devuelve un conjunto de datos rellenado con datos de Perfil como se especifica en la solicitud.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## Lista de todos los trabajos de exportación

Puede devolver una lista de todos los trabajos de exportación para una organización IMS concreta realizando una solicitud de GET al `export/jobs` extremo. La solicitud también admite los parámetros de consulta `limit` y `offset`, como se muestra a continuación.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `start` | Desplaza la página de resultados devueltos, según la hora de creación de la solicitud. Ejemplo: `start=4` |
| `limit` | Limite el número de resultados devueltos. Ejemplo: `limit=10` |
| `page` | Devolver una página específica de resultados, según la hora de creación de la solicitud. Ejemplo: `page=2` |
| `sort` | Ordenar los resultados por un campo específico en orden ascendente ( **`asc`** ) o descendente ( **`desc`** ). El parámetro de ordenación no funciona cuando se devuelven varias páginas de resultados. Ejemplo: `sort=updateTime:asc` |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

La respuesta incluye un `records` objeto que contiene los trabajos de exportación creados por la organización de IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
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
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
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
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## Monitorear el progreso de exportación

Para realizar una vista de los detalles de un trabajo de exportación específico o supervisar su estado a medida que se procesa, puede realizar una solicitud de GET al `/export/jobs` extremo e incluir el `id` del trabajo de exportación en la ruta. El trabajo de exportación se completa una vez que el `status` campo devuelve el valor &quot;SUCCEEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | El `id` del trabajo de exportación al que desea acceder. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `batchId` | El identificador de los lotes creados a partir de una exportación correcta, que se utilizará con fines de búsqueda al leer datos de Perfil. |

## Cancelar un trabajo de exportación

Experience Platform le permite cancelar un trabajo de exportación existente, lo que puede resultar útil por varios motivos, como si el trabajo de exportación no se completó o se quedó atascado en la fase de procesamiento. Para cancelar un trabajo de exportación, puede realizar una solicitud de DELETE al extremo e incluir el trabajo `/export/jobs` `id` de exportación que desea cancelar en la ruta de la solicitud.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | El `id` del trabajo de exportación al que desea acceder. |

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una solicitud de eliminación correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo de respuesta vacío, lo que indica que la operación de cancelación se realizó correctamente.

## Pasos siguientes

Una vez que la exportación se haya completado correctamente, los datos estarán disponibles en el Experience Platform Data Lake. A continuación, puede utilizar la API [de acceso a](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) datos para acceder a los datos mediante el `batchId` vínculo asociado a la exportación. Según el tamaño de la exportación, los datos pueden estar en trozos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso sobre cómo utilizar la API de acceso a datos para acceder y descargar archivos por lotes, siga el tutorial [de acceso a](../../data-access/tutorials/dataset-data.md)datos.

También puede acceder a los datos de Perfil de cliente en tiempo real exportados correctamente mediante el servicio de Consulta de Adobe Experience Platform. El servicio de Consulta, que utiliza la interfaz de usuario o la API RESTful, le permite escribir, validar y ejecutar consultas en los datos dentro de Data Lake.

Para obtener más información sobre cómo consulta de datos de audiencia, consulte la documentación [del servicio de](../../query-service/home.md)Consulta.

## Apéndice

La siguiente sección contiene información adicional sobre los trabajos de exportación en la API de Perfil.

### Ejemplos de carga útil de exportación adicionales

La llamada a la API de ejemplo que se muestra en la sección sobre el [inicio de un trabajo](#initiate) de exportación crea un trabajo que contiene datos de perfil (registro) y de evento (serie temporal). En esta sección se proporcionan ejemplos de carga útil de solicitud adicionales para limitar la exportación a fin de que contenga un tipo de datos o el otro.

La siguiente carga útil crea un trabajo de exportación que solo contiene datos de perfil (sin eventos):

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

Para crear un trabajo de exportación que solo contenga datos de evento (sin atributos de perfil), la carga útil puede tener un aspecto similar al siguiente:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### Exportación de segmentos

También puede utilizar el extremo de trabajos de exportación para exportar segmentos de audiencia en lugar de [!DNL Profile] datos. Consulte la guía sobre los trabajos de [exportación en la API](../../segmentation/api/export-jobs.md) de segmentación para obtener más información.