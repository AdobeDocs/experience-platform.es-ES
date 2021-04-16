---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Exportar extremo de API de trabajos
topic: guía
type: Documentation
description: El perfil del cliente en tiempo real le permite crear una sola vista de clientes individuales dentro de Adobe Experience Platform recopilando datos de varias fuentes, incluidos datos de atributos y datos de comportamiento. A continuación, los datos de perfil se pueden exportar a un conjunto de datos para su procesamiento posterior.
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 2%

---

# Exportar extremo de trabajos

[!DNL Real-time Customer Profile] le permite crear una sola vista de clientes individuales recopilando datos de varias fuentes, incluidos datos de atributos y datos de comportamiento. A continuación, los datos de perfil se pueden exportar a un conjunto de datos para su procesamiento posterior. Por ejemplo, los segmentos de audiencia de datos [!DNL Profile] se pueden exportar para su activación y los atributos de perfil se pueden exportar para la creación de informes.

Este documento proporciona instrucciones paso a paso para la creación y administración de trabajos de exportación mediante la [API de perfil](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

>[!NOTE]
>
>Esta guía cubre el uso de trabajos de exportación en [!DNL Profile API]. Para obtener información sobre cómo administrar los trabajos de exportación para el servicio de segmentación de Adobe Experience Platform, consulte la guía sobre [exportar trabajos en la API de segmentación](../../profile/api/export-jobs.md).

Además de crear un trabajo de exportación, también puede acceder a los datos [!DNL Profile] utilizando el extremo `/entities`, también conocido como &quot;[!DNL Profile Access]&quot;. Consulte la [guía de extremo de entidades](./entities.md) para obtener más información. Para ver los pasos sobre cómo acceder a los datos [!DNL Profile] mediante la interfaz de usuario, consulte la [guía del usuario](../ui/user-guide.md).

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte de la API [!DNL Real-time Customer Profile]. Antes de continuar, consulte la [guía de introducción](getting-started.md) para ver los vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas correctamente a cualquier API [!DNL Experience Platform].

## Creación de un trabajo de exportación

La exportación de datos [!DNL Profile] requiere primero la creación de un conjunto de datos en el que se exportan los datos y, a continuación, el inicio de un nuevo trabajo de exportación. Estos dos pasos se pueden lograr mediante las API de Experience Platform, mientras que el primero utiliza la API de servicio de catálogo y el segundo utiliza la API de perfil de cliente en tiempo real. Las instrucciones detalladas para completar cada paso se describen en las secciones siguientes.

### Creación de un conjunto de datos de destino

Al exportar datos [!DNL Profile], primero debe crearse un conjunto de datos de destino. Es importante que el conjunto de datos esté configurado correctamente para garantizar que la exportación se realice correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de muestra de API que aparece a continuación). Para exportar datos de perfil, el conjunto de datos debe basarse en el [!DNL XDM Individual Profile] Esquema de unión (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase. En este caso, es la clase [!DNL XDM Individual Profile]. Para obtener más información sobre los esquemas de vista de unión, consulte la sección [unión en la guía de composición de esquema](../../xdm/schema/composition.md#union).

Los pasos siguientes en este tutorial describen cómo crear un conjunto de datos que haga referencia al esquema de unión [!DNL XDM Individual Profile] mediante la API [!DNL Catalog]. También puede utilizar la interfaz de usuario [!DNL Platform] para crear un conjunto de datos que haga referencia al esquema de unión. Los pasos para utilizar la interfaz de usuario se describen en [este tutorial de interfaz de usuario para exportar segmentos](../../segmentation/tutorials/create-dataset-export-segment.md), pero también se pueden aplicar aquí. Una vez completado, puede volver a este tutorial para continuar con los pasos para [iniciar un nuevo trabajo de exportación](#initiate).

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso para [iniciar un nuevo trabajo de exportación](#initiate).

**Formato de API**

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
          "persisted": true
        }
      }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre descriptivo para el conjunto de datos. |
| `schemaRef.id` | El ID de la vista de unión (esquema) con la que se asociará el conjunto de datos. |
| `fileDescription.persisted` | Un valor booleano que, cuando se establece en `true`, permite que el conjunto de datos persista en la vista de unión. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID único de solo lectura, generado por el sistema y del conjunto de datos recién creado. Se requiere un ID de conjunto de datos configurado correctamente para exportar correctamente los datos de perfil.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Iniciar trabajo de exportación {#initiate}

Una vez que tenga un conjunto de datos que mantenga la unión, puede crear un trabajo de exportación para mantener los datos de perfil en el conjunto de datos realizando una solicitud de POST al extremo `/export/jobs` en la API de perfil del cliente en tiempo real y proporcionando los detalles de los datos que desea exportar en el cuerpo de la solicitud.

**Formato de API**

```http
POST /export/jobs
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de exportación, que proporciona parámetros de configuración en la carga útil.

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
| `fields` | *(Opcional)* Limita los campos de datos que se incluyen en la exportación solo a los proporcionados en este parámetro. Si se omite este valor, todos los campos se incluirán en los datos exportados. |
| `mergePolicy` | *(Opcional)* Especifica la directiva de combinación que debe regir los datos exportados. Incluya este parámetro cuando se exporten varios segmentos. |
| `mergePolicy.id` | El ID de la directiva de combinación. |
| `mergePolicy.version` | Versión específica de la directiva de combinación que se va a utilizar. Si se omite este valor, se pasará de forma predeterminada a la versión más reciente. |
| `additionalFields.eventList` | *(Opcional)* Controla los campos de evento de serie temporal exportados para objetos secundarios o asociados proporcionando una o más de las siguientes configuraciones:<ul><li>`eventList.fields`: Controle los campos que desea exportar.</li><li>`eventList.filter`: Especifica criterios que limitan los resultados incluidos de objetos asociados. Espera un valor mínimo necesario para la exportación, normalmente una fecha.</li><li>`eventList.filter.fromIngestTimestamp`: Filtra los eventos de series temporales a los que se han introducido después de la marca de tiempo proporcionada. No es la hora del evento en sí, sino la hora de ingesta de los eventos.</li></ul> |
| `destination` | **(Obligatorio)** Información de destino de los datos exportados:<ul><li>`destination.datasetId`:  **(Obligatorio)** El ID del conjunto de datos donde se exportan los datos.</li><li>`destination.segmentPerBatch`:  *(Opcional)* Un valor booleano que, si no se proporciona, toma el valor predeterminado  `false`. Un valor de `false` exporta todos los ID de segmento en un único ID de lote. Un valor de `true` exporta un ID de segmento en un ID de lote. Tenga en cuenta que establecer el valor en `true` puede afectar al rendimiento de la exportación por lotes.</li></ul> |
| `schema.name` | **(Obligatorio)** El nombre del esquema asociado con el conjunto de datos donde se exportan los datos. |

>[!NOTE]
>
>Para exportar solo datos de perfil y no incluir datos de series temporales relacionados, elimine el objeto &quot;additionalFields&quot; de la solicitud.

**Respuesta**

Una respuesta correcta devuelve un conjunto de datos rellenado con datos de perfil como se especifica en la solicitud.

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

## Enumerar todos los trabajos de exportación

Puede devolver una lista de todos los trabajos de exportación para una organización de IMS en particular realizando una solicitud de GET al extremo `export/jobs` . La solicitud también admite los parámetros de consulta `limit` y `offset`, como se muestra a continuación.

**Formato de API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `start` | Desplazar la página de resultados devueltos, según la hora de creación de la solicitud. Ejemplo: `start=4` |
| `limit` | Limite el número de resultados devueltos. Ejemplo: `limit=10` |
| `page` | Devolver una página específica de resultados, según la hora de creación de la solicitud. Ejemplo: `page=2` |
| `sort` | Ordene los resultados por un campo específico en orden ascendente ( **`asc`** ) o descendente ( **`desc`** ). El parámetro de ordenación no funciona cuando se devuelven varias páginas de resultados. Ejemplo: `sort=updateTime:asc` |

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

La respuesta incluye un objeto `records` que contiene los trabajos de exportación creados por su organización IMS.

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

## Monitorización del progreso de exportación

Para ver los detalles de un trabajo de exportación específico o monitorizar su estado a medida que se procesa, puede realizar una solicitud de GET al extremo `/export/jobs` e incluir el `id` del trabajo de exportación en la ruta. El trabajo de exportación se completa una vez que el campo `status` devuelve el valor &quot;SUCCEEDED&quot;.

**Formato de API**

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
| `batchId` | El identificador de los lotes creados a partir de una exportación correcta, que se utilizará con fines de búsqueda al leer datos de perfil. |

## Cancelar un trabajo de exportación

Experience Platform le permite cancelar un trabajo de exportación existente, lo que puede resultar útil por varios motivos, incluido si el trabajo de exportación no se completó o se quedó estancado en la fase de procesamiento. Para cancelar un trabajo de exportación, puede realizar una solicitud de DELETE al extremo `/export/jobs` e incluir el `id` del trabajo de exportación que desea cancelar en la ruta de solicitud.

**Formato de API**

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

Una vez finalizada correctamente la exportación, los datos están disponibles en el Experience Platform Data Lake . A continuación, puede utilizar la [API de acceso a datos](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) para acceder a los datos mediante la `batchId` asociada a la exportación. Según el tamaño de la exportación, los datos pueden estar en trozos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso sobre cómo utilizar la API de acceso a datos para acceder y descargar archivos por lotes, siga el [Tutorial de acceso a datos](../../data-access/tutorials/dataset-data.md).

También puede acceder a los datos del perfil del cliente en tiempo real exportados correctamente mediante el servicio de consulta de Adobe Experience Platform. Con la interfaz de usuario o la API de RESTful, el servicio de consulta le permite escribir, validar y ejecutar consultas sobre datos dentro del lago de datos.

Para obtener más información sobre cómo consultar los datos de audiencia, consulte la [documentación del servicio de consulta](../../query-service/home.md).

## Apéndice

La siguiente sección contiene información adicional sobre los trabajos de exportación en la API de perfil.

### Ejemplos de carga útil de exportación adicionales

La llamada de API de ejemplo que se muestra en la sección [inicio de un trabajo de exportación](#initiate) crea un trabajo que contiene datos de perfil (registro) y de evento (serie temporal). En esta sección se proporcionan ejemplos de carga útil de solicitud adicionales para limitar la exportación a fin de que contenga un tipo de datos o el otro.

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

También puede usar el extremo exportar trabajos para exportar segmentos de audiencia en lugar de datos de [!DNL Profile]. Consulte la guía sobre [trabajos de exportación en la API de segmentación](../../segmentation/api/export-jobs.md) para obtener más información.
