---
keywords: Experience Platform;home;popular topics;data ingestion;batch;Batch;enable dataset;Batch ingestion overview;overview;batch ingestion overview;
solution: Experience Platform
title: Introducción a la ingestión de lotes
topic: overview
description: La API de inserción por lotes permite ingestar datos en Adobe Experience Platform como archivos por lotes. Los datos que se están ingeriendo pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo de parqué) o los datos que se ajustan a un esquema conocido en el registro del Modelo de datos de experiencia (XDM).
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 2%

---


# [!DNL Batch Ingestion]sobre validación

La [!DNL Batch Ingestion] API permite ingerir datos en Adobe Experience Platform como archivos por lotes. Los datos que se ingieren pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo de parqué) o los datos que se ajustan a un esquema conocido en el registro [!DNL Experience Data Model] (XDM).

La referencia [de la API de inserción de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) datos proporciona información adicional sobre estas llamadas de API.

El diagrama siguiente describe el proceso de ingestión por lotes:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Uso de la API

La [!DNL Data Ingestion] API le permite ingerir datos como lotes (una unidad de datos que consta de uno o más archivos que se van a ingerir como una sola unidad) [!DNL Experience Platform] en tres pasos básicos:

1. Crear un nuevo lote.
2. Cargue archivos en un conjunto de datos especificado que coincida con el esquema XDM de los datos.
3. Señale el final del lote.


### [!DNL Data Ingestion] requisitos previos

- Los datos que se van a cargar deben estar en los formatos Parquet o JSON.
- Un conjunto de datos creado en el [[!DNL Catalog services]](../../catalog/home.md).
- El contenido del archivo de parqué debe coincidir con un subconjunto del esquema del conjunto de datos que se está cargando en.
- Tenga su Token de acceso único después de la autenticación.

### Prácticas recomendadas de ingestión por lotes

- El tamaño de lote recomendado está entre 256 MB y 100 GB.
- Cada lote debe contener como máximo 1500 archivos.

Para cargar un archivo de más de 512 MB, el archivo deberá dividirse en partes más pequeñas. Las instrucciones para cargar un archivo grande se pueden encontrar [aquí](#large-file-upload---create-file).

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

### Crear un lote

Antes de agregar datos a un conjunto de datos, debe vincularse a un lote, que luego se cargará en un conjunto de datos especificado.

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `datasetId` | ID del conjunto de datos en el que se cargarán los archivos. |

**Respuesta**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | ID del lote que se acaba de crear (se utiliza en solicitudes posteriores). |
| `relatedObjects.id` | ID del conjunto de datos en el que se cargarán los archivos. |

## Carga de archivos

Después de crear correctamente un nuevo lote para la carga, los archivos se pueden cargar a un conjunto de datos específico.

Puede cargar archivos con la API de carga de archivos pequeños. Sin embargo, si los archivos son demasiado grandes y se supera el límite de la puerta de enlace (como tiempos de espera extendidos, solicitudes de tamaño de cuerpo excedidos y otras restricciones), puede cambiar a la API de carga de archivos grandes. Esta API carga el archivo en fragmentos y vincula los datos mediante la llamada API Large File Upload Complete.

>[!NOTE]
>
>Los ejemplos siguientes utilizan el formato de archivo [parquet](https://parquet.apache.org/documentation/latest/) . Encontrará un ejemplo que utiliza el formato de archivo JSON en la guía para desarrolladores de [ingestión por lotes](./api-overview.md).

### Carga de archivos pequeña

Una vez creado el lote, los datos se pueden cargar en un conjunto de datos preexistente.  El archivo que se está cargando debe coincidir con el esquema XDM al que hace referencia.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote. |
| `{DATASET_ID}` | ID del conjunto de datos para cargar archivos. |
| `{FILE_NAME}` | Nombre del archivo tal como se verá en el conjunto de datos. |

**Solicitud**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta y nombre de archivo del archivo que se va a cargar en el conjunto de datos. |

**Respuesta**

```JSON
#Status 200 OK, with empty response body
```

### Carga de archivos grande: crear archivo

Para cargar un archivo de gran tamaño, el archivo debe dividirse en fragmentos más pequeños y cargarse de uno en uno.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote. |
| `{DATASET_ID}` | ID del conjunto de datos que ingesta los archivos. |
| `{FILE_NAME}` | Nombre del archivo tal como se verá en el conjunto de datos. |

**Solicitud**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

```JSON
#Status 201 CREATED, with empty response body
```

### Carga de archivos grande: carga de partes subsiguientes

Una vez creado el archivo, todos los fragmentos posteriores se pueden cargar realizando solicitudes repetidas de PATCH, una para cada sección del archivo.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote. |
| `{DATASET_ID}` | ID del conjunto de datos en el que se cargarán los archivos. |
| `{FILE_NAME}` | Nombre del archivo tal como se verá en el conjunto de datos. |

**Solicitud**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta y nombre de archivo del archivo que se va a cargar en el conjunto de datos. |

**Respuesta**

```JSON
#Status 200 OK, with empty response
```

## Finalización del lote de señales

Una vez cargados todos los archivos en el lote, se puede indicar la finalización del lote. Al hacer esto, las entradas [!DNL Catalog] DataSetFile se crean para los archivos completados y se asocian al lote generado anteriormente. A continuación, el [!DNL Catalog] lote se marca como correcto, lo que desencadena flujos descendentes para ingestar los datos disponibles.

**Solicitud**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote que se va a cargar en el conjunto de datos. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Respuesta**

```JSON
#Status 200 OK, with empty response
```

## Comprobar estado de lote

Mientras esperan a que los archivos se carguen en el lote, se puede comprobar el estado del lote para ver su progreso.

**Formato API**

```http
GET /batch/{BATCH_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote que se está comprobando. |

**Solicitud**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{USER_ID}` | ID del usuario que creó o actualizó el lote. |

El `"status"` campo muestra el estado actual del lote solicitado. Los lotes pueden tener uno de los siguientes estados:

## Estado de ingestión de lotes

| Estado | Descripción |
| ------ | ----------- |
| Abandonado | El lote no se completó en el intervalo de tiempo esperado. |
| Anulado | Se ha llamado **explícitamente** a una operación de anulación (mediante la API de Ingesta por lotes) para el lote especificado. Una vez que el lote está en estado &quot;Cargado&quot;, no se puede anular. |
| Activo | El lote se ha promocionado correctamente y está disponible para el consumo de flujo descendente. Este estado se puede utilizar de forma intercambiable con &quot;Éxito&quot;. |
| Eliminado | Se han eliminado completamente los datos del lote. |
| Fallido | Estado de terminal que resulta de una configuración incorrecta o de datos incorrectos. Los datos de un lote fallido **no se mostrarán** . Este estado se puede utilizar de forma intercambiable con &quot;Error&quot;. |
| Inactivo | El lote se promocionó correctamente, pero se ha revertido o ha caducado. El lote ya no está disponible para el consumo descendente. |
| Cargado | Los datos del lote se han completado y el lote está listo para la promoción. |
| Cargando | Los datos de este lote se están cargando y el lote **no está** listo para promocionarse. |
| Reintentar | Se están procesando los datos de este lote. Sin embargo, debido a un error de sistema o transitorio, el lote falló; como resultado, este lote se está reintentando. |
| En etapas | Se ha completado la fase de ensayo del proceso de promoción de un lote y se ha ejecutado el trabajo de inserción. |
| Ensayo | Se están procesando los datos del lote. |
| Detenido | Se están procesando los datos del lote. Sin embargo, la promoción por lotes se ha estancado después de varios reintentos. |