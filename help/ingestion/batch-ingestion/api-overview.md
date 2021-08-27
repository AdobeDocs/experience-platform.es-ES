---
keywords: Experience Platform;inicio;temas populares;ingesta por lotes;ingesta por lotes;ingesta;guía para desarrolladores;guía de api;cargar;ingesta de parquet;ingesta de json;
solution: Experience Platform
title: Guía de API de ingesta de lotes
topic-legacy: developer guide
description: Este documento proporciona una descripción general completa del uso de las API de ingesta por lotes.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 7%

---

# Guía de API de ingesta por lotes

Este documento proporciona una descripción general completa del uso de [API de ingesta por lotes](https://www.adobe.io/experience-platform-apis/references/data-ingestion/).

El apéndice de este documento proporciona información sobre los [datos de formato que se utilizarán para la ingesta](#data-transformation-for-batch-ingestion), incluidos archivos de datos CSV y JSON de muestra.

## Primeros pasos

La ingesta de datos proporciona una API RESTful mediante la cual puede realizar operaciones CRUD básicas con los tipos de objeto admitidos.

Las secciones siguientes proporcionan información adicional que debe conocer o tener disponible para realizar llamadas correctamente a la API de ingesta de lotes.

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [Ingesta por lotes](./overview.md): Permite introducir datos en Adobe Experience Platform como archivos por lotes.
- [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Las solicitudes que contienen una carga útil (POST, PUT, PATCH) pueden requerir un encabezado `Content-Type` adicional. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada .

## Tipos

Al ingerir datos, es importante comprender cómo funcionan los esquemas [!DNL Experience Data Model] (XDM). Para obtener más información sobre cómo se asignan los tipos de campo XDM a diferentes formatos, lea la [Guía para desarrolladores del Registro de Esquemas](../../xdm/api/getting-started.md).

Hay cierta flexibilidad a la hora de introducir datos: si un tipo no coincide con lo que hay en el esquema de destino, los datos se convertirán al tipo de destino expresado. Si no puede, fallará el lote con un `TypeCompatibilityException`.

Por ejemplo, ni JSON ni CSV tienen un tipo de fecha o fecha y hora. Como resultado, estos valores se expresan utilizando [cadenas con formato ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) o Tiempo Unix formateado en milisegundos (15312639 59000) y se convierten en el momento de la ingesta al tipo XDM de destino.

La tabla siguiente muestra las conversiones admitidas al introducir datos.

| Entrante (fila) frente a Target (col.) | Cadena | Byte | Corto | Número entero | Largo | Duplicada | Fecha  | Date-Time | Objeto | Mapa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Cadena | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Corto | X | X | X | X | X | X |  |  |  |  |
| Número entero | X | X | X | X | X | X |  |  |  |  |
| Largo | X | X | X | X | X | X | X | X |  |  |
| Duplicada | X | X | X | X | X | X |  |  |  |  |
| Fecha  |  |  |  |  |  |  | X |  |  |  |
| Date-Time |  |  |  |  |  |  |  | X |  |  |
| Objeto |  |  |  |  |  |  |  |  | X | X |
| Mapa |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Los booleanos y las matrices no se pueden convertir a otros tipos.

## Restricciones de ingesta

La ingesta de datos por lotes tiene algunas restricciones:
- Número máximo de archivos por lote: 1500
- Tamaño máximo del lote: 100 GB
- Número máximo de propiedades o campos por fila: 10000
- Número máximo de lotes por minuto, por usuario: 138

## Ingesta de archivos JSON

>[!NOTE]
>
>Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si se supera el tiempo de espera de la puerta de enlace o se solicitan errores de tamaño del cuerpo, debe cambiar a la carga de archivos de gran tamaño.

### Crear lote

En primer lugar, debe crear un lote, con JSON como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También debe asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado.

>[!NOTE]
>
>Los ejemplos siguientes son para JSON de una sola línea. Para ingerir JSON multilínea, será necesario establecer el indicador `isMultiLineJson` . Para obtener más información, lea la [guía de solución de problemas de ingesta por lotes](./troubleshooting.md).

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |

### Cargar archivos

Ahora que ha creado un lote, puede utilizar el `batchId` de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

>[!NOTE]
>
>Consulte la sección del apéndice para ver un [ejemplo de un archivo de datos JSON con formato correcto](#data-transformation-for-batch-ingestion).

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | El ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. Esta ruta de archivo es la ubicación donde se guardará el archivo en el lado del Adobe. |

**Solicitud**

>[!NOTE]
>
>La API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que está intentando cargar. Esta ruta de archivo es la ruta de archivo local, como `Users/sample-user/Downloads/sample.json`. |

**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las partes del archivo, tendrá que indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```http
200 OK
```

## Ingesta de archivos de parquet

>[!NOTE]
>
>Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si supera el tiempo de espera de la puerta de enlace o solicita errores de tamaño del cuerpo, deberá cambiar a la carga de archivos de gran tamaño.

### Crear lote

En primer lugar, tendrá que crear un lote, con Parquet como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También debe asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado.

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |

### Cargar archivos

Ahora que ha creado un lote, puede utilizar el `batchId` de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | El ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. Esta ruta de archivo es la ubicación donde se guardará el archivo en el lado del Adobe. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que está intentando cargar. Esta ruta de archivo es la ruta de archivo local, como `Users/sample-user/Downloads/sample.json`. |

**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las partes del archivo, tendrá que indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote que desea señalar está listo para completarse. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Ingesta de archivos de parqué grandes

>[!NOTE]
>
>Esta sección detalla cómo cargar archivos de más de 256 MB. Los archivos grandes se cargan en fragmentos y luego se vinculan mediante una señal de API.

### Crear lote

En primer lugar, tendrá que crear un lote, con Parquet como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También debe asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado.

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |

### Inicializar archivo grande

Después de crear el lote, tendrá que inicializar el archivo grande antes de cargar fragmentos en el lote.

**Formato de API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{FILE_NAME}` | Nombre del archivo que está a punto de iniciarse. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
201 Created
```

### Cargar fragmentos de archivos grandes

Ahora que el archivo se ha creado, todos los fragmentos posteriores se pueden cargar realizando solicitudes de PATCH repetidas, una para cada sección del archivo.

**Formato de API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | El ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. Esta ruta de archivo es la ubicación donde se guardará el archivo en el lado del Adobe. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONTENT_RANGE}` | En enteros, el principio y el final del rango solicitado. |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que está intentando cargar. Esta ruta de archivo es la ruta de archivo local, como `Users/sample-user/Downloads/sample.json`. |


**Respuesta**

```http
200 OK
```

### Completar archivo grande

Ahora que ha creado un lote, puede utilizar el `batchId` de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

**Formato de API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote que desea que indique la finalización del proceso. |
| `{DATASET_ID}` | El ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | El nombre del archivo que desea que indique la finalización de. |

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
201 Created
```

### Lote completo

Una vez que haya terminado de cargar todas las partes del archivo, tendrá que indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Ingesta de archivos CSV

Para introducir archivos CSV, deberá crear una clase, un esquema y un conjunto de datos que admita CSV. Para obtener información detallada sobre cómo crear la clase y el esquema necesarios, siga las instrucciones proporcionadas en el [tutorial de creación de esquema ad-hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si supera el tiempo de espera de la puerta de enlace o solicita errores de tamaño del cuerpo, deberá cambiar a la carga de archivos de gran tamaño.

### Crear conjunto de datos

Después de seguir las instrucciones anteriores para crear la clase y el esquema necesarios, debe crear un conjunto de datos que admita CSV.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres adecuado y estén contenidos dentro de su organización de IMS. |
| `{SCHEMA_ID}` | El ID del esquema que ha creado. |

### Crear lote

A continuación, debe crear un lote con CSV como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También debe asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema vinculado al conjunto de datos proporcionado.

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |

### Cargar archivos

Ahora que ha creado un lote, puede utilizar el `batchId` de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

>[!NOTE]
>
>Consulte la sección del apéndice para ver un [ejemplo de un archivo de datos CSV con formato correcto](#data-transformation-for-batch-ingestion).

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | El ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. Esta ruta de archivo es la ubicación donde se guardará el archivo en el lado del Adobe. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que está intentando cargar. Esta ruta de archivo es la ruta de archivo local, como `Users/sample-user/Downloads/sample.json`. |


**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las partes del archivo, tendrá que indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato de API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```http
200 OK
```

## Cancelar un lote

Mientras el lote se esté procesando, aún se puede cancelar. Sin embargo, una vez finalizado un lote (como un estado de éxito o de error), el lote no se puede cancelar.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Eliminar un lote {#delete-a-batch}

Se puede eliminar un lote realizando la siguiente solicitud de POST con el parámetro de consulta `action=REVERT` al ID del lote que desea eliminar. El lote está marcado como &quot;inactivo&quot;, lo que lo hace apto para la recolección de basura. El lote se recopilará asincrónicamente, momento en el que se marcará como &quot;eliminado&quot;.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Respuesta**

```http
200 OK
```

## Reproducir un lote

Si desea reemplazar un lote ya ingestado, puede hacerlo con &quot;reproducción por lotes&quot;: esta acción equivale a eliminar el lote antiguo e ingerir uno nuevo en su lugar.

### Crear lote

En primer lugar, debe crear un lote, con JSON como formato de entrada. Al crear el lote, deberá proporcionar un ID de conjunto de datos. También debe asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado. Además, debe proporcionar los lotes antiguos como referencia en la sección de repetición. En el siguiente ejemplo, está reproduciendo lotes con ID `batchIdA` y `batchIdB`.

**Formato de API**

```http
POST /batches
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |


### Cargar archivos

Ahora que ha creado un lote, puede utilizar el `batchId` de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote al que desea cargar. |
| `{DATASET_ID}` | El ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. Esta ruta de archivo es la ubicación donde se guardará el archivo en el lado del Adobe. |

**Solicitud**

>[!CAUTION]
>
>Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream. No utilice la opción curl -F, ya que el valor predeterminado de la solicitud de varias partes es incompatible con la API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que está intentando cargar. Esta ruta de archivo es la ruta de archivo local, como `Users/sample-user/Downloads/sample.json`. |

**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las partes del archivo, tendrá que indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```http
200 OK
```

## Apéndice

### Transformación de datos para la ingesta por lotes

Para poder introducir un archivo de datos en [!DNL Experience Platform], la estructura jerárquica del archivo debe cumplir con el esquema [Experience Data Model (XDM)](../../xdm/home.md) asociado con el conjunto de datos que se está cargando en.

Puede encontrar información sobre cómo asignar un archivo CSV para cumplir con un esquema XDM en el documento [transformaciones de ejemplo](../../etl/transformations.md), junto con un ejemplo de archivo de datos JSON con formato correcto. Los archivos de muestra proporcionados en el documento se pueden encontrar aquí:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
