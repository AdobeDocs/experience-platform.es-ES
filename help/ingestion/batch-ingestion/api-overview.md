---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del desarrollador de la ingestión por lotes de Adobe Experience Platform
topic: developer guide
translation-type: tm+mt
source-git-commit: 6c17351b04fedefd4b57b9530f1d957da8183a68

---


# Guía para desarrolladores de ingestión por lotes

Este documento proporciona una descripción general completa del uso de las API [de ingestión por](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)lotes.

El apéndice de este documento proporciona información para [dar formato a los datos que se van a utilizar para la ingestión](#data-transformation-for-batch-ingestion), incluidos los archivos de datos CSV y JSON de ejemplo.

## Primeros pasos

La ingestión de datos proporciona una API RESTful mediante la cual puede realizar operaciones CRUD básicas con los tipos de objeto admitidos.

Las siguientes secciones proporcionan información adicional que debe conocer o tener disponible para realizar llamadas exitosas a la API de inserción por lotes.

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Ingesta](./overview.md)por lotes: Permite ingestar datos en Adobe Experience Platform como archivos por lotes.
- [Sistema](../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
- [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Las solicitudes que contienen una carga útil (POST, PUT, PATCH) pueden requerir un `Content-Type` encabezado adicional. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada. En esta guía se utilizan los siguientes tipos de contenido:

- Content-Type: application/json
- Content-Type: application/octet-stream

## Tipos

Al ingerir datos, es importante comprender cómo funcionan los esquemas del modelo de datos de experiencia (XDM). Para obtener más información sobre cómo los tipos de campos XDM se asignan a diferentes formatos, lea la guía [para desarrolladores de](../../xdm/api/getting-started.md)Esquema Registry.

Existe cierta flexibilidad al ingerir datos: si un tipo no coincide con lo que hay en el esquema de destinatario, los datos se convertirán al tipo de destinatario expresado. Si no puede, fallará el lote con un `TypeCompatibilityException`.

Por ejemplo, ni JSON ni CSV tienen un tipo de fecha ni de fecha y hora. Como resultado, estos valores se expresan con cadenas [formateadas](https://www.iso.org/iso-8601-date-and-time-format.html) ISO 8061 (&quot;2018-07-10T15:05:59.000-08:00&quot;) o con formato de hora Unix en milisegundos (1531263959999000 00) y se convierten en el momento de la ingestión al tipo XDM de destinatario.

La siguiente tabla muestra las conversiones admitidas al ingestar datos.

| Entrada (fila) vs Destinatario (col.) | Cadena | Byte | Corto | Número entero | Largo | Duplicada | Fecha | Fecha y hora | Objeto | Mapa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Cadena | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Corto | X | X | X | X | X | X |  |  |  |  |
| Número entero | X | X | X | X | X | X |  |  |  |  |
| Largo | X | X | X | X | X | X | X | X |  |  |
| Duplicada | X | X | X | X | X | X |  |  |  |  |
| Fecha |  |  |  |  |  |  | X |  |  |  |
| Fecha y hora |  |  |  |  |  |  |  | X |  |  |
| Objeto |  |  |  |  |  |  |  |  | X | X |
| Mapa |  |  |  |  |  |  |  |  | X | X |

>[!NOTE] Los booleanos y las matrices no se pueden convertir a otros tipos.

## Restricciones de entrada

La ingestión de datos por lotes tiene algunas restricciones:
- Número máximo de archivos por lote: 1500
- Tamaño máximo del lote: 100 GB
- Número máximo de propiedades o campos por fila: 10000
- Número máximo de lotes por minuto, por usuario: 138

## Ingestar archivos JSON

>[!NOTE] Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si se alcanza un tiempo de espera de puerta de enlace o se producen errores de tamaño del cuerpo de la solicitud, es necesario cambiar a una carga de archivos grande.

### Crear lote

En primer lugar, deberá crear un lote, con JSON como formato de entrada. Al crear el lote, deberá proporcionar una ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado.

>[!NOTE] Los ejemplos siguientes son para JSON de una sola línea. Para ingerir JSON multilínea, será necesario establecer el `isMultiLineJson` indicador. Para obtener más información, lea la guía de solución de problemas de ingestión de [lotes](./troubleshooting.md).

**Formato API**

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
| `{BATCH_ID}` | ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |

### Carga de archivos

Ahora que ha creado un lote, puede utilizar el `batchId` formulario de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

>[!NOTE] Consulte la sección del apéndice para ver un [ejemplo de un archivo](#data-transformation-for-batch-ingestion)de datos JSON formateado correctamente.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. |

**Solicitud**

>[!NOTE] La API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. |

**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote al que desea cargar. |

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

## Ingestar archivos de parquet

>[!NOTE] Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si se alcanza un tiempo de espera de puerta de enlace o se producen errores de tamaño del cuerpo de la solicitud, deberá cambiar a una carga de archivos grande.

### Crear lote

En primer lugar, deberá crear un lote, con Parquet como formato de entrada. Al crear el lote, deberá proporcionar una ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado.

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
| `{BATCH_ID}` | ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |

### Carga de archivos

Ahora que ha creado un lote, puede utilizar el `batchId` formulario de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. |

**Solicitud**

>[!CAUTION] Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. |

**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El ID del lote que desea señalar está listo para su finalización. |

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

## Ingestar archivos de parquet grandes

>[!NOTE] En esta sección se explica cómo cargar archivos de más de 256 MB. Los archivos de gran tamaño se cargan en fragmentos y luego se vinculan mediante una señal de API.

### Crear lote

En primer lugar, deberá crear un lote, con Parquet como formato de entrada. Al crear el lote, deberá proporcionar una ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado.

**Formato API**

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
| `{BATCH_ID}` | ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |

### Inicializar archivo grande

Después de crear el lote, deberá inicializar el archivo grande antes de cargar los fragmentos en el lote.

**Formato API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{FILE_NAME}` | Nombre del archivo que se va a inicializar. |

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

### Carga de grandes fragmentos de archivos

Ahora que el archivo se ha creado, todos los fragmentos subsiguientes se pueden cargar realizando solicitudes de PARCHE repetidas, una para cada sección del archivo.

**Formato API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. |

**Solicitud**

>[!CAUTION] Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

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
| `{CONTENT_RANGE}` | En enteros, el principio y el final del intervalo solicitado. |
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. |


**Respuesta**

```http
200 OK
```

### Completar archivo grande

Ahora que ha creado un lote, puede utilizar el `batchId` formulario de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

**Formato API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote que desea indicar que se ha completado. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo del que se desea indicar que se ha completado. |

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

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | Se completó la ID del lote que desea señalar. |


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

## Ingestar archivos CSV

Para poder ingestar archivos CSV, deberá crear una clase, un esquema y un conjunto de datos que admita CSV. Para obtener información detallada sobre cómo crear la clase y el esquema necesarios, siga las instrucciones que se proporcionan en el tutorial [de creación de esquemas](../../xdm/api/ad-hoc.md)específicos.

>[!NOTE] Los siguientes pasos son aplicables a archivos pequeños (256 MB o menos). Si se alcanza un tiempo de espera de puerta de enlace o se producen errores de tamaño del cuerpo de la solicitud, deberá cambiar a una carga de archivos grande.

### Crear conjunto de datos

Después de seguir las instrucciones anteriores para crear la clase y el esquema necesarios, deberá crear un conjunto de datos que admita CSV.

**Formato API**

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
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TENANT_ID}` | Este ID se utiliza para garantizar que los recursos que cree tengan el espacio de nombres correcto y estén contenidos en la organización de IMS. |
| `{SCHEMA_ID}` | ID del esquema que ha creado. |

A continuación se explica qué parte de la sección &quot;fileDescription&quot; del cuerpo de JSON es diferente:

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `format` | El formato del archivo maestro, no el formato del archivo de entrada. |
| `delimiters` | Carácter que se va a utilizar como delimitador. |
| `quotes` | Carácter que se va a utilizar para las comillas. |
| `escapes` | Carácter que se va a utilizar como carácter de escape. |
| `header` | El archivo cargado **debe** contener encabezados. Como la validación de esquema se realiza, esto debe establecerse en true. Además, los encabezados **no pueden** contener espacios. Si tiene espacios en el encabezado, reemplácelos por caracteres de subrayado. |
| `charset` | Campo opcional. Otros conjuntos de caracteres admitidos son &quot;US-ASCII&quot; e &quot;ISO-8869-1&quot;. Si se deja vacío, UTF-8 se asume de forma predeterminada. |

El conjunto de datos al que se hace referencia debe tener el bloque de descripción de archivo enumerado arriba y debe apuntar a un esquema válido en el Registro. De lo contrario, el archivo no se convertirá en parqué.

### Crear lote

A continuación, deberá crear un lote con CSV como formato de entrada. Al crear el lote, deberá proporcionar una ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema vinculado al conjunto de datos proporcionado.

**Formato API**

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
| `{BATCH_ID}` | ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |

### Carga de archivos

Ahora que ha creado un lote, puede utilizar el `batchId` formulario de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

>[!NOTE] Consulte la sección del apéndice para ver un [ejemplo de un archivo](#data-transformation-for-batch-ingestion)de datos CSV con el formato adecuado.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. |

**Solicitud**

>[!CAUTION] Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. |


**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato API**

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

Mientras el lote está procesando, aún puede cancelarse. Sin embargo, una vez finalizado un lote (como un estado de éxito o de error), el lote no se puede cancelar.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote que desea cancelar. |

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

Un lote puede eliminarse realizando la siguiente solicitud POST con el parámetro de `action=REVERT` consulta al ID del lote que desea eliminar. El lote está marcado como &quot;inactivo&quot;, lo que lo hace apto para la recolección de elementos no utilizados. El lote se recopilará de forma asíncrona, y en ese momento se marcará como &quot;eliminado&quot;.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote que desea eliminar. |

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

## Reproducción de un lote

Si desea reemplazar un lote ya ingerido, puede hacerlo con &quot;repetición por lotes&quot;; esta acción equivale a eliminar el lote antiguo y a ingerir uno nuevo en su lugar.

### Crear lote

En primer lugar, deberá crear un lote, con JSON como formato de entrada. Al crear el lote, deberá proporcionar una ID de conjunto de datos. También deberá asegurarse de que todos los archivos cargados como parte del lote se ajustan al esquema XDM vinculado al conjunto de datos proporcionado. Además, deberá proporcionar los lotes antiguos como referencia en la sección de reproducción. En el ejemplo siguiente, está reproduciendo lotes con ID `batchIdA` y `batchIdB`.

**Formato API**

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
| `{BATCH_ID}` | ID del lote recién creado. |
| `{DATASET_ID}` | ID del conjunto de datos al que se hace referencia. |
| `{USER_ID}` | ID del usuario que creó el lote. |


### Carga de archivos

Ahora que ha creado un lote, puede utilizar el `batchId` formulario de antes para cargar archivos en el lote. Puede cargar varios archivos en el lote.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote al que desea cargar. |
| `{DATASET_ID}` | ID del conjunto de datos de referencia del lote. |
| `{FILE_NAME}` | Nombre del archivo que desea cargar. |

**Solicitud**

>[!CAUTION] Esta API admite la carga de una sola parte. Asegúrese de que el tipo de contenido sea application/octet-stream. No utilice la opción curl -F, ya que establece de forma predeterminada una solicitud de varias partes que no es compatible con la API.

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
| `{FILE_PATH_AND_NAME}` | Ruta de acceso completa y nombre del archivo que intenta cargar. |

**Respuesta**

```http
200 OK
```

### Lote completo

Una vez que haya terminado de cargar todas las diferentes partes del archivo, deberá indicar que los datos se han cargado completamente y que el lote está listo para la promoción.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | ID del lote que desea completar. |

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

### Transformación de datos para la ingestión de lotes

Para poder transferir un archivo de datos a la plataforma de experiencia, la estructura jerárquica del archivo debe cumplir con el esquema del Modelo de datos de [experiencia (XDM)](../../xdm/home.md) asociado al conjunto de datos que se está cargando.

La información sobre cómo asignar un archivo CSV para cumplir con un esquema XDM se encuentra en el documento de transformaciones [de](../../etl/transformations.md) ejemplo, junto con un ejemplo de archivo de datos JSON formateado correctamente. Los archivos de ejemplo proporcionados en el documento se pueden encontrar aquí:

- [CRM_perfiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_perfiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)