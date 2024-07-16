---
keywords: Experience Platform;inicio;temas populares;recuperar lotes fallidos;lotes fallidos;ingesta por lotes;ingesta por lotes;lotes fallidos;obtener lotes fallidos;obtener lotes fallidos;descargar lotes fallidos;descargar lotes fallidos;
solution: Experience Platform
title: Recuperación de lotes con errores mediante la API de acceso a datos
type: Tutorial
description: Este tutorial cubre los pasos para recuperar información sobre un lote fallido mediante las API de ingesta de datos.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 14%

---

# Recuperación de lotes con errores mediante la API de acceso a datos

Adobe Experience Platform proporciona dos métodos para cargar e ingerir datos. Puede usar la ingesta por lotes, que le permite insertar sus datos mediante varios tipos de archivo (como CSV), o la ingesta por transmisión, que le permite insertar sus datos en [!DNL Platform] mediante extremos de transmisión en tiempo real.

Este tutorial cubre los pasos para recuperar información sobre un lote fallido mediante las API [!DNL Data Ingestion].

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Data Ingestion]](../home.md): métodos mediante los cuales se pueden enviar datos a [!DNL Experience Platform].

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Schema Registry], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- `Content-Type: application/json`

### Lote con errores de muestra

Este tutorial usará datos de ejemplo con una marca de tiempo con formato incorrecto que establece el valor del mes en **00**, como se ve a continuación:

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

La carga útil anterior no se validará correctamente con el esquema XDM debido a la marca de tiempo mal formada.

## Recuperación del lote fallido

**Formato de API**

```http
GET /batches/{BATCH_ID}/failed
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que está buscando. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
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

Con la respuesta anterior, puede ver qué fragmentos del lote se realizaron correctamente y cuáles fallaron. A partir de esta respuesta, puede ver que el archivo `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contiene el lote con errores.

## Descargar el lote fallido

Una vez que sepa qué archivo del lote falló, puede descargar el archivo fallido y ver cuál es el mensaje de error.

**Formato de API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que contiene el archivo fallido. |
| `{FAILED_FILE}` | Nombre del archivo que tiene el formato erróneo. |

**Solicitud**

La siguiente solicitud le permite descargar el archivo que tenía errores de ingesta.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Dado que el lote introducido anteriormente tenía una fecha y hora no válidas, se mostrará el siguiente error de validación.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## Pasos siguientes

Después de leer este tutorial, ha aprendido a recuperar errores de lotes fallidos. Para obtener más información sobre la ingesta por lotes, lea la [guía para desarrolladores de ingesta por lotes](../batch-ingestion/overview.md). Para obtener más información sobre la ingesta de transmisión por secuencias, lea el [tutorial sobre la creación de una conexión de transmisión por secuencias](../tutorials/create-streaming-connection.md).

## Apéndice

Esta sección contiene información sobre otros tipos de errores de ingesta que se pueden producir.

### XDM con formato incorrecto

Al igual que el error de marca de hora del ejemplo anterior, estos errores se deben a un XDM con formato incorrecto. Estos mensajes de error variarán según la naturaleza del problema. Como resultado, no se puede mostrar ningún ejemplo de error específico.

### Falta el ID de organización o no es válido

Este error se muestra si el ID de organización que falta en la carga no es válido.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Falta el esquema XDM

Este error se muestra si falta el `schemaRef` para `xdmMeta`.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Falta el nombre de origen

Este error se muestra si a `source` del encabezado le falta su `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### Falta la entidad XDM

Este error se muestra si no hay `xdmEntity` presente.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
