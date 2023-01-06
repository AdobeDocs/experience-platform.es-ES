---
keywords: Experience Platform;inicio;temas populares;flujo continuo;ingesta de transmisión;validación de ingesta de transmisión;validación;validación;validación de ingesta de transmisión;validación;validación sincrónica;validación sincrónica;validación asincrónica;validación asincrónica;validación asincrónica;
solution: Experience Platform
title: Validación de ingesta de flujos
type: Tutorial
description: 'La introducción por transmisión le permite cargar sus datos en Adobe Experience Platform mediante la transmisión de puntos de conexión en tiempo real. Las API de ingesta de transmisión admiten dos modos de validación: sincrónica y asincrónica.'
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 4%

---

# Validación de ingesta de transmisión

La introducción por transmisión le permite cargar sus datos en Adobe Experience Platform mediante la transmisión de puntos de conexión en tiempo real. Las API de ingesta de transmisión admiten dos modos de validación: sincrónica y asincrónica.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): Uno de los métodos mediante los cuales se pueden enviar datos a [!DNL Experience Platform].

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidas las pertenecientes al [!DNL Schema Registry], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

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

La validación sincrónica es un método de validación que proporciona información inmediata sobre el motivo del error de ingesta. Sin embargo, al producirse un error, los registros en los que se ha producido un error en la validación se pierden e impiden que se envíen de forma descendente. Como resultado, la validación sincrónica solo debe utilizarse durante el proceso de desarrollo. Al realizar la validación sincrónica, se informa a los autores de llamadas del resultado de la validación XDM y, si ha fallado, del motivo del error.

De forma predeterminada, la validación sincrónica no está activada. Para habilitarlo, debe pasar el parámetro de consulta opcional `syncValidation=true` al realizar llamadas de API. Además, la validación sincrónica actualmente solo está disponible si el punto final del flujo está en el centro de datos de VA7.

>[!NOTE]
>
>La variable `syncValidation` El parámetro de consulta solo está disponible para el extremo de mensaje único y no se puede usar para el extremo de lote.

Si un mensaje falla durante la validación sincrónica, el mensaje no se escribirá en la cola de salida, lo que proporciona comentarios inmediatos a los usuarios.

>[!NOTE]
>
>Es posible que los cambios del esquema no estén disponibles inmediatamente, ya que los cambios se almacenan en la caché. Espere hasta quince minutos para que la caché se actualice.

**Formato de API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | La variable `id` de la conexión de flujo continuo creada anteriormente. |

**Solicitud**

Envíe la siguiente solicitud para introducir datos en la entrada de datos con validación sincrónica:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | El cuerpo JSON de los datos que desea introducir. |

**Respuesta**

Con la validación sincrónica activada, una respuesta correcta incluye los errores de validación encontrados en su carga útil:

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

La respuesta anterior enumera cuántas violaciones de esquema se encontraron y cuáles fueron las violaciones. Por ejemplo, esta respuesta indica que las claves `workEmail` y `person` no se han definido en el esquema y, por lo tanto, no se permiten. También marca el valor de `_id` como incorrecto, ya que el esquema esperaba un `string`, pero un `long` en su lugar. Tenga en cuenta que una vez que se encuentren cinco errores, el servicio de validación **stop** procesar ese mensaje. Sin embargo, se seguirán analizando otros mensajes.

## Validación asincrónica

La validación asíncrona es un método de validación que no proporciona comentarios inmediatos. En su lugar, los datos se envían a un lote con errores en [!DNL Data Lake] para evitar la pérdida de datos. Estos datos fallidos se pueden recuperar posteriormente para su posterior análisis y reproducción. Este método debe utilizarse en la producción. A menos que se solicite lo contrario, la ingesta de flujo continuo funciona en modo de validación asincrónica.

**Formato de API**

```http
POST /collection/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | La variable `id` de la conexión de flujo continuo creada anteriormente. |

**Solicitud**

Envíe la siguiente solicitud para introducir datos en la entrada de datos con validación asíncrona:

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

Con la validación asíncrona habilitada, una respuesta correcta devuelve lo siguiente:

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

Esta sección contiene información sobre qué significan los distintos códigos de estado para las respuestas de ingesta de datos.

### Códigos de estado

| Código de estado | Lo que significa |
| ----------- | ------------- |
| 200 | Correcto. Para la validación sincrónica, significa que ha pasado las comprobaciones de validación. Para la validación asincrónica, significa que solo ha recibido el mensaje correctamente. Los usuarios pueden averiguar el estado final del mensaje observando el conjunto de datos. |
| 400 | Error. Hay algo mal en tu solicitud. Se recibe un mensaje de error con más detalles de los servicios de validación de flujo continuo. |
| 401 | Error. Su solicitud no está autorizada: deberá solicitarla con un token al portador. Para obtener más información sobre cómo solicitar acceso, consulte esta [tutorial](https://www.adobe.com/go/platform-api-authentication-en) o [publicación de blog](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Error. Hay un error interno del sistema. |
| 501 | Error. Esto significa que la validación sincrónica es **not** compatible con esta ubicación. |
| 503 | Error. El servicio no está disponible actualmente. Los clientes deben volver a intentarlo al menos tres veces usando una estrategia exponencial de back-off. |
