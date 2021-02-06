---
keywords: Experience Platform;inicio;temas populares;ingestión por lotes;ingestión por lotes;ingestión parcial;Ingesta parcial;Error de recuperación;error de recuperación;ingestión parcial por lotes;ingestión parcial por lotes;ingestión parcial;ingesta;Ingesta;diagnóstico de errores;recuperación de diagnósticos de errores;obtención de diagnósticos de errores;error;obtención de errores;recuperación de errores;
solution: Experience Platform
title: Recuperación de diagnósticos de error de inserción de datos
topic: overview
description: Este documento proporciona información sobre la monitorización de la ingestión por lotes, la gestión de errores de ingestión parcial por lotes, así como una referencia para tipos de ingestión parcial por lotes.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---


# Recuperación de diagnósticos de error de inserción de datos

Adobe Experience Platform proporciona dos métodos para cargar e ingestar datos. Puede utilizar la ingestión por lotes, que le permite insertar datos mediante varios tipos de archivo (como CSV), o la ingestión por flujo continuo, que le permite insertar sus datos en [!DNL Platform] mediante el uso de puntos finales de flujo en tiempo real.

Este documento proporciona información sobre la monitorización de la ingestión por lotes, la gestión de errores de ingestión parcial por lotes, así como una referencia para tipos de ingestión parcial por lotes.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md):: Métodos por los que se pueden enviar datos  [!DNL Experience Platform].

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Schema Registry], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

## Descarga de diagnósticos de error {#download-diagnostics}

Adobe Experience Platform permite a los usuarios descargar los diagnósticos de error de los archivos de entrada. Los diagnósticos se conservarán en [!DNL Platform] durante un máximo de 30 días.

### Archivos de entrada de lista {#list-files}

La siguiente solicitud recupera una lista de todos los archivos proporcionados en un lote finalizado.

**Formato API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote que está buscando. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devolverá objetos JSON en los que se detalla dónde se guardaron los diagnósticos.

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

### Recuperar diagnósticos de archivos de entrada {#retrieve-diagnostics}

Una vez que haya recuperado una lista de todos los diferentes archivos de entrada, puede recuperar los diagnósticos del archivo individual mediante la siguiente solicitud.

**Formato API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote que está buscando. |
| `{FILE}` | Nombre del archivo al que está accediendo. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devolverá objetos JSON que contengan `path` objetos que detallen dónde se guardaron los diagnósticos. La respuesta devolverá los objetos `path` en formato [Líneas JSON](https://jsonlines.org/).

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recuperar errores de ingestión por lotes {#retrieve-errors}

Si los lotes contienen errores, debe recuperar la información de error sobre estos errores para poder volver a ingestar los datos.

### Comprobar estado {#check-status}

Para comprobar el estado del lote ingestado, debe proporcionar el ID del lote en la ruta de una solicitud de GET.

**Formato API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El valor `id` del lote del que desea comprobar el estado. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
        "imsOrg": "{IMS_ORG}",
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
| `metrics.failedRecordCount` | Número de filas que no se pudieron procesar debido al análisis, la conversión o la validación. Este valor se puede obtener restando el `inputRecordCount` del `outputRecordCount`. Este valor se genera en todos los lotes, independientemente de si `errorDiagnostics` está habilitado. |

**Respuesta con errores**

Si el lote tiene uno o más errores y tiene habilitados los diagnósticos de error, la respuesta devuelve más información sobre los errores, tanto dentro de la carga útil como en un archivo de error descargable. Tenga en cuenta que el estado de un lote que contiene errores puede seguir teniendo un estado de éxito.

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
        "imsOrg": "{IMS_ORG}",
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
| `metrics.failedRecordCount` | Número de filas que no se pudieron procesar debido al análisis, la conversión o la validación. Este valor se puede obtener restando el `inputRecordCount` del `outputRecordCount`. Este valor se genera en todos los lotes, independientemente de si `errorDiagnostics` está habilitado. |
| `errors.recordCount` | El número de filas en las que se produjo un error en el código de error especificado. Este valor es **sólo** generado si `errorDiagnostics` está habilitado. |

>[!NOTE]
>
>Si los diagnósticos de error no están disponibles, aparecerá el siguiente mensaje de error:
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Pasos siguientes {#next-steps}

Este tutorial trata sobre cómo controlar los errores de ingestión parcial por lotes. Para obtener más información sobre la ingestión por lotes, lea la [guía para desarrolladores de ingestión por lotes](../batch-ingestion/api-overview.md).

## Apéndice {#appendix}

Esta sección proporciona información adicional sobre los tipos de error de ingestión.

### Tipos de error de ingestión parcial por lotes {#partial-ingestion-types}

La ingestión parcial de lotes tiene tres tipos de error diferentes al ingerir datos:

- [Archivos ilegibles](#unreadable)
- [Esquemas o encabezados no válidos](#schemas-headers)
- [Filas no analizables](#unparsable)

### Archivos ilegibles {#unreadable}

Si el lote ingestado tiene archivos ilegibles, los errores del lote se adjuntarán al lote mismo. Encontrará más información sobre cómo recuperar el lote dañado en la [guía de recuperación de lotes fallidos](../quality/retrieve-failed-batches.md).

### Esquemas o encabezados no válidos {#schemas-headers}

Si el lote ingestado tiene un esquema no válido o encabezados no válidos, los errores del lote se adjuntarán al lote mismo. Encontrará más información sobre cómo recuperar el lote dañado en la [guía de recuperación de lotes fallidos](../quality/retrieve-failed-batches.md).

### Filas no analizables {#unparsable}

Si el lote que ha ingestado tiene filas inanalizables, puede utilizar la siguiente solicitud para vista de una lista de archivos que contengan errores.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El valor `id` del lote desde el que está recuperando la información de error. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

A continuación, puede recuperar información detallada sobre los errores mediante el [extremo de recuperación de diagnósticos](#retrieve-diagnostics).

A continuación se muestra una respuesta de ejemplo de recuperación del archivo de error:

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
