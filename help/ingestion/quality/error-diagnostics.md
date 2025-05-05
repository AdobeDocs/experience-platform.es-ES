---
keywords: Experience Platform;inicio;temas populares;ingesta por lotes;ingesta por lotes;ingesta parcial;ingesta parcial;Recuperar error;recuperar error;ingesta parcial por lotes;ingesta parcial por lotes;ingesta parcial;ingesta parcial;ingesta;diagnósticos de error;recuperar diagnósticos de error;obtener diagnósticos de error;obtener error;obtener errores;recuperar errores;
solution: Experience Platform
title: Recuperación de diagnósticos de error de ingesta de datos
description: Este documento proporciona información sobre la monitorización de la ingesta por lotes y la gestión de los errores de ingesta parcial por lotes, así como una referencia para los tipos de ingesta parcial por lotes.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 9%

---

# Recuperando diagnósticos de error de ingesta de datos

Adobe Experience Platform proporciona dos métodos para cargar e ingerir datos. Puede usar la ingesta por lotes, que le permite insertar datos mediante varios tipos de archivo (como CSV), o la ingesta por transmisión, que le permite insertar sus datos en [!DNL Experience Platform] mediante extremos de transmisión en tiempo real.

Este documento proporciona información sobre la monitorización de la ingesta por lotes y la gestión de los errores de ingesta parcial por lotes, así como una referencia para los tipos de ingesta parcial por lotes.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): métodos mediante los cuales se pueden enviar datos a [!DNL Experience Platform].

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Schema Registry], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

## Descargando diagnósticos de error {#download-diagnostics}

Adobe Experience Platform permite a los usuarios descargar los diagnósticos de error de los archivos de entrada. Los diagnósticos se conservarán dentro de [!DNL Experience Platform] por un máximo de 30 días.

### Lista de archivos de entrada {#list-files}

La siguiente solicitud recupera una lista de todos los archivos proporcionados en un lote finalizado.

**Formato de API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que está buscando. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devolverá objetos JSON que detallan dónde se guardaron los diagnósticos.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Recuperar diagnósticos de archivo de entrada {#retrieve-diagnostics}

Una vez que haya recuperado una lista de todos los archivos de entrada diferentes, puede recuperar los diagnósticos del archivo individual mediante la siguiente solicitud.

**Formato de API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que está buscando. |
| `{FILE}` | Nombre del archivo al que está accediendo. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devolverá objetos JSON que contienen `path` objetos que detallan dónde se guardaron los diagnósticos. La respuesta devolverá los objetos `path` en formato [Líneas JSON](https://jsonlines.readthedocs.io/en/latest/).

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recuperar errores de ingesta por lotes {#retrieve-errors}

Si los lotes contienen errores, debe recuperar la información de error sobre estos errores para poder volver a introducir los datos.

### Comprobar estado {#check-status}

Para comprobar el estado del lote introducido, debe proporcionar el ID del lote en la ruta de una petición GET. Para obtener más información sobre cómo usar esta llamada de API, lea la [guía de extremo de catálogo](../../catalog/api/list-objects.md).

**Formato de API**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El valor `id` del lote del que desea comprobar el estado. |
| `{FILTER}` | Un parámetro de consulta utilizado para filtrar los resultados devueltos en la respuesta. Los parámetros múltiples se separan con el símbolo et (`&`). Para obtener más información, lea la guía sobre [filtrado de datos del catálogo](../../catalog/api/filter-data.md). |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta sin errores**

Se devuelve una respuesta correcta con información detallada sobre el estado del lote.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `metrics.failedRecordCount` | Número de filas que no se pudieron procesar debido al análisis, la conversión o la validación. Este valor se puede derivar restando `inputRecordCount` de `outputRecordCount`. Este valor se genera en todos los lotes independientemente de si `errorDiagnostics` está habilitado. |

**Respuesta con errores**

Si el lote tiene uno o más errores y tiene habilitados los diagnósticos de error, la respuesta devuelve más información sobre los errores, tanto dentro de la propia carga útil como de un archivo de error descargable. Tenga en cuenta que el estado de un lote que contiene errores puede seguir siendo correcto.

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `metrics.failedRecordCount` | Número de filas que no se pudieron procesar debido al análisis, la conversión o la validación. Este valor se puede derivar restando `inputRecordCount` de `outputRecordCount`. Este valor se genera en todos los lotes independientemente de si `errorDiagnostics` está habilitado. |
| `errors.recordCount` | Número de filas con errores para el código de error especificado. Este valor se genera **solamente** si `errorDiagnostics` está habilitado. |

>[!NOTE]
>
>Si los diagnósticos de error no están disponibles, aparecerá el siguiente mensaje de error en su lugar:
>
>```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Pasos siguientes {#next-steps}

En este tutorial se explica cómo monitorizar los errores de ingesta parcial por lotes. Para obtener más información sobre la ingesta por lotes, lea la [guía para desarrolladores de ingesta por lotes](../batch-ingestion/api-overview.md).

## Apéndice {#appendix}

Esta sección proporciona información suplementaria sobre los tipos de error de ingesta.

### Tipos de error de ingesta parcial por lotes {#partial-ingestion-types}

La ingesta parcial por lotes tiene tres tipos de error diferentes al ingerir datos:

- [Archivos ilegibles](#unreadable)
- [Esquemas o encabezados no válidos](#schemas-headers)
- [Filas no analizables](#unparsable)

### Archivos ilegibles {#unreadable}

Si el lote introducido tiene archivos ilegibles, los errores del lote se adjuntarán en el propio lote. Encontrará más información sobre la recuperación del lote con errores en la [guía de recuperación de lotes con errores](../quality/retrieve-failed-batches.md).

### Esquemas o encabezados no válidos {#schemas-headers}

Si el lote introducido tiene un esquema no válido o encabezados no válidos, los errores del lote se adjuntarán en el propio lote. Encontrará más información sobre la recuperación del lote con errores en la [guía de recuperación de lotes con errores](../quality/retrieve-failed-batches.md).

### Filas no analizables {#unparsable}

Si el lote que ha introducido tiene filas no analizables, puede utilizar la siguiente solicitud para ver una lista de archivos que contienen errores.

**Formato de API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El valor `id` del lote del que está recuperando información de error. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de los archivos que tienen errores.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Puede recuperar información detallada sobre los errores mediante el [extremo de recuperación de diagnósticos](#retrieve-diagnostics).

A continuación, se muestra una respuesta de ejemplo de recuperación del archivo de error:

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
