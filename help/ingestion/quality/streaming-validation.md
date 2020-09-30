---
keywords: Experience Platform;home;popular topics;streaming;streaming ingestion;streaming ingestion validation;validation;Streaming ingestion validation;validate;Synchronous validation;synchronous validation;Asynchronous validation;asynchronous validation;
solution: Experience Platform
title: Validación de la ingesta de flujo continuo
topic: tutorial
type: Tutorial
description: 'El flujo continuo de la ingestión le permite cargar sus datos en Adobe Experience Platform mediante puntos finales de flujo en tiempo real. Las API de inserción de flujo continuo admiten dos modos de validación: sincrónico y asincrónico.'
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 3%

---


# Validación de la ingesta de flujo continuo

El flujo continuo de la ingestión le permite cargar sus datos en Adobe Experience Platform mediante puntos finales de flujo en tiempo real. Las API de inserción de flujo continuo admiten dos modos de validación: sincrónico y asincrónico.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema de modelo de datos de experiencia (XDM) [!DNL]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!Ingesta de flujo DNL]](../streaming-ingestion/overview.md): Uno de los métodos mediante los cuales se pueden enviar datos [!DNL Experience Platform].

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen al [!DNL Schema Registry], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: `application/json`

### Cobertura de validación

[!DNL Streaming Validation Service] abarca la validación en las siguientes áreas:
- Intervalo
- Presencia
- Enum
- Patrón
- Tipo
- Formato

## Validación sincrónica

La validación sincrónica es un método de validación que proporciona información inmediata sobre los motivos por los que se ha producido un error en la ingestión. Sin embargo, si se produce un error, los registros en los que se ha producido un error al efectuar la validación se eliminan y se impide que se envíen en sentido descendente. Como resultado, la validación sincrónica sólo debe utilizarse durante el proceso de desarrollo. Al realizar la validación sincrónica, se informa a los autores de llamadas tanto del resultado de la validación XDM como, en caso de error, del motivo del error.

De forma predeterminada, la validación sincrónica no está activada. Para habilitarlo, debe pasar el parámetro de consulta opcional `synchronousValidation=true` al realizar llamadas de API. Además, la validación sincrónica actualmente solo está disponible si el extremo de flujo está en el centro de datos VA7.

Si un mensaje falla durante la validación sincrónica, el mensaje no se escribirá en la cola de salida, lo que proporciona información inmediata para los usuarios.

**Formato API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El `id` valor de la conexión de flujo creada anteriormente. |

**Solicitud**

Envíe la siguiente solicitud para transferir datos a la entrada de datos con validación sincrónica:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | El cuerpo JSON de los datos que desea ingestar. |

**Respuesta**

Con la validación sincrónica habilitada, una respuesta correcta incluye todos los errores de validación encontrados en su carga útil:

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

La respuesta anterior lista cuántas violaciones de esquema se encontraron y cuáles fueron. Por ejemplo, esta respuesta indica que las claves `workEmail` y `person` no se definieron en el esquema y, por lo tanto, no se permiten. También marca el valor para `_id` como incorrecto, ya que el esquema esperaba un `string`, pero se `long` insertó un valor en su lugar. Tenga en cuenta que una vez que se detecten cinco errores, el servicio de validación **dejará** de procesar ese mensaje. Sin embargo, se seguirán analizando otros mensajes.

## Validación asincrónica

La validación asincrónica es un método de validación que no proporciona información inmediata. En su lugar, los datos se envían a un lote dañado en [!DNL Data Lake] para evitar la pérdida de datos. Estos datos fallidos se pueden recuperar posteriormente para mayor análisis y reproducción. Este método debe utilizarse en la producción. A menos que se solicite lo contrario, la transmisión por flujo continuo funciona en modo de validación asincrónico.

**Formato API**

```http
POST /collection/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El `id` valor de la conexión de flujo creada anteriormente. |

**Solicitud**

Envíe la siguiente solicitud para transferir datos a la entrada de datos con validación asincrónica:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | El cuerpo JSON de los datos que desea ingestar. |

>[!NOTE]
>
>No se requiere ningún parámetro de consulta adicional, ya que la validación asincrónica está habilitada de forma predeterminada.

**Respuesta**

Con la validación asincrónica habilitada, una respuesta correcta devuelve lo siguiente:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

Observe cómo la respuesta indica que se ha omitido la validación sincrónica, ya que no se ha solicitado explícitamente.

## Apéndice

Esta sección contiene información sobre el significado de los distintos códigos de estado para las respuestas para la ingesta de datos.

### Códigos de estado

| Código de estado | Qué significa |
| ----------- | ------------- |
| 200 | Correcto. Para la validación sincrónica, significa que ha pasado las comprobaciones de validación. Para la validación asincrónica, significa que solo ha recibido correctamente el mensaje. Los usuarios pueden averiguar el estado final del mensaje observando el conjunto de datos. |
| 400 | Error. Hay algo malo en tu solicitud. Se recibe un mensaje de error con más detalles de los servicios de validación de flujo. |
| 401 | Error. Su solicitud no está autorizada, deberá solicitarla con un distintivo al portador. Para obtener más información sobre cómo solicitar acceso, consulte este [tutorial](../../tutorials/authentication.md) o esta entrada [de](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)blog. |
| 500 | Error. Hay un error interno del sistema. |
| 501 | Error. Esto significa que la validación sincrónica **no es** compatible con esta ubicación. |
| 503 | Error. El servicio no está disponible en este momento. Los clientes deben volver a intentarlo al menos tres veces con una estrategia exponencial de retroceso. |