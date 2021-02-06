---
keywords: Experience Platform;inicio;temas populares;recuperar lotes fallidos;lotes fallidos;ingestión por lotes;ingestión por lotes;lotes fallidos;Obtener lotes fallidos;obtener lotes fallidos;Descargar lotes fallidos;descargar lotes fallidos;
solution: Experience Platform
title: Recuperación de lotes fallidos mediante la API de acceso a datos
topic: tutorial
type: Tutorial
description: En este tutorial se explican los pasos para recuperar información sobre un lote en el que se ha producido un error al utilizar las API de inserción de datos.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---


# Recuperación de lotes con errores mediante la API de acceso a datos

Adobe Experience Platform proporciona dos métodos para cargar e ingestar datos. Puede utilizar la ingestión por lotes, que le permite insertar sus datos mediante varios tipos de archivo (como CSV), o la ingestión por flujo continuo, que le permite insertar sus datos en [!DNL Platform] mediante el uso de puntos finales de flujo en tiempo real.

En este tutorial se explican los pasos para recuperar información sobre un lote con errores mediante API [!DNL Data Ingestion].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
- [[!DNL Data Ingestion]](../home.md):: Métodos por los que se pueden enviar datos  [!DNL Experience Platform].

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Schema Registry], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

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

Después de leer este tutorial, ha aprendido a recuperar errores de lotes con errores. Para obtener más información sobre la ingestión por lotes, lea la [guía para desarrolladores de ingestión por lotes](../batch-ingestion/overview.md). Para obtener más información sobre la ingestión de flujo continuo, lea el [tutorial de creación de una conexión de flujo](../tutorials/create-streaming-connection.md).

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

Este error se muestra si falta `schemaRef` para `xdmMeta`.

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

Este error se muestra si el `source` del encabezado no tiene su `name`.

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
