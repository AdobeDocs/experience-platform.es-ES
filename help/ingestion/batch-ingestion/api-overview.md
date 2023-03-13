---
keywords: Experience Platform;inicio;temas populares;ingesta por lotes;ingesta por lotes;ingesta;guía para desarrolladores;guía de api;cargar;ingesta de parquet;ingesta de json;
solution: Experience Platform
title: Guía API de ingesta por lotes
description: Este documento proporciona una guía completa para los desarrolladores que trabajan con las API de ingesta por lotes para Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 49281d6ef959c84c3da964f0a9e19859fd8901a5
workflow-type: tm+mt
source-wordcount: '2413'
ht-degree: 5%

---

# Guía para desarrolladores de ingesta por lotes

Este documento proporciona una guía completa para utilizar [extremos de API de ingesta por lotes](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion) en Adobe Experience Platform. Para obtener una descripción general de las API de ingesta por lotes, incluidos los requisitos previos y las prácticas recomendadas, comience por leer el [información general de API de ingesta por lotes](overview.md).

En el apéndice del presente documento se proporciona información sobre [datos de formato que se utilizarán para la ingesta](#data-transformation-for-batch-ingestion), incluidos archivos de datos CSV y JSON de ejemplo.

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte de la variable [API de ingesta de datos](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). La ingesta de datos proporciona una API RESTful a través de la cual puede realizar operaciones básicas de CRUD con los tipos de objetos admitidos.

Antes de continuar, consulte la [información general de API de ingesta por lotes](overview.md) y el [guía de introducción](getting-started.md).

## Ingesta de archivos JSON

>[!NOTE]
>
>Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si supera el tiempo de espera de una puerta de enlace o solicita errores de tamaño de cuerpo, debe cambiar a una carga de archivo grande.

### Crear lote

En primer lugar, debe crear un lote, con JSON como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajusten al esquema XDM vinculado al conjunto de datos proporcionado.

>[!NOTE]
>
>Los ejemplos siguientes son para JSON de una sola línea. Para ingerir JSON de varias líneas, la variable `isMultiLineJson` será necesario establecer el indicador. Para obtener más información, lea la [guía de solución de problemas de ingesta por lotes](./troubleshooting.md).

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | ID del conjunto de datos de referencia. |

**Respuesta**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | El ID del conjunto de datos al que se hace referencia. |

### Cargar archivos

Ahora que ha creado un lote, puede utilizar el ID de lote de la respuesta de creación de lotes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

>[!NOTE]
>
>Consulte la sección del apéndice para obtener una [ejemplo de un archivo de datos JSON con formato correcto](#data-transformation-for-batch-ingestion).

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | El nombre del archivo que desea cargar. Asegúrese de utilizar un nombre de archivo único para que no entre en conflicto con otro archivo para el lote de archivos que se envía. |

**Solicitud**

>[!NOTE]
>
>La API admite la carga de una sola parte. Asegúrese de que content-type es application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. Esta ruta de acceso del archivo es la ruta de acceso del archivo local, como `acme/customers/campaigns/summer.json`. |

**Respuesta**

```http
200 OK
```

### Completar lote

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```http
200 OK
```

## Ingesta de archivos de Parquet {#ingest-parquet-files}

>[!NOTE]
>
>Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si supera el tiempo de espera de una puerta de enlace o solicita errores de tamaño de cuerpo, deberá cambiar a una carga de archivo grande.

### Crear lote

En primer lugar, deberá crear un lote, con Parquet como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajusten al esquema XDM vinculado al conjunto de datos proporcionado.

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Parámetro | Descripción |
| --------- | ------------ |
| `{DATASET_ID}` | ID del conjunto de datos de referencia. |

**Respuesta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | El ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | El ID del usuario que creó el lote. |

### Cargar archivos

Ahora que ha creado un lote, puede utilizar el `batchId` desde antes de cargar los archivos en el lote. Puede cargar varios archivos en el lote.

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | El nombre del archivo que desea cargar. Asegúrese de utilizar un nombre de archivo único para que no entre en conflicto con otro archivo para el lote de archivos que se envía. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que content-type es application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. Esta ruta de acceso del archivo es la ruta de acceso del archivo local, como `acme/customers/campaigns/summer.parquet`. |

**Respuesta**

```http
200 OK
```

### Completar lote

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El identificador del lote que desea señalar está listo para su finalización. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Ingesta de archivos grandes de Parquet

>[!NOTE]
>
>En esta sección se explica cómo cargar archivos que superen los 256 MB. Los archivos grandes se cargan en fragmentos y luego se vinculan a través de una señal de API.

### Crear lote

En primer lugar, deberá crear un lote, con Parquet como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajusten al esquema XDM vinculado al conjunto de datos proporcionado.

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | ID del conjunto de datos de referencia. |

**Respuesta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | El ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | El ID del usuario que creó el lote. |

### Inicializar archivo grande

Después de crear el lote, deberá inicializar el archivo grande antes de cargar los fragmentos en el lote.

**Formato de API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | El ID del conjunto de datos al que se hace referencia. |
| `{FILE_NAME}` | Nombre del archivo que se va a inicializar. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
201 Created
```

### Cargar fragmentos de archivo grandes

Ahora que se ha creado el archivo, se pueden cargar todos los fragmentos posteriores realizando solicitudes repetidas al PATCH, una para cada sección del archivo.

**Formato de API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | El nombre del archivo que desea cargar. Asegúrese de utilizar un nombre de archivo único para que no entre en conflicto con otro archivo para el lote de archivos que se envía. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que content-type es application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONTENT_RANGE}` | En enteros, el principio y el final del intervalo solicitado. |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. Esta ruta de acceso del archivo es la ruta de acceso del archivo local, como `acme/customers/campaigns/summer.json`. |


**Respuesta**

```http
200 OK
```

### Archivo grande completo

Ahora que ha creado un lote, puede utilizar el `batchId` desde antes de cargar los archivos en el lote. Puede cargar varios archivos en el lote.

**Formato de API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote del que desea indicar la finalización. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | El nombre del archivo del que desea indicar la finalización. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
201 Created
```

### Completar lote

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | Se ha completado el ID del lote que desea señalar. |


**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Ingesta de archivos CSV

Para introducir archivos CSV, deberá crear una clase, un esquema y un conjunto de datos que admita CSV. Para obtener información detallada sobre cómo crear la clase y el esquema necesarios, siga las instrucciones que se proporcionan en la [tutorial de creación de esquemas ad hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si supera el tiempo de espera de una puerta de enlace o solicita errores de tamaño de cuerpo, deberá cambiar a una carga de archivo grande.

### Crear conjunto de datos

Después de seguir las instrucciones anteriores para crear la clase y el esquema necesarios, debe crear un conjunto de datos compatible con CSV.

**Formato de API**

```http
POST /catalog/dataSets
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres correcto y estén contenidos en su organización IMS. |
| `{SCHEMA_ID}` | El ID del esquema que ha creado. |

### Crear lote

A continuación, debe crear un lote con CSV como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajusten al esquema vinculado al conjunto de datos proporcionado.

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | ID del conjunto de datos de referencia. |

**Respuesta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | El ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | El ID del usuario que creó el lote. |

### Cargar archivos

Ahora que ha creado un lote, puede utilizar el `batchId` desde antes de cargar los archivos en el lote. Puede cargar varios archivos en el lote.

>[!NOTE]
>
>Consulte la sección del apéndice para obtener una [ejemplo de un archivo de datos CSV con el formato correcto](#data-transformation-for-batch-ingestion).

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | El nombre del archivo que desea cargar. Asegúrese de utilizar un nombre de archivo único para que no entre en conflicto con otro archivo para el lote de archivos que se envía. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que content-type es application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. Esta ruta de acceso del archivo es la ruta de acceso del archivo local, como `acme/customers/campaigns/summer.csv`. |


**Respuesta**

```http
200 OK
```

### Completar lote

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```http
200 OK
```

## Cancelar un lote

Mientras el lote se está procesando, aún se puede cancelar. Sin embargo, una vez finalizado un lote (como un estado correcto o fallido), el lote no se puede cancelar.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote que desea cancelar. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Eliminar un lote {#delete-a-batch}

Un lote se puede eliminar realizando la siguiente solicitud de POST con el `action=REVERT` parámetro de consulta al ID del lote que desea eliminar. El lote está marcado como &quot;inactivo&quot;, por lo que es apto para la recolección de basura. El lote se recopilará asincrónicamente, momento en el que se marcará como &quot;eliminado&quot;.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote que desea eliminar. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Parche de un lote

En ocasiones puede ser necesario actualizar los datos en el almacén de perfiles de su organización. Por ejemplo, es posible que tenga que corregir registros o cambiar un valor de atributo. Adobe Experience Platform admite la actualización o el parche de datos del Almacenamiento de perfiles mediante una acción de actualización o &quot;aplicación de parches a un lote&quot;.

>[!NOTE]
>
>Estas actualizaciones solo se permiten en registros de perfil, no en eventos de experiencia.

Para aplicar parches a un lote, es necesario lo siguiente:

- **Un conjunto de datos habilitado para actualizaciones de perfiles y atributos.** Esto se realiza mediante etiquetas de conjuntos de datos y requiere un `isUpsert:true` se añadirá a la etiqueta `unifiedProfile` matriz. Para obtener más información sobre los pasos que muestran cómo crear un conjunto de datos o configurar uno existente para su actualización, siga el tutorial de [habilitar un conjunto de datos para actualizaciones de perfil](../../catalog/datasets/enable-upsert.md).
- **Archivo de parquet que contiene los campos a los que se va a aplicar el parche y los campos de identidad del perfil.** El formato de datos para aplicar parches a un lote es similar al proceso normal de introducción por lotes. La entrada requerida es un archivo de Parquet. Además de los campos que se van a actualizar, los datos cargados deben contener los campos de identidad para que coincidan con los datos del almacén de perfiles.

Una vez que tenga un conjunto de datos habilitado para Perfil y actualización, y un archivo de Parquet que contenga los campos a los que desee aplicar parches, así como los campos de identidad necesarios, puede seguir los pasos para [ingesta de archivos de Parquet](#ingest-parquet-files) para completar el parche mediante la ingesta por lotes.

## Reproducción de un lote

Si desea reemplazar un lote ya introducido, puede hacerlo con &quot;reproducción por lotes&quot;: esta acción equivale a eliminar el lote antiguo e ingerir uno nuevo en su lugar.

### Crear lote

En primer lugar, debe crear un lote, con JSON como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajusten al esquema XDM vinculado al conjunto de datos proporcionado. Además, deberá proporcionar los lotes antiguos como referencia en la sección de reproducción. En el siguiente ejemplo, se reproducen lotes con ID `batchIdA` y `batchIdB`.

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Parámetro | Descripción |
| --------- | ----------- | 
| `{DATASET_ID}` | ID del conjunto de datos de referencia. |

**Respuesta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | El ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | El ID del usuario que creó el lote. |


### Cargar archivos

Ahora que ha creado un lote, puede utilizar el `batchId` desde antes de cargar los archivos en el lote. Puede cargar varios archivos en el lote.

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | El nombre del archivo que desea cargar. Asegúrese de utilizar un nombre de archivo único para que no entre en conflicto con otro archivo para el lote de archivos que se envía. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que content-type es application/octet-stream. No utilice la opción curl -F, ya que el valor predeterminado es una solicitud de varias partes incompatible con la API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. Esta ruta de acceso del archivo es la ruta de acceso del archivo local, como `acme/customers/campaigns/summer.json`. |

**Respuesta**

```http
200 OK
```

### Completar lote

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote que desea completar. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```http
200 OK
```

## Apéndice

La siguiente sección contiene información adicional para la ingesta de datos en Experience Platform mediante la ingesta por lotes.

### Transformación de datos para la ingesta por lotes

Para introducir un archivo de datos en [!DNL Experience Platform], la estructura jerárquica del archivo debe cumplir con el [Modelo de datos de experiencia (XDM)](../../xdm/home.md) esquema asociado con el conjunto de datos que se carga en.

Encontrará información sobre cómo asignar un archivo CSV para cumplir con un esquema XDM en la [transformaciones de muestra](../../etl/transformations.md) , junto con un ejemplo de un archivo de datos JSON con el formato correcto. Los archivos de ejemplo proporcionados en el documento se pueden encontrar aquí:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
