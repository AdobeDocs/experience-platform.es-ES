---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector HubSpot mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: 7aa6f85308bacb275bd6f3234d03530a621c1c02

---


# Creación de un conector HubSpot mediante la API de servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar la plataforma de experiencia con HubSpot.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a HubSpot mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con HubSpot, debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientId` | ID de cliente asociado a la aplicación HubSpot. |
| `clientSecret` | El secreto de cliente asociado a la aplicación HubSpot. |
| `accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `refreshToken` | El autentificador de actualización obtenido al autenticar inicialmente la integración de OAuth. |

Para obtener más información sobre cómo empezar, consulte este documento [de HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

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

## Buscar especificaciones de conexión

Para crear una conexión HubSpot, debe existir un conjunto de especificaciones de conexión HubSpot dentro del servicio de flujo. El primer paso para conectar Platform a HubSpot es recuperar estas especificaciones.

**Formato API**

Cada fuente disponible tiene su propio conjunto exclusivo de especificaciones de conexión para describir propiedades del conector, como los requisitos de autenticación. Si se envía una solicitud GET al extremo, se devolverán las especificaciones de conexión de todos los orígenes disponibles. `/connectionSpecs` También puede incluir la consulta `property=name=="hubspot"` para obtener información específica para HubSpot.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="hubspot"
```

**Solicitud**

La siguiente solicitud recupera las especificaciones de conexión para HubSpot.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="hubspot"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la especificación de conexión de HubSpot, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión para la API.

```json
{
    "items": [
        {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "name": "hubspot",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to HubSpot",
                        "properties": {
                            "clientId": {
                                "type": "string",
                                "description": "The client ID associated with your HubSpot application."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret associated with your HubSpot application.",
                                "format": "password"
                            },
                            "accessToken": {
                                "type": "string",
                                "description": "The access token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientId",
                            "clientSecret",
                            "accessToken",
                            "refreshToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Creación de una conexión para la API

Una conexión para la API especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión para la API por cuenta de HubSpot, ya que se puede usar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

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
| `auth.params.clientId` | ID de cliente asociado a la aplicación HubSpot. |
| `auth.params.clientSecret` | El secreto de cliente asociado a la aplicación HubSpot. |
| `auth.params.accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `auth.params.refreshToken` | El autentificador de actualización obtenido al autenticar inicialmente la integración de OAuth. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada para la API, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2eb9c78b-e8b8-4400-b9c7-8be8b86400b2",
    "etag": "\"05026cf5-0000-0200-0000-5e4c42920000\""
}
```

Siguiendo este tutorial, ha creado una conexión HubSpot con la API de servicio de flujo y ha obtenido el valor de ID único de la conexión. Este ID de conexión se puede utilizar en el siguiente tutorial cuando aprenda a [explorar sistemas CRM mediante la API](../../explore/crm.md)de servicio de flujo.