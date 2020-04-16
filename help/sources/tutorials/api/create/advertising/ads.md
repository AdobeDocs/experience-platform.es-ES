---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de Google Ads mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: 950fa88ed6c9235bff98658763b662113bb76caa

---


# Creación de un conector de Google Ads mediante la API de servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar la plataforma de experiencia con Google Ads.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a la publicidad mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con los anuncios, debe proporcionar valores para las siguientes propiedades de conexión:

| **Credencial** | **Descripción** |
| -------------- | --------------- |
| ID del cliente | ID de cliente de la cuenta de anuncios. |
| Token de desarrollador | El testigo del programador asociado a la cuenta del administrador. |
| Actualizar token | El autentificador de actualización obtenido de Google para autorizar el acceso a los anuncios. |
| ID de cliente | ID de cliente de la aplicación de Google utilizada para adquirir el autentificador de actualización. |
| Secreto del cliente | El secreto de cliente de la aplicación de Google utilizado para adquirir el autentificador de actualización. |
| ID de especificación de conexión | Identificador único necesario para crear una conexión. El ID de especificación de conexión para Google Ads es: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Para obtener más información sobre estos valores, consulte este documento [de](https://developers.google.com/adwords/api/docs/guides/authentication)Google Ads.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de Google Ads, ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```https
POST /connections
```

**Solicitud**

Para crear una conexión de Google Ads, se debe proporcionar su ID de especificación de conexión única como parte de la solicitud POST. El ID de especificación de conexión para Google Ads es `221c7626-58f6-4eec-8ee2-042b0226f03b`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-ads connection",
        "description": "Connection for google-ads",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.clientCustomerID` | ID de cliente de su cuenta de anuncios. |
| `auth.params.developerToken` | El testigo de programadores de su cuenta de anuncios. |
| `auth.params.refreshToken` | El testigo de actualización de la cuenta de anuncios. |
| `auth.params.clientID` | ID de cliente de la cuenta de anuncios. |
| `auth.params.clientSecret` | El secreto de cliente de su cuenta de anuncios. |
| `connectionSpec.id` | ID de especificación de conexión de Google Ads: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de Google Ads mediante la API de servicio de flujo y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial a medida que aprenda a [explorar los sistemas de publicidad mediante la API](../../explore/advertising.md)de servicio de flujo.
