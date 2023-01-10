---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Configuración de especificaciones de autenticación para fuentes de autoservicio (SDK por lotes)
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# Configuración de especificaciones de autenticación para fuentes de autoservicio (SDK por lotes)

Las especificaciones de autenticación definen cómo los usuarios de Adobe Experience Platform pueden conectarse a su origen.

La variable `authSpec` contiene información sobre los parámetros de autenticación necesarios para conectar un origen a Platform. Cualquier fuente dada puede admitir varios tipos diferentes de autenticación.

## Especificaciones de autenticación

Las fuentes de autoservicio (SDK por lotes) admiten códigos de actualización de OAuth 2 y autenticación básica. Consulte las tablas siguientes para obtener instrucciones sobre el uso de un código de actualización de OAuth 2 y una autenticación básica

### Código de actualización de OAuth 2

El código de actualización de OAuth 2 permite el acceso seguro a una aplicación mediante la generación de un token de acceso temporal y un token de actualización. El token de acceso le permite acceder de forma segura a sus recursos sin tener que proporcionar otras credenciales, mientras que el token de actualización le permite generar un nuevo token de acceso, una vez que caduque el token de acceso.

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| Propiedad | Descripción | Ejemplo |
| --- | --- | --- |
| `authSpec.name` | Muestra el nombre del tipo de autenticación admitido. | `oAuth2-refresh-code` |
| `authSpec.type` | Define el tipo de autenticación que admite el origen. | `oAuth2-refresh-code` |
| `authSpec.spec` | Contiene información sobre el esquema, el tipo de datos y las propiedades de la autenticación. |
| `authSpec.spec.$schema` | Define el esquema utilizado para la autenticación. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define el tipo de datos del esquema. | `object` |
| `authSpec.spec.properties` | Contiene información sobre las credenciales utilizadas para la autenticación. |
| `authSpec.spec.properties.description` | Muestra una breve descripción de las credenciales. |
| `authSpec.spec.properties.type` | Define el tipo de datos de la credencial. | `string` |
| `authSpec.spec.properties.clientId` | El ID de cliente asociado a la aplicación. El ID de cliente se utiliza junto con el secreto de cliente para recuperar el token de acceso. |
| `authSpec.spec.properties.clientSecret` | El secreto de cliente asociado a la aplicación. El secreto de cliente se utiliza junto con el ID de cliente para recuperar el token de acceso. |
| `authSpec.spec.properties.accessToken` | El token de acceso autoriza su acceso seguro a su aplicación. |
| `authSpec.spec.properties.refreshToken` | El token de actualización se utiliza para generar un nuevo token de acceso, cuando caduca el token de acceso. |
| `authSpec.spec.properties.expirationDate` | Define la fecha de caducidad del token de acceso. |
| `authSpec.spec.properties.refreshTokenUrl` | Dirección URL utilizada para recuperar el token de actualización. |
| `authSpec.spec.properties.accessTokenUrl` | Dirección URL utilizada para recuperar el token de actualización. |
| `authSpec.spec.properties.requestParameterOverride` | Permite especificar parámetros de credencial que se deben anular al autenticarse. |
| `authSpec.spec.required` | Muestra las credenciales necesarias para autenticarse. | `accessToken` |

{style=&quot;table-layout:auto&quot;}


### Autenticación básica

La autenticación básica es un tipo de autenticación que le permite acceder a su aplicación mediante una combinación del nombre de usuario de su cuenta y la contraseña de su cuenta.

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| Propiedad | Descripción | Ejemplo |
| --- | --- | --- |
| `authSpec.name` | Muestra el nombre del tipo de autenticación admitido. | `Basic Authentication` |
| `authSpec.type` | Define el tipo de autenticación que admite el origen. | `BasicAuthentication` |
| `authSpec.spec` | Contiene información sobre el esquema, el tipo de datos y las propiedades de la autenticación. |
| `authSpec.spec.$schema` | Define el esquema utilizado para la autenticación. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define el tipo de datos del esquema. | `object` |
| `authSpec.spec.description` | Muestra información adicional específica para su tipo de autenticación. |
| `authSpec.spec.properties` | Contiene información sobre las credenciales utilizadas para la autenticación. |
| `authSpec.spec.properties.username` | El nombre de usuario de la cuenta asociado a su aplicación. |
| `authSpec.spec.properties.password` | La contraseña de la cuenta asociada a su aplicación. |
| `authSpec.spec.required` | Especifica los campos requeridos como valores obligatorios que se van a introducir en Platform. | `username` |

{style=&quot;table-layout:auto&quot;}

## Ejemplo de especificación de autenticación

A continuación se muestra un ejemplo de una especificación de autenticación completada mediante un [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) fuente.

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

## Pasos siguientes

Con las especificaciones de autenticación rellenadas, puede proceder a configurar las especificaciones de origen para la fuente que desea integrar en Platform. Consulte el documento en [configuración de especificaciones de origen](./sourcespec.md) para obtener más información.
