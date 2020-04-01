---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportación de datos mediante API
topic: tutorial
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# Exportación de datos de Perfil mediante API

El Perfil del cliente en tiempo real le permite crear una única vista de clientes individuales al reunir datos de múltiples fuentes, incluidos datos de atributos y datos de comportamiento. Los datos disponibles dentro de Perfil se pueden exportar a un conjunto de datos para su posterior procesamiento. Este tutorial proporciona instrucciones paso a paso para crear y administrar trabajos de exportación mediante la API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentación.

Además de crear un trabajo de exportación, también puede acceder a los datos de Perfil mediante la API de acceso a Perfil y mediante proyecciones. Consulte el tutorial [de la API de acceso a](../../profile/api/entities.md) Perfil o el tutorial sobre la [configuración de destinos y proyecciones](../../profile/api/edge-projections.md) de Edge para obtener más información sobre estos otros patrones de acceso.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que intervienen en el trabajo con datos de Perfil. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [Servicio](../home.md)de segmentación de la plataforma Adobe Experience: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
- [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Encabezados requeridos

Este tutorial también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar correctamente llamadas a las API de plataforma. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Crear un trabajo de exportación

La exportación de datos de Perfil requiere primero crear un conjunto de datos en el que se exportarán los datos y, a continuación, iniciar un nuevo trabajo de exportación. Estos dos pasos se pueden realizar mediante las API de la plataforma de experiencia; el primero utiliza la API del servicio de catálogo y el segundo utiliza la API de Perfil del cliente en tiempo real. Las instrucciones detalladas para completar cada paso se describen en las secciones siguientes.

- [Crear un conjunto de datos](#create-a-target-dataset) de destinatario: cree un conjunto de datos para retener los datos exportados.
- [Iniciar un nuevo trabajo](#initiate-export-job) de exportación: Rellene el conjunto de datos con datos de Perfil individual XDM.

### Creación de un conjunto de datos de destinatario

Al exportar datos de Perfil, primero se debe crear un conjunto de datos de destinatario. Es importante que el conjunto de datos se configure correctamente para garantizar que la exportación se realiza correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de muestra de API que se muestra a continuación). Para exportar un segmento, el conjunto de datos debe basarse en el Esquema de Unión de Perfil individual XDM (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de sólo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase, en este caso la clase de Perfil individual XDM. Para obtener más información sobre los esquemas de vista de uniones, consulte la sección Perfil de clientes en tiempo [real de la guía](../../xdm/schema/composition.md#union)para desarrolladores de Esquema Registry.

Los pasos siguientes en este tutorial describen cómo crear un conjunto de datos que haga referencia al Esquema de Unión de Perfil individual XDM mediante la API de catálogo. También puede utilizar la interfaz de usuario de Adobe Experience Platform para crear un conjunto de datos que haga referencia al esquema de unión. Los pasos para utilizar la interfaz de usuario se describen en [este tutorial de la interfaz de usuario para exportar segmentos](./create-dataset-export-segment.md) , pero también se pueden aplicar aquí. Una vez completado, puede volver a este tutorial para continuar con los pasos para [iniciar un nuevo trabajo](#initiate-export-job)de exportación.

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso para [iniciar un nuevo trabajo](#initiate-export-job)de exportación.

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
        },
        "aspect": "production"
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

### Iniciar trabajo de exportación

Una vez que tenga un conjunto de datos que mantenga la unión, puede crear un trabajo de exportación para que los datos de Perfil se mantengan en el conjunto de datos realizando una solicitud POST al extremo en la API de Perfil del cliente en tiempo real y proporcionando los detalles de los datos que desea exportar en el cuerpo de la solicitud. `/export/jobs`

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
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
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `fields` | *(Opcional)* Limita los campos de datos que se van a incluir en la exportación solo a los proporcionados en este parámetro. El mismo parámetro también está disponible al crear un segmento, por lo que es posible que los campos del segmento ya se hayan filtrado. Si se omite este valor, todos los campos se incluirán en los datos exportados. |
| `mergePolicy` | *(Opcional)* Especifica la directiva de combinación que regirá los datos exportados. Incluya este parámetro cuando se exporten varios segmentos. Si se omite este valor, el servicio de exportación usará la directiva de combinación proporcionada por el segmento. |
| `mergePolicy.id` | ID de la directiva de combinación. |
| `mergePolicy.version` | Versión específica de la directiva de combinación que se va a utilizar. Si se omite este valor, se pasará de forma predeterminada a la versión más reciente. |
| `filter` | *(Opcional)* Especifica uno o varios de los siguientes filtros que se aplicarán al segmento antes de la exportación. |
| `filter.segments` | *(Opcional)* Especifica los segmentos que se van a exportar. Si se omite este valor, se exportarán todos los datos de todos los perfiles. Acepta una matriz de objetos de segmento, cada uno de los cuales contiene los campos siguientes:<ul><li>`segmentId`:: **(Necesario si se utiliza`segments`)** ID del segmento para la exportación de perfiles.</li><li>`segmentNs` *(Opcional)* Área de nombres de segmentos para el `segmentID`.</li><li>`status` *(Opcional)* Una matriz de cadenas que proporciona un filtro de estado para la `segmentID`. De forma predeterminada, `status` tendrá el valor `["realized", "existing"]` que representa todos los perfiles que entran en el segmento en el momento actual. Los valores posibles incluyen: `"realized"`, `"existing"`, y `"exited"`.</br></br>Para obtener más información, consulte el tutorial [sobre la](./create-a-segment.md)creación de segmentos.</li></ul> |
| `filter.segmentQualificationTime` | *(Opcional)* Filtre según el tiempo de calificación del segmento. Se puede proporcionar la hora de inicio y/o la hora de finalización. |
| `filter.segmentQualificationTime.startTime` | *(Opcional)* Tiempo de inicio de cualificación del segmento para un ID de segmento para un estado determinado. No se proporciona, no habrá ningún filtro en el tiempo de inicio para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Opcional)* Hora de finalización de la calificación del segmento para un ID de segmento para un estado determinado. No se proporciona, no habrá ningún filtro en la hora de finalización para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | *(Opcional)* Limita los perfiles exportados para incluir solo aquellos que se hayan actualizado después de esta marca de tiempo. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` en el caso de **perfiles**, en su caso: Incluye todos los perfiles combinados en los que la marca de tiempo actualizada combinada es buena que la marca de tiempo dada. Admite `greater_than` operando.</li><li>`fromTimestamp` para **eventos**: Todos los eventos ingeridos después de esta marca de tiempo se exportarán según el resultado de perfil resultante. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos.</li> |
| `filter.emptyProfiles` | *(Opcional)* Booleano. Los Perfiles pueden contener registros de Perfiles, registros de ExperienceEvent o ambos. Los Perfiles sin registros de Perfil y solo los registros de ExperienceEvent se denominan &quot;emptyProfiles&quot;. Para exportar todos los perfiles del almacén de Perfiles, incluido &quot;emptyProfiles&quot;, establezca el valor de `emptyProfiles` en `true`. Si `emptyProfiles` se establece en `false`, solo se exportan los perfiles con registros de Perfil en el almacén. De forma predeterminada, si no se incluye `emptyProfiles` el atributo, solo se exportan los perfiles que contienen registros de Perfil. |
| `additionalFields.eventList` | *(Opcional)* Controla los campos de evento de la serie temporal exportados para objetos secundarios o asociados proporcionando una o varias de las siguientes opciones de configuración:<ul><li>`eventList.fields`:: Controle los campos que desea exportar.</li><li>`eventList.filter`:: Especifica criterios que limitan los resultados incluidos de los objetos asociados. Espera un valor mínimo necesario para la exportación, normalmente una fecha.</li><li>`eventList.filter.fromIngestTimestamp`:: Filtros eventos de series temporales a los que se han ingerido después de la marca de tiempo proporcionada. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos.</li></ul> |
| `destination` | **(Requerido)** Información de destino de los datos exportados:<ul><li>`destination.datasetId`:: **(Requerido)** El ID del conjunto de datos donde se exportan los datos.</li><li>`destination.segmentPerBatch`:: *(Opcional)* Un valor booleano que, si no se proporciona, toma como valor predeterminado `false`. Un valor de `false` exporta todos los ID de segmento en un único ID de lote. Un valor de `true` exporta un ID de segmento en un ID de lote. Tenga en cuenta que la configuración del valor que se va a definir `true` puede afectar al rendimiento de exportación de lotes.</li></ul> |
| `schema.name` | **(Requerido)** El nombre del esquema asociado con el conjunto de datos donde se exportan los datos. |

>[!NOTE] Para exportar solo datos de Perfil y no incluir datos de ExperienceEvent relacionados, elimine el objeto &quot;extraFields&quot; de la solicitud.

**Respuesta**

Una respuesta correcta devuelve un conjunto de datos rellenado con datos de Perfil como se especifica en la solicitud.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Si no `destination.segmentPerBatch` se hubiera incluido en la solicitud (si no está presente, se establece de forma predeterminada en `false`) o el valor se hubiera establecido en `false`, el `destination` objeto de la respuesta anterior no tendría una `batches` matriz y, en su lugar, incluiría sólo una `batchId`, como se muestra a continuación. Ese único lote incluiría todos los ID de segmento, mientras que la respuesta anterior muestra un único ID de segmento por ID de lote.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## Lista de todos los trabajos de exportación

Puede devolver una lista de todos los trabajos de exportación para una organización IMS concreta realizando una solicitud GET al `export/jobs` extremo. La solicitud también admite los parámetros de consulta `limit` y `offset`, como se muestra a continuación.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Propiedad | Descripción |
| -------- | ----------- |
| `limit` | Especifique el número de registros que se van a devolver. |
| `offset` | Desplaza la página de resultados que devuelve el número proporcionado. |

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
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
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

Para realizar una vista de los detalles de un trabajo de exportación específico o supervisar su estado a medida que se procesa, puede realizar una solicitud GET al `/export/jobs` extremo e incluir el `id` del trabajo de exportación en la ruta. El trabajo de exportación se completa una vez que el `status` campo devuelve el valor &quot;SUCCEEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Propiedad | Descripción |
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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
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

La plataforma de experiencias permite cancelar un trabajo de exportación existente, lo que puede resultar útil por varios motivos, como si el trabajo de exportación no se completó o se quedó atascado en la fase de procesamiento. Para cancelar un trabajo de exportación, puede realizar una solicitud de ELIMINACIÓN al extremo e incluir el `/export/jobs` `id` del trabajo de exportación que desea cancelar en la ruta de la solicitud.

**Formato API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Propiedad | Descripción |
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

Una vez que la exportación se haya completado correctamente, los datos estarán disponibles en el lago de datos de la plataforma de experiencia. A continuación, puede utilizar la API [de acceso a](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) datos para acceder a los datos mediante el `batchId` vínculo asociado a la exportación. Según el tamaño de la exportación, los datos pueden estar en trozos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso sobre cómo utilizar la API de acceso a datos para acceder y descargar archivos por lotes, siga el tutorial [de acceso a](../../data-access/tutorials/dataset-data.md)datos.

También puede acceder a los datos de Perfil de cliente en tiempo real exportados correctamente mediante el servicio de Consulta de la plataforma Adobe Experience Platform. El servicio de Consulta, que utiliza la interfaz de usuario o la API RESTful, le permite escribir, validar y ejecutar consultas en los datos dentro de Data Lake.

Para obtener más información sobre cómo consulta de datos de audiencia, consulte la documentación [del servicio de](../../query-service/home.md)Consulta.