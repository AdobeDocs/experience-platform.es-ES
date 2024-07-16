---
keywords: Experience Platform;inicio;temas populares;transmisión;transmisión;transmisión por secuencias;validación de transmisión por secuencias;validación;validación de transmisión por secuencias;validación;validación sincrónica;validación asincrónica;validación asincrónica;validación asincrónica;
solution: Experience Platform
title: Validación de ingesta de streaming
type: Tutorial
description: 'La introducción por transmisión le permite cargar los datos en Adobe Experience Platform mediante transmisión por secuencias de puntos finales en tiempo real. Las API de ingesta de transmisión admiten dos modos de validación: sincrónico y asincrónico.'
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 11%

---

# Validación de ingesta de streaming

La introducción por transmisión le permite cargar los datos en Adobe Experience Platform mediante transmisión por secuencias de puntos finales en tiempo real. Las API de ingesta de transmisión admiten dos modos de validación: sincrónico y asincrónico.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): uno de los métodos mediante los cuales se pueden enviar datos a [!DNL Experience Platform].

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Schema Registry], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Tipo de contenido: `application/json`

### Cobertura de validación

[!DNL Streaming Validation Service] cubre la validación en las siguientes áreas:
- Intervalo
- Presencia
- Enumeración
- Patrón
- Tipo
- Formato

## Validación sincrónica

La validación sincrónica es un método de validación que proporciona información inmediata sobre el motivo por el que ha fallado una ingesta. Sin embargo, si se produce un error, se pierden los registros que no superan la validación y se impide que se envíen de forma descendente. Como resultado, la validación sincrónica solo debe utilizarse durante el proceso de desarrollo. Al realizar la validación sincrónica, se informa a los llamadores tanto del resultado de la validación XDM como, si falla, del motivo del error.

De forma predeterminada, la validación sincrónica no está activada. Para habilitarlo, debe pasar el parámetro de consulta opcional `syncValidation=true` al realizar llamadas de API. Además, la validación sincrónica solo está disponible actualmente si el punto final de la secuencia se encuentra en el centro de datos de VA7.

>[!NOTE]
>
>El parámetro de consulta `syncValidation` solo está disponible para el extremo de mensaje único y no se puede usar para el extremo por lotes.

Si un mensaje falla durante la validación sincrónica, no se escribirá en la cola de salida, que proporciona comentarios inmediatos a los usuarios.

>[!NOTE]
>
>Es posible que los cambios de esquema no estén disponibles inmediatamente porque los cambios se almacenan en caché. Espere hasta quince minutos para que se actualice la caché.

**Formato de API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de la conexión de flujo continuo creada anteriormente. |

**Solicitud**

Envíe la siguiente solicitud para introducir datos a la entrada de datos con validación sincrónica:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | El cuerpo JSON de los datos que desea introducir. |

**Respuesta**

Con la validación sincrónica habilitada, una respuesta correcta incluye los errores de validación encontrados en su carga útil:

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

La respuesta anterior enumera cuántas violaciones de esquema se encontraron y cuáles fueron. Por ejemplo, esta respuesta indica que las claves `workEmail` y `person` no se definieron en el esquema y, por lo tanto, no están permitidas. También marca el valor de `_id` como incorrecto, ya que el esquema esperaba `string`, pero en su lugar se insertó `long`. Tenga en cuenta que cuando se encuentren cinco errores, el servicio de validación **detendrá** el procesamiento de ese mensaje. Sin embargo, se seguirán analizando otros mensajes.

## Validación asincrónica

La validación asincrónica es un método de validación que no proporciona comentarios inmediatos. En su lugar, los datos se envían a un lote erróneo en [!DNL Data Lake] para evitar la pérdida de datos. Estos datos con errores se pueden recuperar más adelante para su análisis y reproducción. Este método debe utilizarse en producción. A menos que se solicite lo contrario, la ingesta de transmisión funciona en modo de validación asincrónico.

**Formato de API**

```http
POST /collection/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de la conexión de flujo continuo creada anteriormente. |

**Solicitud**

Envíe la siguiente solicitud para introducir datos a la entrada de datos con validación asíncrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | El cuerpo JSON de los datos que desea introducir. |

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
    "syncValidation": {
        "skipped": true
    }
}
```

Tenga en cuenta cómo la respuesta indica que la validación sincrónica se ha omitido, ya que no se ha solicitado explícitamente.

## Apéndice

Esta sección contiene información sobre el significado de los distintos códigos de estado para las respuestas de ingesta de datos.

### Códigos de estado

| Código de estado | Lo que significa |
| ----------- | ------------- |
| 200 | Correcto. Para la validación sincrónica, significa que ha superado las comprobaciones de validación. Para la validación asincrónica, significa que solo ha recibido correctamente el mensaje. Los usuarios pueden averiguar el estado final del mensaje observando el conjunto de datos. |
| 400 | Error. Hay un problema con su solicitud. Se recibe un mensaje de error con más detalles de los servicios de validación de streaming. |
| 401 | Error. Su solicitud no está autorizada: deberá solicitarla con un token de portador. Para obtener más información sobre cómo solicitar acceso, vea este [tutorial](https://www.adobe.com/go/platform-api-authentication-en) o esta [publicación de blog](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Error. Hay un error interno del sistema. |
| 501 | Error. Esto significa que la validación sincrónica **no** es compatible con esta ubicación. |
| 503 | Error. El servicio no está disponible en este momento. Los clientes deben intentarlo al menos tres veces con una estrategia de retroceso exponencial. |
