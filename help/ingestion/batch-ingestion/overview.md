---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;lote;habilitar conjunto de datos;información general sobre ingesta por lotes;información general;información general sobre ingesta por lotes
solution: Experience Platform
title: Información general sobre la ingesta de lotes
topic-legacy: overview
description: La API de ingesta de datos de Adobe Experience Platform le permite introducir datos en Platform como archivos por lotes. Los datos introducidos pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo Parquet) o los datos que se ajustan a un esquema conocido en el registro del Modelo de datos de experiencia (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 2%

---

# Información general sobre la ingesta por lotes

La API de ingesta de datos de Adobe Experience Platform le permite introducir datos en Platform como archivos por lotes. Los datos introducidos pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo Parquet) o los datos que se ajustan a un esquema conocido en el registro [!DNL Experience Data Model] (XDM).

La [referencia de la API de ingesta de datos](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) proporciona información adicional sobre estas llamadas a la API.

El diagrama siguiente describe el proceso de ingesta por lotes:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Uso de la API

La API [!DNL Data Ingestion] permite introducir datos como lotes (una unidad de datos que consta de uno o más archivos que se van a introducir como una sola unidad) en [!DNL Experience Platform] en tres pasos básicos:

1. Cree un nuevo lote.
2. Cargue archivos a un conjunto de datos especificado que coincida con el esquema XDM de los datos.
3. Indica el final del lote.


### [!DNL Data Ingestion] requisitos previos

- Los datos que se van a cargar deben estar en los formatos Parquet o JSON.
- Un conjunto de datos creado en [[!DNL Catalog services]](../../catalog/home.md).
- El contenido del archivo de parquet debe coincidir con un subconjunto del esquema del conjunto de datos que se está cargando en.
- Tenga su token de acceso único después de la autenticación.

### Prácticas recomendadas sobre la ingesta por lotes

- El tamaño recomendado del lote está entre 256 MB y 100 GB.
- Cada lote debe contener como máximo 1500 archivos.

Para cargar un archivo de más de 512 MB, el archivo deberá dividirse en trozos más pequeños. Las instrucciones para cargar un archivo grande se encuentran [aquí](#large-file-upload---create-file).

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

### Crear un lote

Para poder agregar datos a un conjunto de datos, estos deben vincularse a un lote que luego se cargará en un conjunto de datos especificado.

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
| `datasetId` | El ID del conjunto de datos en el que se cargarán los archivos. |

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
| `id` | El ID del lote que se acaba de crear (se utiliza en solicitudes posteriores). |
| `relatedObjects.id` | El ID del conjunto de datos en el que se cargarán los archivos. |

## Carga de archivos

Después de crear correctamente un nuevo lote para su carga, los archivos se pueden cargar en un conjunto de datos específico.

Puede cargar archivos mediante la API de carga de archivos pequeños. Sin embargo, si los archivos son demasiado grandes y se supera el límite de la puerta de enlace (como los tiempos de espera extendidos, las solicitudes de tamaño de cuerpo excedidos y otras restricciones), puede cambiar a la API de carga de archivos grandes. Esta API carga el archivo en fragmentos y vincula los datos mediante la llamada API de finalización de carga de archivos grandes.

>[!NOTE]
>
>Los ejemplos siguientes utilizan el formato de archivo [Apache Parquet](https://parquet.apache.org/documentation/latest/). Puede encontrar un ejemplo que use el formato de archivo JSON en la [guía para desarrolladores de ingesta por lotes](./api-overview.md).

### Carga de archivo pequeño

Una vez creado un lote, los datos se pueden cargar en un conjunto de datos preexistente.  El archivo que se está cargando debe coincidir con su esquema XDM al que se hace referencia.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote. |
| `{DATASET_ID}` | ID del conjunto de datos para cargar archivos. |
| `{FILE_NAME}` | El nombre del archivo tal como se verá en el conjunto de datos. |

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

### Carga de archivo grande: crear archivo

Para cargar un archivo grande, el archivo debe dividirse en fragmentos más pequeños y cargarse de uno en uno.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote. |
| `{DATASET_ID}` | ID del conjunto de datos que incorpora los archivos. |
| `{FILE_NAME}` | El nombre del archivo tal como se verá en el conjunto de datos. |

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

### Carga de archivos grande: cargue las partes siguientes

Una vez creado el archivo, todos los fragmentos posteriores se pueden cargar realizando solicitudes de PATCH repetidas, una para cada sección del archivo.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote. |
| `{DATASET_ID}` | El ID del conjunto de datos en el que se cargarán los archivos. |
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

Una vez cargados todos los archivos en el lote, se puede indicar que el lote ha finalizado. Al hacerlo, las entradas [!DNL Catalog] DataSetFile se crean para los archivos completados y se asocian al lote generado anteriormente. El lote [!DNL Catalog] se marca como correcto, lo que déclencheur los flujos descendentes para introducir los datos disponibles.

**Solicitud**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que se cargará en el conjunto de datos. |

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

## Comprobar el estado del lote

Mientras esperan que los archivos se carguen en el lote, se puede comprobar el estado del lote para ver su progreso.

**Formato de API**

```http
GET /batch/{BATCH_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que se está comprobando. |

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

El campo `"status"` es lo que muestra el estado actual del lote solicitado. Los lotes pueden tener uno de los siguientes estados:

## Estados de ingesta por lotes

| Estado | Descripción |
| ------ | ----------- |
| Abandonado | El lote no se ha completado en el intervalo de tiempo esperado. |
| Anulado | Se ha llamado a una operación de anulación **explícitamente** (a través de la API de ingesta de lotes) para el lote especificado. Una vez que el lote está en estado &quot;Loaded&quot;, no se puede anular. |
| Activo | El lote se ha promocionado correctamente y está disponible para el consumo descendente. Este estado se puede utilizar de forma intercambiable con &quot;Success&quot;. |
| Eliminado | Los datos del lote se han eliminado por completo. |
| Fallido | Estado de terminal que resulta de una configuración incorrecta o de datos incorrectos. Los datos de un lote fallido **no** aparecerán. Este estado se puede utilizar de forma intercambiable con &quot;Fallo&quot;. |
| Inactivo | El lote se promocionó correctamente, pero se ha revertido o ha caducado. El lote ya no está disponible para el consumo descendente. |
| Cargado | Los datos del lote se completan y el lote está listo para su promoción. |
| Carga | Los datos de este lote se están cargando y el lote está **no** listo para su promoción. |
| Reintentando | Se están procesando los datos de este lote. Sin embargo, debido a un error del sistema o transitorio, el lote falló, por lo que se está reintentando este lote. |
| Ensayo | La fase de ensayo del proceso de promoción de un lote se ha completado y el trabajo de ingesta se ha ejecutado. |
| Ensayo | Se están procesando los datos del lote. |
| Estancado | Se están procesando los datos del lote. Sin embargo, la promoción por lotes se ha estancado después de varios reintentos. |
