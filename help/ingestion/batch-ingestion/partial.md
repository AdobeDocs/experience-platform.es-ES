---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre la ingesta parcial de lotes de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: ac75b1858b6a731915bbc698107f0be6043267d8
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 1%

---



# Ingestión parcial por lotes

La ingestión parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un cierto umbral. Con esta capacidad, los usuarios pueden transferir correctamente todos los datos correctos a Adobe Experience Platform mientras que todos los datos incorrectos se agrupan por lotes por separado, junto con los detalles de por qué no son válidos.

Este documento proporciona un tutorial para administrar la ingestión parcial por lotes.

Además, el [apéndice](#appendix) de este tutorial proporciona una referencia para los tipos de error de ingestión parcial por lotes.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos servicios de Adobe Experience Platform que intervienen en la ingestión parcial de lotes. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Ingesta](./overview.md)por lotes: Método que [!DNL Platform] ingiere y almacena datos de archivos de datos, como CSV y Parquet.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a [!DNL Platform] las API de forma satisfactoria.

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

## Habilitar un lote para la ingestión parcial de lotes en la API {#enable-api}

>[!NOTE]
>
>En esta sección se describe cómo habilitar un lote para la ingestión parcial por lotes mediante la API. Para obtener instrucciones sobre el uso de la interfaz de usuario, lea el paso [habilitar un lote para la ingestión parcial por lotes en la interfaz de usuario](#enable-ui) .

Puede crear un nuevo lote con la ingestión parcial activada.

Para crear un nuevo lote, siga los pasos de la guía [para desarrolladores de](./api-overview.md)ingestión por lotes. Una vez que llegue al paso **[!UICONTROL Crear lote]** , agregue el siguiente campo dentro del cuerpo de la solicitud:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `enableErrorDiagnostics` | Un indicador que permite [!DNL Platform] generar mensajes de error detallados sobre el lote. |
| `partialIngestionPercentage` | El porcentaje de errores aceptables antes de que se produzca un error en todo el lote. Así que, en este ejemplo, un máximo del 5% del lote puede ser error, antes de que falle. |


## Habilitar un lote para la ingestión parcial de lotes en la interfaz de usuario {#enable-ui}

>[!NOTE]
>
>En esta sección se describe cómo habilitar un lote para la ingestión parcial por lotes mediante la interfaz de usuario. Si ya ha habilitado un lote para la ingestión parcial por lotes mediante la API, puede pasar a la siguiente sección.

Para habilitar un lote para la ingestión parcial a través de la interfaz de usuario, puede crear un nuevo lote a través de conexiones de origen, crear un nuevo lote en un conjunto de datos existente o crear un nuevo lote a través del flujo [!DNL Platform] &quot;Asignar CSV a XDM&quot;.

### Crear una nueva conexión de origen {#new-source}

Para crear una nueva conexión de origen, siga los pasos que se enumeran en la descripción general [de](../../sources/home.md)Fuentes. Una vez que llegue al paso de detalle **[!UICONTROL de]** flujo de datos, tome nota de los campos de diagnóstico **[!UICONTROL de ingestión]** parcial y **** error.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

La **[!UICONTROL conmutación de ingestión]** parcial le permite habilitar o deshabilitar el uso de la ingestión parcial por lotes.

La opción de **[!UICONTROL diagnóstico]** de errores solo aparece cuando la opción de alternancia de ingestión **** parcial está desactivada. Esta función permite [!DNL Platform] generar mensajes de error detallados sobre los lotes ingestados. Si se activa la opción de alternancia de ingestión ** parcial, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

El umbral **[!UICONTROL de]** error permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

### Usar un conjunto de datos existente {#existing-dataset}

Para utilizar un conjunto de datos existente, seleccione un conjunto de datos para el inicio. La barra lateral de la derecha se rellena con información sobre el conjunto de datos.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

La **[!UICONTROL conmutación de ingestión]** parcial le permite habilitar o deshabilitar el uso de la ingestión parcial por lotes.

La opción de **[!UICONTROL diagnóstico]** de errores solo aparece cuando la opción de alternancia de ingestión **** parcial está desactivada. Esta función permite [!DNL Platform] generar mensajes de error detallados sobre los lotes ingestados. Si se activa la opción de alternancia de ingestión **** parcial, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

El umbral **[!UICONTROL de]** error permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

Ahora, puede cargar datos con el botón **Añadir datos** y se ingesta con ingestión parcial.

### Utilizar el flujo &quot;[!UICONTROL Asignar CSV al esquema]XDM&quot; {#map-flow}

Para utilizar el flujo &quot;[!UICONTROL Asignar CSV al esquema]XDM&quot;, siga los pasos enumerados en el tutorial [](../tutorials/map-a-csv-file.md)Asignar un archivo CSV. Una vez que llegue al paso de **[!UICONTROL Añadir datos]** , tome nota de los campos de diagnóstico de ingestión **** parcial y **[!UICONTROL error]** .

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

La **[!UICONTROL conmutación de ingestión]** parcial le permite habilitar o deshabilitar el uso de la ingestión parcial por lotes.

La opción de **[!UICONTROL diagnóstico]** de errores solo aparece cuando la opción de alternancia de ingestión **** parcial está desactivada. Esta función permite [!DNL Platform] generar mensajes de error detallados sobre los lotes ingestados. Si se activa la opción de alternancia de ingestión **** parcial, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

El umbral **[!UICONTROL de]** error permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

## Descarga de metadatos de nivel de archivo {#download-metadata}

Adobe Experience Platform permite a los usuarios descargar los metadatos de los archivos de entrada. Los metadatos se conservarán en un plazo [!DNL Platform] de hasta 30 días.

### Archivos de entrada de lista {#list-files}

La siguiente solicitud le permitirá vista de una lista de todos los archivos proporcionados en un lote finalizado.

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devolverá el estado HTTP 200 con objetos JSON que contengan objetos de ruta que detallen dónde se guardaron los metadatos.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Recuperar metadatos de archivo de entrada {#retrieve-metadata}

Una vez que haya recuperado una lista de todos los diferentes archivos de entrada, puede recuperar los metadatos del archivo individual utilizando el punto final siguiente.

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devolverá el estado HTTP 200 con objetos JSON que contengan objetos de ruta que detallen dónde se guardaron los metadatos.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recuperar errores parciales de ingesta por lotes {#retrieve-errors}

Si los lotes contienen errores, deberá recuperar la información de error sobre estos errores para poder volver a ingestar los datos.

### Comprobar estado {#check-status}

Para comprobar el estado del lote ingestado, debe proporcionar el ID del lote en la ruta de una solicitud de GET.

**Formato API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El `id` valor del lote del que desea comprobar el estado. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta sin errores**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el estado del lote.

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
| `metrics.failedRecordCount` | Número de filas que no se pudieron procesar debido al análisis, la conversión o la validación. Este valor se puede obtener restando el `inputRecordCount` valor de la `outputRecordCount`. Este valor se generará en todos los lotes, independientemente de si `errorDiagnostics` está activado. |

**Respuesta con errores**

Si el lote tiene uno o más errores y tiene habilitados los diagnósticos de error, el estado incluirá más información `success` sobre los errores proporcionados tanto en la respuesta como en un archivo de error descargable.

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
| `metrics.failedRecordCount` | Número de filas que no se pudieron procesar debido al análisis, la conversión o la validación. Este valor se puede obtener restando el `inputRecordCount` valor de la `outputRecordCount`. Este valor se generará en todos los lotes, independientemente de si `errorDiagnostics` está activado. |
| `errors.recordCount` | El número de filas en las que se produjo un error en el código de error especificado. Este valor **solo** se genera si `errorDiagnostics` está activado. |

>[!NOTE]
>
>Si los diagnósticos de error no están disponibles, aparecerá el siguiente mensaje de error:
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## Pasos siguientes {#next-steps}

Este tutorial trata sobre cómo crear o modificar un conjunto de datos para habilitar la ingestión parcial por lotes. Para obtener más información sobre la ingestión por lotes, lea la guía [para desarrolladores de la ingestión de](./api-overview.md)lotes.

## Tipos de error de ingestión parcial por lotes {#appendix}

La ingestión parcial de lotes tiene tres tipos de error diferentes al ingerir datos.

- [Archivos ilegibles](#unreadable)
- [Esquemas o encabezados no válidos](#schemas-headers)
- [Filas no analizables](#unparsable)

### Archivos ilegibles {#unreadable}

Si el lote ingestado tiene archivos ilegibles, los errores del lote se adjuntarán al lote mismo. Encontrará más información sobre cómo recuperar el lote dañado en la guía [de](../quality/retrieve-failed-batches.md)recuperación de lotes con errores.

### Esquemas o encabezados no válidos {#schemas-headers}

Si el lote ingestado tiene un esquema no válido o encabezados no válidos, los errores del lote se adjuntarán al lote mismo. Encontrará más información sobre cómo recuperar el lote dañado en la guía [de](../quality/retrieve-failed-batches.md)recuperación de lotes con errores.

### Filas no analizables {#unparsable}

Si el lote que ha ingestado tiene filas inanalizables, puede utilizar el punto final siguiente para la vista de una lista de archivos que contengan errores.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El `id` valor del lote desde el que está recuperando la información de error. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de los archivos que tienen errores.

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

A continuación, puede recuperar información detallada sobre los errores mediante el extremo [de recuperación de](#retrieve-metadata)metadatos.

A continuación se muestra una respuesta de ejemplo de recuperación del archivo de error:

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
