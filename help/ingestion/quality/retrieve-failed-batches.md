---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recuperar lotes con errores
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Recuperación de lotes con errores mediante la API

Adobe Experience Platform proporciona dos métodos para cargar e ingestar datos. Puede utilizar la ingestión por lotes, que le permite insertar sus datos mediante varios tipos de archivo (como CSV), o la ingestión por flujo continuo, que le permite insertar sus datos en la plataforma mediante puntos finales de flujo en tiempo real.

En este tutorial se explican los pasos para recuperar información sobre un lote en el que se ha producido un error al utilizar las API de inserción de datos.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
- [Ingesta](../home.md)de datos: Métodos mediante los cuales se pueden enviar datos a la plataforma de experiencias.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen al Registro de Esquemas, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: `application/json`

### Muestra de lote fallido

Este tutorial utilizará datos de ejemplo con una marca de tiempo con formato incorrecto que establece el valor del mes en **00**, como se muestra a continuación:

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

## Recuperar el lote fallido

**Formato API**

```http
GET /batches/{BATCH_ID}/failed
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote que está buscando. |

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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

Con la respuesta anterior, puede ver qué partes del lote se ejecutaron correctamente y fallaron. A partir de esta respuesta, puede ver que el archivo `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contiene el lote dañado.

## Descargar el lote dañado

Una vez que sepa qué archivo del lote ha fallado, puede descargar el archivo con error y ver cuál es el mensaje de error.

**Formato API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BATCH_ID}` | ID del lote que contiene el archivo con error. |
| `{FAILED_FILE}` | Nombre del archivo que tiene el formato con errores. |

**Solicitud**

La siguiente solicitud le permite descargar el archivo con errores de ingestión.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Después de leer este tutorial, ha aprendido a recuperar errores de lotes con errores. Para obtener más información sobre la ingestión por lotes, lea la guía [para desarrolladores de la ingestión de](../batch-ingestion/overview.md)lotes. Para obtener más información acerca de la transmisión por secuencias de ingesta, lea el tutorial sobre la [creación de una conexión de transmisión por secuencias](../tutorials/create-streaming-connection.md).

## Apéndice

Esta sección contiene información sobre otros tipos de error de ingestión que pueden producirse.

### XDM con formato incorrecto

Al igual que el error de marca de hora en el flujo de ejemplo anterior, estos errores se deben a un XDM con formato incorrecto. Estos mensajes de error variarán según la naturaleza del problema. Como resultado, no se puede mostrar ningún ejemplo de error específico.

### Falta el identificador de organización de IMS o no es válido

Este error se muestra si falta el identificador de organización de IMS en la carga no es válido.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Falta el esquema XDM

Este error se muestra si falta el `schemaRef` de la `xdmMeta` .

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Falta el nombre del origen

Este error se muestra si el `source` encabezado no tiene su valor `name`.

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

Este error se muestra si no hay `xdmEntity` presencia.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
