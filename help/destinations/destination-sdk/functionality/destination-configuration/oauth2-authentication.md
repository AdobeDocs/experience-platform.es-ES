---
description: Esta página describe los distintos flujos de autenticación de OAuth 2 admitidos por el Destination SDK y proporciona instrucciones para configurar la autenticación OAuth 2 para su destino.
title: Autenticación OAuth 2
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 4%

---

# Autenticación OAuth 2

Destination SDK admite varios métodos de autenticación en el destino. Entre ellas está la opción de autenticarse en el destino mediante el uso de la variable [Marco de autenticación de OAuth 2](https://tools.ietf.org/html/rfc6749).

Esta página describe los distintos flujos de autenticación de OAuth 2 admitidos por el Destination SDK y proporciona instrucciones para configurar la autenticación OAuth 2 para su destino.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | No |

## Cómo añadir detalles de autenticación de OAuth 2 a la configuración de destino {#how-to-setup}

### Requisitos previos del sistema {#prerequisites}

Como primer paso, debe crear una aplicación en el sistema para Adobe Experience Platform o, de lo contrario, registrar un Experience Platform en el sistema. El objetivo es generar un ID de cliente y un secreto de cliente, que son necesarios para autenticar el Experience Platform en el destino. Como parte de esta configuración en su sistema, necesita las URL de redireccionamiento/rellamada de Adobe Experience Platform OAuth 2, que puede obtener de la lista siguiente.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>El paso para registrar una URL de redireccionamiento/rellamada para Adobe Experience Platform en su sistema solo es necesario para el [OAuth 2 con código de autorización](oauth2-authentication.md#authorization-code) tipo de concesión. Para los otros dos tipos de concesión admitidos (contraseña y credenciales de cliente), puede omitir este paso.

Al final de este paso, debe tener:
* Un ID de cliente;
* Un secreto de cliente;
* URL de devolución de llamada del Adobe (para la concesión de código de autorización).

### Qué debe hacer en Destination SDK {#to-do-in-destination-sdk}

Para configurar la autenticación de OAuth 2 para su destino en Experience Platform, debe añadir los detalles de OAuth 2 a la variable [configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md), en la sección `customerAuthenticationConfigurations` parámetro. Consulte [autenticación de cliente](../../functionality/destination-configuration/customer-authentication.md) para ver ejemplos detallados. A continuación, en esta página encontrará instrucciones específicas sobre qué campos debe agregar a la plantilla de configuración, según el tipo de concesión de autenticación de OAuth 2.

## Tipos de concesión de OAuth 2 compatibles {#oauth2-grant-types}

Experience Platform admite los tres tipos de concesión de OAuth 2 en la siguiente tabla. Si tiene una configuración personalizada de OAuth 2, Adobe puede admitirla con la ayuda de campos personalizados en su integración. Consulte las secciones de cada tipo de concesión para obtener más información.

>[!IMPORTANT]
>
>* Los parámetros de entrada se proporcionan tal como se indica en las secciones siguientes. Los sistemas Adobe-internos se conectan al sistema de autenticación de su plataforma y obtienen parámetros de salida, que se utilizan para autenticar al usuario y mantener la autenticación en su destino.
>* Los parámetros de entrada resaltados en negrita en la tabla son parámetros requeridos en el flujo de autenticación de OAuth 2. Los demás parámetros son opcionales. Hay otros parámetros de entrada personalizados que no se muestran aquí, pero que se describen en detalle en las secciones [Personalizar la configuración de OAuth 2](#customize-configuration) y [Actualización del token de acceso](#access-token-refresh).


| OAuth 2 Grant | Entradas | Salidas |
|---------|----------|---------|
| Código de autorización | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Una contraseña | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Credencial del cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

La tabla anterior enumera los campos que se utilizan en los flujos estándar de OAuth 2. Además de estos campos estándar, varias integraciones de socios pueden requerir entradas y salidas adicionales. Adobe ha diseñado un marco flexible de autenticación/autorización de OAuth 2 para el Destination SDK que puede gestionar variaciones del patrón de campos estándar anterior, mientras que admite un mecanismo para volver a generar automáticamente resultados no válidos, como tokens de acceso caducados.

La salida en todos los casos incluye un token de acceso, que el Experience Platform utiliza para autenticarse y mantener la autenticación en el destino.

El sistema que Adobe ha diseñado para la autenticación OAuth 2:
* Admite las tres subvenciones de OAuth 2 al mismo tiempo que se tienen en cuenta las variaciones que se producen en ellas, como campos de datos adicionales, llamadas de API no estándar y más.
* Admite tokens de acceso con valores de duración variables, ya sea 90 días, 30 minutos o cualquier otro valor de duración especificado.
* Admite flujos de autorización de OAuth 2 con o sin tokens de actualización.

## OAuth 2 con código de autorización {#authorization-code}

Si su destino admite un flujo de código de autorización de OAuth 2.0 estándar (lea la [Especificaciones de estándares RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) o una variación de él, consulte los campos opcionales y requeridos a continuación:

| OAuth 2 Grant | Entradas | Salidas |
|---------|----------|---------|
| Código de autorización | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Para configurar este método de autenticación para el destino, agregue las siguientes líneas a la configuración, cuando [crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authType` | Cadena | Utilice &quot;OAUTH2&quot;. |
| `grant` | Cadena | Utilice &quot;OAUTH2_AUTHORIZATION_CODE&quot;. |
| `accessTokenUrl` | Cadena | La URL de su lado, que emite los tokens de acceso y, opcionalmente, los tokens de actualización. |
| `authorizationUrl` | Cadena | La URL de su servidor de autorización, donde redirige al usuario para que inicie sesión en su aplicación. |
| `refreshTokenUrl` | Cadena | *Opcional.* La dirección URL de su lado, que emite tokens de actualización. A menudo, la variable `refreshTokenUrl` es igual que la variable `accessTokenUrl`. |
| `clientId` | Cadena | El ID de cliente que el sistema asigna a Adobe Experience Platform. |
| `clientSecret` | Cadena | El secreto del cliente que el sistema asigna a Adobe Experience Platform. |
| `scope` | Lista de cadenas | *Opcional*. Establezca el ámbito de lo que el token de acceso permite que el Experience Platform realice en los recursos. Ejemplo: &quot;leer, escribir&quot;. |

{style="table-layout:auto"}

## OAuth 2 con concesión de contraseña

Para la concesión de contraseña de OAuth 2 (lea la [Especificaciones de estándares RFC](https://tools.ietf.org/html/rfc6749#section-4.3)), el Experience Platform requiere el nombre de usuario y la contraseña del usuario. En el flujo de autenticación, el Experience Platform intercambia estas credenciales para un token de acceso y, opcionalmente, un token de actualización.
El Adobe utiliza las entradas estándar que se indican a continuación para simplificar la configuración de destino, con la capacidad de anular los valores:

| OAuth 2 Grant | Entradas | Salidas |
|---------|----------|---------|
| Una contraseña | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> No es necesario agregar ningún parámetro para `username` y `password` en la configuración siguiente. Al agregar `"grant": "OAUTH2_PASSWORD"` en la configuración de destino, el sistema solicitará al usuario que proporcione un nombre de usuario y una contraseña en la interfaz de usuario del Experience Platform cuando se autentique en el destino.

Para configurar este método de autenticación para el destino, agregue las siguientes líneas a la configuración, cuando [crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authType` | Cadena | Utilice &quot;OAUTH2&quot;. |
| `grant` | Cadena | Utilice &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | Cadena | La URL de su lado, que emite los tokens de acceso y, opcionalmente, los tokens de actualización. |
| `clientId` | Cadena | El ID de cliente que el sistema asigna a Adobe Experience Platform. |
| `clientSecret` | Cadena | El secreto del cliente que el sistema asigna a Adobe Experience Platform. |
| `scope` | Lista de cadenas | *Opcional*. Establezca el ámbito de lo que el token de acceso permite que el Experience Platform realice en los recursos. Ejemplo: &quot;leer, escribir&quot;. |

{style="table-layout:auto"}

## OAuth 2 con concesión de credenciales de cliente

Puede configurar una Credenciales de cliente de OAuth 2 (lea la [Especificaciones de estándares RFC](https://tools.ietf.org/html/rfc6749#section-4.4)), que admite las entradas y salidas estándar que se enumeran a continuación. Puede personalizar los valores. Consulte [Personalizar la configuración de OAuth 2](#customize-configuration) para obtener más información.

| OAuth 2 Grant | Entradas | Salidas |
|---------|----------|---------|
| Credenciales del cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Para configurar este método de autenticación para el destino, agregue las siguientes líneas a la configuración, cuando [crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authType` | Cadena | Utilice &quot;OAUTH2&quot;. |
| `grant` | Cadena | Utilice &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | Cadena | La dirección URL del servidor de autorización, que emite un token de acceso y un token de actualización opcional. |
| `refreshTokenUrl` | Cadena | *Opcional.* La dirección URL de su lado, que emite tokens de actualización. A menudo, la variable `refreshTokenUrl` es igual que la variable `accessTokenUrl`. |
| `clientId` | Cadena | El ID de cliente que el sistema asigna a Adobe Experience Platform. |
| `clientSecret` | Cadena | El secreto del cliente que el sistema asigna a Adobe Experience Platform. |
| `scope` | Lista de cadenas | *Opcional*. Establezca el ámbito de lo que el token de acceso permite que el Experience Platform realice en los recursos. Ejemplo: &quot;leer, escribir&quot;. |

{style="table-layout:auto"}

## Personalizar la configuración de OAuth 2 {#customize-configuration}

Las configuraciones descritas en las secciones anteriores describen las subvenciones estándar de OAuth 2. Sin embargo, el sistema diseñado por Adobe proporciona flexibilidad para que pueda utilizar parámetros personalizados para cualquier variación en la subvención de OAuth 2. Para personalizar la configuración estándar de OAuth 2, utilice la variable `authenticationDataFields` como se muestra en los ejemplos siguientes.

### Ejemplo 1: Uso `authenticationDataFields` para capturar información procedente de la respuesta de autenticación {#example-1}

En este ejemplo, una plataforma de destino tiene tokens de actualización que caducan después de una determinada cantidad de tiempo. En este caso, el socio configura la variable `refreshTokenExpiration` campo personalizado para obtener la caducidad del token de actualización del `refresh_token_expires_in` en la respuesta de API.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### Ejemplo 2: Uso `authenticationDataFields` para proporcionar un token de actualización especial {#example-2}

En este ejemplo, un socio configura su destino para proporcionar un token de actualización especial. Además, la fecha de caducidad de los tokens de acceso no se devuelve en la respuesta de API, por lo que pueden codificar mediante hardcode un valor predeterminado, en este caso 3600 segundos.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### Ejemplo 3: El usuario introduce el ID de cliente y el secreto de cliente cuando configura el destino {#example-3}

En este ejemplo, en lugar de crear un ID de cliente global y un secreto de cliente como se muestra en la sección [Requisitos previos del sistema](#prerequisites), el cliente debe introducir el ID de cliente, el secreto del cliente y el ID de cuenta (el ID que el cliente utiliza para iniciar sesión en el destino)

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



Puede utilizar los parámetros siguientes en `authenticationDataFields` para personalizar la configuración de OAuth 2:

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authenticationDataFields.name` | Cadena | Nombre del campo personalizado. |
| `authenticationDataFields.title` | Cadena | Título que se puede proporcionar para el campo personalizado. |
| `authenticationDataFields.description` | Cadena | Descripción del campo de datos personalizado que ha configurado. |
| `authenticationDataFields.type` | Cadena | Define el tipo del campo de datos personalizado. <br> Valores aceptados: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Booleano | Especifica si el campo de datos personalizado es necesario en el flujo de autenticación. |
| `authenticationDataFields.format` | Cadena | Al seleccionar `"format":"password"`, Adobe cifra el valor del campo de datos de autenticación. Cuando se usa con `"fieldType": "CUSTOMER"`, esto también oculta la entrada en la interfaz de usuario cuando el usuario escribe en el campo . |
| `authenticationDataFields.fieldType` | Cadena | Indica si la entrada proviene del socio (usted) o del usuario, cuando configuran el destino en Experience Platform. |
| `authenticationDataFields.value` | Cadena. Booleano. Número entero | El valor del campo de datos personalizado. El valor coincide con el tipo elegido de `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Cadena | Indica a qué campo de la ruta de respuesta de API se hace referencia. |

{style="table-layout:auto"}

## Actualización del token de acceso {#access-token-refresh}

Adobe ha diseñado un sistema que actualiza los tokens de acceso caducados sin requerir que el usuario vuelva a iniciar sesión en su plataforma. El sistema puede generar un nuevo token para que la activación en el destino continúe sin problemas para el cliente.

Para configurar la actualización de token de acceso, es posible que tenga que configurar una solicitud HTTP con plantilla que permita a Adobe obtener un nuevo token de acceso mediante un token de actualización. Si el token de acceso ha caducado, Adobe toma la solicitud de plantilla proporcionada por usted, añadiendo los parámetros proporcionados. Utilice la variable `accessTokenRequest` para configurar un mecanismo de actualización de token de acceso.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

Puede utilizar los parámetros siguientes en `accessTokenRequest` para personalizar el proceso de actualización de tokens:

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Cadena | En su lugar, utilice `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Cadena | <ul><li>Uso `PEBBLE_V1` si utiliza plantillas para el valor en `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Uso `NONE` si el valor del campo `accessTokenRequest.urlBasedDestination.url.value` es una constante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Cadena | Dirección URL donde el Experience Platform solicita el token de acceso. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Cadena | <ul><li>Uso `PEBBLE_V1` si utiliza plantillas para los valores de `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Uso `NONE` si el valor del campo `accessTokenRequest.httpTemplate.requestBody.value` es una constante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Cadena | Utilice el lenguaje de plantilla para personalizar los campos de la solicitud HTTP al extremo del token de acceso. Para obtener información sobre cómo utilizar la plantilla para personalizar campos, consulte la [plantillas, convenciones](#templating-conventions) para obtener más información. |
| `accessTokenRequest.httpTemplate.httpMethod` | Cadena | Especifica el método HTTP utilizado para llamar al extremo del token de acceso. En la mayoría de los casos, este valor es `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Cadena | Especifica el tipo de contenido de la llamada HTTP al extremo del token de acceso. <br> Por ejemplo: `application/x-www-form-urlencoded` o `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Cadena | Especifica si se deben agregar encabezados a la llamada HTTP al extremo del token de acceso. |
| `accessTokenRequest.responseFields.templatingStrategy` | Cadena | <ul><li>Uso `PEBBLE_V1` si utiliza plantillas para los valores de `accessTokenRequest.responseFields.value`.</li><li> Uso `NONE` si el valor del campo `accessTokenRequest.responseFields.value` es una constante. </li></li> |
| `accessTokenRequest.responseFields.value` | Cadena | Utilice el lenguaje de plantilla para acceder a los campos de la respuesta HTTP desde el extremo del token de acceso. Para obtener información sobre cómo utilizar la plantilla para personalizar campos, consulte la [plantillas, convenciones](#templating-conventions) para obtener más información. |
| `accessTokenRequest.validations.name` | Cadena | Indica el nombre que ha proporcionado para esta validación. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Cadena | <ul><li>Uso `PEBBLE_V1` si utiliza plantillas para los valores de `accessTokenRequest.validations.actualValue.value`.</li><li> Uso `NONE` si el valor del campo `accessTokenRequest.validations.actualValue.value` es una constante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Cadena | Utilice el lenguaje de plantilla para acceder a los campos de la respuesta HTTP. Para obtener información sobre cómo utilizar la plantilla para personalizar campos, consulte la [plantillas, convenciones](#templating-conventions) para obtener más información. |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Cadena | <ul><li>Uso `PEBBLE_V1` si utiliza plantillas para los valores de `accessTokenRequest.validations.expectedValue.value`.</li><li> Uso `NONE` si el valor del campo `accessTokenRequest.validations.expectedValue.value` es una constante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Cadena | Utilice el lenguaje de plantilla para acceder a los campos de la respuesta HTTP. Para obtener información sobre cómo utilizar la plantilla para personalizar campos, consulte la [plantillas, convenciones](#templating-conventions) para obtener más información. |

{style="table-layout:auto"}

## Plantillas, convenciones {#templating-conventions}

Según la personalización de la autenticación, es posible que deba acceder a los campos de datos en la respuesta de autenticación, como se muestra en la sección anterior. Para ello, familiarícese con el [Lenguaje de plantilla de guijarros](https://pebbletemplates.io/) utilizado por Adobe y consulte las convenciones de plantilla que se describen a continuación para personalizar su implementación de OAuth 2.


| Prefijo | Descripción | Ejemplo |
|---------|----------|---------|
| authData | Acceda al valor de cualquier campo de datos de cliente o socio. | ``{{ authData.accessToken }}`` |
| response.body | Cuerpo de respuesta HTTP | ``{{ response.body.access_token }}`` |
| response.status | Estado de respuesta HTTP | ``{{ response.status }}`` |
| response.headers | Encabezados de respuesta HTTP | ``{{ response.headers.server[0] }}`` |
| userContext | Acceso a información sobre el intento de autenticación actual | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora conoce los patrones de autenticación de OAuth 2 admitidos por Adobe Experience Platform y sabe cómo configurar su destino con compatibilidad con autenticación de OAuth 2. A continuación, puede configurar su destino compatible con OAuth 2 mediante Destination SDK. Lectura [Use el Destination SDK para configurar el destino](../../guides/configure-destination-instructions.md) para los pasos siguientes.
