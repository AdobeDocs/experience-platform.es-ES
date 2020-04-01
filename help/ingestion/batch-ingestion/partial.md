---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre la ingesta parcial por lotes de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---



# Ingestión parcial por lotes

La ingestión parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un cierto umbral. Con esta capacidad, los usuarios pueden transferir correctamente todos los datos correctos a Adobe Experience Platform mientras que todos los datos incorrectos se agrupan por lotes por separado, junto con los detalles de por qué no son válidos.

Este documento proporciona un tutorial para administrar la ingestión parcial por lotes.

Además, el [apéndice](#partial-batch-ingestion-error-types) de este tutorial proporciona una referencia para los tipos de error de ingestión parcial por lotes.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform relacionados con la ingestión parcial por lotes. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Ingesta](./overview.md)por lotes: El método que Platform ingesta y almacena datos de archivos de datos, como CSV y Parquet.
- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API de plataforma.

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

## Habilitar un conjunto de datos para la ingestión parcial por lotes en la API

>[!NOTE] En esta sección se describe cómo habilitar un conjunto de datos para la ingestión parcial por lotes mediante la API. Para obtener instrucciones sobre el uso de la interfaz de usuario, lea el paso [habilitar un conjunto de datos para la ingestión parcial por lotes en la interfaz de usuario](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) .

Puede crear un nuevo conjunto de datos o modificar un conjunto de datos existente con la ingestión parcial habilitada.

Para crear un nuevo conjunto de datos, siga los pasos del tutorial [](../../catalog/api/create-dataset.md)Crear un conjunto de datos. Una vez que llegue al paso *Crear un conjunto de datos* , agregue el siguiente campo dentro del cuerpo de la solicitud:

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `errorThresholdPercentage` | El porcentaje de errores aceptables antes de que se produzca un error en todo el lote. |

Del mismo modo, para modificar un conjunto de datos existente, siga los pasos de la guía para desarrolladores de [catálogos](../../catalog/api/update-object.md).

Dentro del conjunto de datos, deberá agregar la etiqueta descrita anteriormente.

## Habilitar un conjunto de datos para la ingestión parcial por lotes en la interfaz de usuario

>[!NOTE] En esta sección se describe cómo habilitar un conjunto de datos para la ingestión parcial por lotes mediante la interfaz de usuario. Si ya ha habilitado un conjunto de datos para la ingestión parcial por lotes mediante la API, puede pasar a la siguiente sección.

Para habilitar un conjunto de datos para la ingestión parcial a través de la interfaz de usuario de la plataforma, haga clic en **Conjuntos** de datos en el panel de navegación izquierdo. Puede [crear un nuevo conjunto de datos](#create-a-new-dataset-with-partial-batch-ingestion-enabled) o [modificar uno existente](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### Crear un nuevo conjunto de datos con la ingestión parcial por lotes habilitada

Para crear un nuevo conjunto de datos, siga los pasos que se indican en la guía del usuario del [conjunto de datos](../../catalog/datasets/user-guide.md). Una vez que llegue al paso *Configurar conjunto de datos* , tome nota de los campos Ingesta ** parcial y Diagnósticos *de* error.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

La *conmutación de ingestión* parcial le permite habilitar o deshabilitar el uso de la ingestión parcial por lotes.

La opción Diagnósticos *de* error solo aparece cuando está desactivada la opción de alternancia de ingestión ** parcial. Esta función permite a Platform generar mensajes de error detallados sobre los lotes ingestados. Si se activa la *opción de cambio de inserción* parcial, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

El umbral *de* error permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

### Modificar un conjunto de datos existente para habilitar la ingestión parcial de lotes

Para modificar un conjunto de datos existente, seleccione el conjunto de datos que desee modificar. La barra lateral de la derecha se rellena con información sobre el conjunto de datos.

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

La *conmutación de ingestión* parcial le permite habilitar o deshabilitar el uso de la ingestión parcial por lotes.

El umbral *de* error permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

## Recuperar errores parciales de ingesta por lotes

Si los lotes contienen errores, deberá recuperar la información de error sobre estos errores para poder volver a ingestar los datos.

### Comprobar estado

Para comprobar el estado del lote ingestado, debe proporcionar el ID del lote en la ruta de una solicitud GET.

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

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre el estado del lote.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
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
            "outputRecordCount": 497
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

Si el lote tiene un error y los diagnósticos de error están habilitados, el estado será &quot;correcto&quot; con más información sobre el error proporcionado en un archivo de error descargable.

## Pasos siguientes

Este tutorial trata sobre cómo crear o modificar un conjunto de datos para habilitar la ingestión parcial por lotes. Para obtener más información sobre la ingestión por lotes, lea la guía [para desarrolladores de la ingestión de](./api-overview.md)lotes.

## Tipos de error de ingestión parcial por lotes

La ingestión parcial de lotes tiene cuatro tipos de error diferentes al ingerir datos.

- [Archivos ilegibles](#unreadable)
- [esquemas o encabezados no válidos](#schemas-headers)
- [Filas no analizables](#unparsable)
- [Conversión XDM no válida](#conversion)

### Archivos ilegibles {#unreadable}

Si el lote ingestado tiene archivos ilegibles, los errores del lote se adjuntarán al lote mismo. Encontrará más información sobre cómo recuperar el lote dañado en la guía [de](../quality/retrieve-failed-batches.md)recuperación de lotes con errores.

### esquemas o encabezados no válidos {#schemas-headers}

Si el lote ingestado tiene un esquema no válido o encabezados no válidos, los errores del lote se adjuntarán al lote mismo. Encontrará más información sobre cómo recuperar el lote dañado en la guía [de](../quality/retrieve-failed-batches.md)recuperación de lotes con errores.

### Filas no analizables {#unparsable}

Si el lote ingestado tiene filas inanalizables, los errores del lote se almacenarán en un archivo al que se pueda acceder mediante el punto final que se describe a continuación.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El `id` valor del lote desde el que está recuperando la información de error. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de las filas inanalizables.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### Conversión XDM no válida {#conversion}

Si el lote ingestado tiene conversiones XDM no válidas, los errores del lote se almacenarán en un archivo al que se puede acceder mediante el siguiente extremo.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BATCH_ID}` | El `id` valor del lote desde el que está recuperando la información de error. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de los errores en la conversión XDM.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
