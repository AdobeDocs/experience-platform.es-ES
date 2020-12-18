---
keywords: Experience Platform;home;popular topics;hubspot;Hubspot
solution: Experience Platform
title: Creación de un conector HubSpot mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar Experience Platform a HubSpot.
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---


# Cree un conector [!DNL HubSpot] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL HubSpot] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] a [!DNL HubSpot].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse con éxito a [!DNL HubSpot] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL HubSpot], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientId` | El ID de cliente asociado a la aplicación [!DNL HubSpot]. |
| `clientSecret` | El secreto de cliente asociado con la aplicación [!DNL HubSpot]. |
| `accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `refreshToken` | El autentificador de actualización obtenido al autenticar inicialmente la integración de OAuth. |
| `connectionSpec` | Identificador único necesario para crear una conexión. El identificador de especificación de conexión para [!DNL HubSpot] es: `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Para obtener más información sobre cómo empezar, consulte este [documento de HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](../../../../../tutorials/authentication.md). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta [!DNL HubSpot], ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```https
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL HubSpot], se debe proporcionar su ID de especificación de conexión única como parte de la solicitud del POST. El identificador de especificación de conexión para [!DNL HubSpot] es `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.clientId` | El ID de cliente asociado a la aplicación [!DNL HubSpot]. |
| `auth.params.clientSecret` | El secreto de cliente asociado con la aplicación [!DNL HubSpot]. |
| `auth.params.accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `auth.params.refreshToken` | El autentificador de actualización obtenido al autenticar inicialmente la integración de OAuth. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Siguiendo este tutorial, ha creado una conexión [!DNL HubSpot] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este identificador de conexión en el siguiente tutorial cuando aprenda a [explorar los sistemas de automatización de mercadotecnia mediante la API de servicio de flujo](../../explore/marketing-automation.md).