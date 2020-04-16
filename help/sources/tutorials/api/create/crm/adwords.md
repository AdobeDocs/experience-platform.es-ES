---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector Google AdWords mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: a456dce58c32348c9e680cd672b71dd7bbdc1a04

---


# Creación de un conector Google AdWords mediante la API de servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar la plataforma de experiencia con Google AdWords (en adelante, &quot;AdWords&quot;).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a AdWords mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con AdWords, debe proporcionar valores para las siguientes propiedades de conexión:

| **Credencial** | **Descripción** |
| -------------- | --------------- |
| `clientCustomerID` | El ID de cliente asociado a Google AdWords de destinatario | account. |
| `developerToken` | Cadena utilizada para identificar a un desarrollador de la API AdWords. |
| `refreshToken` | El autentificador de actualización obtenido de Google utilizado para autorizar el acceso a AdWords. |
| `clientID` | ID de la aplicación utilizada para generar el token de actualización. |
| `clientSecret` | El secreto de cliente para la aplicación que se utiliza para generar el token de actualización. |

Para obtener más información sobre estos valores, consulte este documento [de](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

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

Para crear una conexión AdWords, debe existir un conjunto de especificaciones de conexión AdWords en el servicio de flujo. El primer paso para conectar Plataforma a AdWords es recuperar estas especificaciones.

**Formato API**

Cada fuente disponible tiene su propio conjunto exclusivo de especificaciones de conexión para describir propiedades del conector, como los requisitos de autenticación. Puede consultar las especificaciones de conexión de AdWords realizando una solicitud GET y utilizando parámetros de consulta.

El envío de una solicitud GET sin parámetros de consulta devolverá especificaciones de conexión para todos los orígenes disponibles. Puede incluir la consulta `property=name=="google-adwords"` para obtener información específica sobre AdWords.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="google-adwords"
```

**Solicitud**

La siguiente solicitud recupera la especificación de conexión de AdWords.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?{QUERY_PARAMS}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la especificación de conexión de AdWords, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión base.

```json
{
    "items": [
        {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "name": "google-adwords",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for google-adwords",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "clientCustomerID": {
                                "type": "string",
                                "description": "The Client customer ID of the AdWords account"
                            },
                            "developerToken": {
                                "type": "string",
                                "description": "The developer token associated with the manager account",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained from Google for authorizing access to AdWords",
                                "format": "password"
                            },
                            "clientId": {
                                "type": "string",
                                "description": "The client ID of the Google application used to acquire the refresh token"
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret of the google application used to acquire the refresh token",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientCustomerID",
                            "developerToken",
                            "refreshToken",
                            "clientId",
                            "clientSecret"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Creación de una conexión base

Una conexión base especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión de base por cuenta de AdWords, ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-adwords base connection",
        "description": "Base connection for google-adwords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.clientCustomerID` | ID de cliente de su cuenta de AdWords. |
| `auth.params.developerToken` | El testigo del programador de su cuenta de AdWords. |
| `auth.params.refreshToken` | El testigo de actualización de la cuenta de AdWords. |
| `auth.params.clientID` | ID de cliente de la cuenta de AdWords. |
| `auth.params.clientSecret` | El secreto de cliente de la cuenta de AdWords. |
| `connectionSpec.id` | Especificación de conexión `id` de la cuenta de AdWords recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada. Este ID es necesario para explorar los datos de AdWords en el siguiente tutorial.

```json
{
    "id": "e6ce1eab-416b-4a20-8e1e-ab416b1a206f",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base de AdWords mediante la API de servicio de flujo y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID de conexión base en el siguiente tutorial a medida que aprenda a [explorar sistemas CRM mediante la API](../../explore/crm.md)de servicio de flujo.
