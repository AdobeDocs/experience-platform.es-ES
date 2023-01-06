---
keywords: Experience Platform;inicio;temas populares;recuperar lotes fallidos;lotes fallidos;ingesta por lotes;ingesta por lotes;lotes fallidos;obtener lotes fallidos;obtener lotes fallidos;descargar lotes fallidos;descargar lotes fallidos;
solution: Experience Platform
title: Recuperación de lotes en los que se han producido errores al usar la API de acceso a datos
type: Tutorial
description: Este tutorial trata los pasos para recuperar información sobre un lote con errores mediante las API de ingesta de datos.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# Recuperación de lotes con errores mediante la API de acceso a datos

Adobe Experience Platform proporciona dos métodos para cargar e introducir datos. Puede utilizar la ingesta por lotes, que le permite insertar sus datos mediante varios tipos de archivo (como CSV), o la ingesta de flujo, que le permite insertar sus datos en [!DNL Platform] uso de extremos de flujo continuo en tiempo real.

Este tutorial trata los pasos para recuperar información sobre un lote fallido mediante [!DNL Data Ingestion] API.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Data Ingestion]](../home.md): Métodos por los cuales se pueden enviar datos [!DNL Experience Platform].

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidas las pertenecientes al [!DNL Schema Registry], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- `Content-Type: application/json`

### Muestra de lote fallido

Este tutorial utilizará datos de ejemplo con una marca de tiempo con formato incorrecto que establece el valor del mes que se **00**, como se ve a continuación:

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

La carga útil anterior no se validará correctamente con el esquema XDM debido a una marca de tiempo mal formada.

## Recuperar el lote fallido

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

Con la respuesta anterior, puede ver qué partes del lote se completaron correctamente y fallaron. Desde esta respuesta, puede ver que el archivo `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contiene el lote fallido.

## Descargar el lote fallido

Una vez que sepa qué archivo del lote ha fallado, puede descargar el archivo fallido y ver cuál es el mensaje de error.

**Formato de API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | El ID del lote que contiene el archivo con error. |
| `{FAILED_FILE}` | Nombre del archivo que tiene el formato con errores. |

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

Dado que el lote ingestado anterior tenía una fecha y hora no válida, se mostrará el siguiente error de validación.

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

Después de leer este tutorial, ha aprendido a recuperar errores de lotes con errores. Para obtener más información sobre la ingesta de lotes, lea la [guía para desarrolladores sobre ingesta por lotes](../batch-ingestion/overview.md). Para obtener más información sobre la transmisión por secuencias, lea la [creación de un tutorial de conexión de flujo continuo](../tutorials/create-streaming-connection.md).

## Apéndice

Esta sección contiene información sobre otros tipos de error de ingesta que pueden producirse.

### XDM con formato incorrecto

Al igual que el error de marca de tiempo en el flujo del ejemplo anterior, estos errores se deben a un XDM con formato incorrecto. Estos mensajes de error variarán según la naturaleza del problema. Como resultado, no se puede mostrar ningún ejemplo de error específico.

### Falta o no es válido el ID de organización de IMS

Este error se muestra si el ID de organización de IMS que falta en la carga no es válido.

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

Este error se muestra si la variable `schemaRef` para el `xdmMeta` falta.

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

Este error se muestra si la variable `source` en el encabezado falta su `name`.

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
