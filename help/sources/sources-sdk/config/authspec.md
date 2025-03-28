---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
title: Configuración de las especificaciones de autenticación para orígenes de autoservicio (SDK por lotes)
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 8517532f991413a239e0da890bf53b1bf5b621f0
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 3%

---

# Configuración de las especificaciones de autenticación para orígenes de autoservicio (SDK por lotes)

Las especificaciones de autenticación definen cómo los usuarios de Adobe Experience Platform pueden conectarse a su origen.

La matriz `authSpec` contiene información sobre los parámetros de autenticación necesarios para conectar un origen a Platform. Cualquier fuente determinada puede admitir varios tipos diferentes de autenticación.

## Especificaciones de autenticación

Fuentes de autoservicio (SDK por lotes) admite códigos de actualización de OAuth 2 y autenticación básica. Consulte las tablas siguientes para obtener instrucciones sobre el uso de un código de actualización de OAuth 2 y la autenticación básica

### Código de actualización de OAuth 2

Un código de actualización de OAuth 2 permite el acceso seguro a una aplicación mediante la generación de un token de acceso temporal y un token de actualización. El token de acceso le permite acceder de forma segura a sus recursos sin tener que proporcionar otras credenciales, mientras que el token de actualización le permite generar un nuevo token de acceso, una vez que caduque el token de acceso.

+++Ver ejemplo de código de actualización de OAuth 2

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
| `authSpec.type` | Define el tipo de autenticación admitida por el origen. | `oAuth2-refresh-code` |
| `authSpec.spec` | Contiene información sobre el esquema, el tipo de datos y las propiedades de la autenticación. |
| `authSpec.spec.$schema` | Define el esquema utilizado para la autenticación. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define el tipo de datos del esquema. | `object` |
| `authSpec.spec.properties` | Contiene información sobre las credenciales utilizadas para la autenticación. |
| `authSpec.spec.properties.description` | Muestra una breve descripción de la credencial. |
| `authSpec.spec.properties.type` | Define el tipo de datos de la credencial. | `string` |
| `authSpec.spec.properties.clientId` | El ID de cliente asociado con su aplicación. El ID de cliente se utiliza junto con el secreto de cliente para recuperar el token de acceso. |
| `authSpec.spec.properties.clientSecret` | Secreto de cliente asociado a la aplicación. El secreto de cliente se utiliza junto con su ID de cliente para recuperar el token de acceso. |
| `authSpec.spec.properties.accessToken` | El token de acceso autoriza el acceso seguro a la aplicación. |
| `authSpec.spec.properties.refreshToken` | El token de actualización se utiliza para generar un nuevo token de acceso cuando caduca el token de acceso. |
| `authSpec.spec.properties.expirationDate` | Define la fecha de caducidad del token de acceso. |
| `authSpec.spec.properties.refreshTokenUrl` | Dirección URL utilizada para recuperar el token de actualización. |
| `authSpec.spec.properties.accessTokenUrl` | Dirección URL utilizada para recuperar el token de actualización. |
| `authSpec.spec.properties.requestParameterOverride` | Permite especificar parámetros de credencial para anular al autenticarse. |
| `authSpec.spec.required` | Muestra las credenciales necesarias para autenticarse. | `accessToken` |

{style="table-layout:auto"}

+++

### Autenticación básica

La autenticación básica es un tipo de autenticación que le permite acceder a su aplicación mediante una combinación del nombre de usuario de la cuenta y la contraseña de la cuenta.

+++ Ver ejemplo de autenticación básica

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
| `authSpec.type` | Define el tipo de autenticación admitida por el origen. | `BasicAuthentication` |
| `authSpec.spec` | Contiene información sobre el esquema, el tipo de datos y las propiedades de la autenticación. |
| `authSpec.spec.$schema` | Define el esquema utilizado para la autenticación. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Define el tipo de datos del esquema. | `object` |
| `authSpec.spec.description` | Muestra más información específica del tipo de autenticación. |
| `authSpec.spec.properties` | Contiene información sobre las credenciales utilizadas para la autenticación. |
| `authSpec.spec.properties.username` | El nombre de usuario de la cuenta asociado con su aplicación. |
| `authSpec.spec.properties.password` | La contraseña de la cuenta asociada con su aplicación. |
| `authSpec.spec.required` | Especifica los campos requeridos como valores obligatorios para introducir en Experience Platform. | `username` |

{style="table-layout:auto"}

+++

### Autenticación de clave API {#api-key-authentication}

La autenticación de clave de API es un método seguro para acceder a las API al proporcionar una clave de API y otros parámetros de autenticación relevantes en las solicitudes. Según la información de API específica, puede enviar la clave de API como parte del encabezado de la solicitud, los parámetros de consulta o el cuerpo de la solicitud.

Los siguientes parámetros suelen ser necesarios al utilizar la autenticación de clave de API:

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `host` | cadena | No | La URL del recurso. |
| `authKey1` | cadena | Sí | La primera clave de autenticación necesaria para acceder a la API. Normalmente se envía en el encabezado de la solicitud o en los parámetros de consulta. |
| `authKey2` | cadena | Opcional | Una segunda clave de autenticación. Si es necesario, esta clave se utiliza a menudo para validar solicitudes aún más. |
| `authKeyN` | cadena | Opcional | Una variable de autenticación adicional que se puede utilizar según sea necesario, pero la API. |

{style="table-layout:auto"}

+++Ver autenticación de clave API

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### Comportamiento de autenticación

Puede usar el parámetro `restAttributes` para definir cómo se debe incluir la clave de API en la solicitud. Por ejemplo, en el ejemplo siguiente, el atributo `headerParamName` indica que `X-Auth-Key1` debe enviarse como encabezado.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

Cada clave de autenticación (como `authKey1`, `authKey2`, etc.) se puede asociar con `restAttributes` para dictar cómo se envían como solicitudes.

Si `authKey1` tiene `"headerParamName": "X-Auth-Key1"`. Esto significa que el encabezado de la solicitud debe incluir `X-Auth-Key:{YOUR_AUTH_KEY1}`. Además, el nombre de clave y `headerParamName` no tienen por qué ser necesariamente iguales. Por ejemplo:

* `authKey1` puede tener `headerParamName: X-Custom-Auth-Key`. Esto significa que el encabezado de la solicitud usará `X-Custom-Auth-Key` en lugar de `authKey1`.
* A la inversa, `authKey1` puede tener `headerParamName: authKey1`. Esto significa que el nombre del encabezado de la solicitud permanece sin cambios.

**Ejemplo de formato de API**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## Ejemplo de especificación de autenticación

A continuación se muestra un ejemplo de una especificación de autenticación completada mediante un origen [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md).

+++Ver ejemplo de especificación de autenticación

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

+++

## Pasos siguientes

Una vez rellenadas las especificaciones de autenticación, puede continuar con la configuración de las especificaciones de origen para el origen que desea integrar en Platform. Consulte el documento sobre [configuración de especificaciones de origen](./sourcespec.md) para obtener más información.
