---
keywords: Experience Platform;inicio;temas populares;conexión de transmisión;crear conexión de transmisión;guía de API;tutorial;crear una conexión de transmisión;transmisión de flujo continuo;ingestión;
solution: Experience Platform
title: Creación de una conexión de flujo mediante la API
topic: tutorial
type: Tutorial
description: Este tutorial le ayudará a empezar a utilizar las API de inserción de flujo continuo, que forman parte de las API de servicio de inserción de datos de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5932d63820dd0e50acccd18573746061232e099e
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 2%

---


# Creación de una conexión de flujo mediante la API

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos a fin de crear una conexión de flujo mediante la API de servicio de flujo.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):: El marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.

Las siguientes secciones proporcionan información adicional que debe conocer para realizar llamadas a las API de inserción de flujo continuo.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../../../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Crear una conexión

Una conexión especifica el origen y contiene la información necesaria para que el flujo sea compatible con las API de inserción de flujo continuo. Al crear una conexión, tiene la opción de crear una conexión no autenticada y autenticada.

### Conexión no autenticada

Las conexiones no autenticadas son la conexión de flujo estándar que se puede crear cuando se desea transmitir datos a la plataforma.

**Formato API**

```http
POST /flowservice/connections
```

**Solicitud**

Para crear una conexión de flujo continuo, el ID del proveedor y el ID de especificación de conexión deben proporcionarse como parte de la solicitud del POST. El identificador del proveedor es `521eee4d-8cbe-4906-bb48-fb6bd4450033` y el identificador de especificación de conexión es `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.sourceId` | ID de la conexión de flujo que desea crear. |
| `auth.params.dataType` | Tipo de datos para la conexión de flujo continuo. Este valor debe ser `xdm`. |
| `auth.params.name` | Nombre de la conexión de flujo que desea crear. |
| `connectionSpec.id` | Especificación de conexión `id` para conexiones de flujo continuo. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El `id` de la conexión recién creada. Esto se denominará `{CONNECTION_ID}`. |
| `etag` | Identificador asignado a la conexión, que especifica la revisión de la conexión. |

### Conexión autenticada

Las conexiones autenticadas deben utilizarse cuando necesite diferenciar entre registros procedentes de fuentes de confianza y no de confianza. Los usuarios que deseen enviar información con Información de identificación personal (PII) deben crear una conexión autenticada al transmitir información a la plataforma.

**Formato API**

```http
POST /flowservice/connections
```

**Solicitud**

Para crear una conexión de flujo continuo, el ID del proveedor y el ID de especificación de conexión deben proporcionarse como parte de la solicitud del POST. El identificador del proveedor es `521eee4d-8cbe-4906-bb48-fb6bd4450033` y el identificador de especificación de conexión es `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.sourceId` | ID de la conexión de flujo que desea crear. |
| `auth.params.dataType` | Tipo de datos para la conexión de flujo continuo. Este valor debe ser `xdm`. |
| `auth.params.name` | Nombre de la conexión de flujo que desea crear. |
| `auth.params.authenticationRequired` | El parámetro que especifica que la conexión de flujo creada |
| `connectionSpec.id` | Especificación de conexión `id` para conexiones de flujo continuo. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El `id` de la conexión recién creada. Esto se denominará `{CONNECTION_ID}`. |
| `etag` | Identificador asignado a la conexión, que especifica la revisión de la conexión. |

## Obtener URL del extremo de flujo continuo

Con la conexión creada, ahora puede recuperar la URL del extremo de flujo continuo.

**Formato API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` de la conexión que creó anteriormente. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la conexión solicitada. La dirección URL del extremo de flujo se crea automáticamente con la conexión y se puede recuperar con el valor `inletUrl`.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión HTTP de flujo continuo que le permite utilizar el extremo de flujo para transferir datos a Platform. Para obtener instrucciones para crear una conexión de flujo continuo en la interfaz de usuario, lea el [tutorial de creación de una conexión de flujo](../../../ui/create/streaming/http.md).

Para aprender a transmitir datos a la plataforma, lea el tutorial sobre [transmisión de datos de series temporales](../../../../../ingestion/tutorials/streaming-time-series-data.md) o el tutorial sobre [transmisión de datos de registros](../../../../../ingestion/tutorials/streaming-record-data.md).

## Apéndice

Esta sección proporciona información adicional sobre la creación de conexiones de flujo mediante la API.

### Envío de mensajes a una conexión de flujo autenticada

Si una conexión de flujo continuo tiene habilitada la autenticación, el cliente deberá agregar el encabezado `Authorization` a su solicitud.

Si el encabezado `Authorization` no está presente o se envía un token de acceso no válido o caducado, se devolverá una respuesta HTTP 401 no autorizada, con una respuesta similar a la siguiente:

**Respuesta**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
