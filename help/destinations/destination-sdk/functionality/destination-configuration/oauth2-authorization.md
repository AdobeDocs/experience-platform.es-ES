---
description: En esta página se describen los distintos flujos de autorización de OAuth 2 admitidos por el Destination SDK y se proporcionan instrucciones para configurar la autorización de OAuth 2 para el destino.
title: Autorización de OAuth 2
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 7ba9971b44410e609c64f4dcf956a1976207353e
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 2%

---


# Autorización de OAuth 2

Destination SDK admite varios métodos de autorización para el destino. Entre ellas se encuentra la opción de autenticarse en el destino mediante el [marco de autorización de OAuth 2](https://tools.ietf.org/html/rfc6749).

En esta página se describen los distintos flujos de autorización de OAuth 2 admitidos por el Destination SDK y se proporcionan instrucciones para configurar la autorización de OAuth 2 para el destino.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK distinguen entre mayúsculas y minúsculas **1&rbrace;.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | No |

## Cómo añadir detalles de autorización de OAuth 2 a la configuración de destino {#how-to-setup}

### Requisitos previos en el sistema {#prerequisites}

Como primer paso, debe crear una aplicación en el sistema para Adobe Experience Platform o, de lo contrario, registrar un Experience Platform en el sistema. El objetivo es generar un ID de cliente y un secreto de cliente, que son necesarios para autenticar al Experience Platform en el destino.

Como parte de esta configuración en su sistema, necesita las URL de redireccionamiento/llamada de retorno de OAuth 2 de Adobe Experience Platform, que puede obtener de la lista siguiente.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>El paso para registrar una URL de redireccionamiento/llamada de retorno para Adobe Experience Platform en su sistema solo es necesario para el tipo de concesión [OAuth 2 con código de autorización](#authorization-code). Para los otros dos tipos de concesión admitidos (contraseña y credenciales de cliente), puede omitir este paso.

Al final de este paso, debería tener:
* Un ID de cliente;
* Un secreto de cliente;
* URL de devolución de llamada de Adobe (para la concesión del código de autorización).

### Qué debe hacer en Destination SDK {#to-do-in-destination-sdk}

Para configurar la autorización de OAuth 2 para su destino en Experience Platform, debe agregar los detalles de OAuth 2 a la [configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md), en el parámetro `customerAuthenticationConfigurations`. Consulte [autenticación de cliente](../../functionality/destination-configuration/customer-authentication.md) para ver ejemplos detallados. A continuación, en esta página, se proporcionan instrucciones específicas sobre qué campos debe añadir a la plantilla de configuración, según el tipo de concesión de autorización de OAuth 2.

## Tipos de concesión de OAuth 2 admitidos {#oauth2-grant-types}

El Experience Platform admite los tres tipos de concesión de OAuth 2 que aparecen en la siguiente tabla. Si tiene una configuración de OAuth 2 personalizada, Adobe puede admitirla con la ayuda de campos personalizados en la integración. Consulte las secciones de cada tipo de concesión para obtener más información.

>[!IMPORTANT]
>
>* Proporcione los parámetros de entrada como se indica en las secciones siguientes. Los sistemas internos del Adobe se conectan al sistema de autorización de su plataforma y obtienen parámetros de salida, que se utilizan para autenticar al usuario y mantener la autorización en su destino.
>* Los parámetros de entrada resaltados en negrita en la tabla son parámetros obligatorios en el flujo de autorización de OAuth 2. Los demás parámetros son opcionales. Hay otros parámetros de entrada personalizados que no se muestran aquí, pero que se describen en detalle en las secciones [Personalizar la configuración de OAuth 2](#customize-configuration) y [Actualización de token de acceso](#access-token-refresh).

| Concesión de OAuth 2 | Entradas | Salidas |
|---------|----------|---------|
| Código de autorización | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>token de acceso</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Contraseña | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li><li><b>nombre de usuario</b></li><li><b>contraseña</b></li></ul> | <ul><li><b>token de acceso</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Credenciales del cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>token de acceso</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

En la tabla anterior se enumeran los campos que se utilizan en los flujos de OAuth 2 estándar. Además de estos campos estándar, varias integraciones de socios pueden requerir entradas y salidas adicionales. El Adobe ha diseñado un marco de autorización de OAuth 2 flexible para Destination SDK que puede gestionar variaciones del patrón de campos estándar anterior y, al mismo tiempo, admitir un mecanismo para regenerar automáticamente salidas no válidas, como tokens de acceso caducados.

La salida en todos los casos incluye un token de acceso, que el Experience Platform utiliza para autenticar y mantener la autorización en el destino.

El sistema que el Adobe ha diseñado para la autorización de OAuth 2:
* Admite las tres concesiones de OAuth 2, teniendo en cuenta cualquier variación en ellas, como campos de datos adicionales, llamadas de API no estándar y más.
* Admite tokens de acceso con distintos valores de duración, ya sea 90 días, 30 minutos o cualquier otro valor de duración especificado.
* Admite flujos de autorización de OAuth 2 con o sin tokens de actualización.

## OAuth 2 con código de autorización {#authorization-code}

Si su destino admite un flujo de código de autorización de OAuth 2.0 estándar (lea las [especificaciones de estándares RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) o una variación de este, consulte los campos obligatorios y opcionales que aparecen a continuación:

| Concesión de OAuth 2 | Entradas | Salidas |
|---------|----------|---------|
| Código de autorización | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>token de acceso</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Para configurar este método de autorización para su destino, agregue las siguientes líneas a su configuración cuando [cree una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `accessTokenUrl` | Cadena | La dirección URL del sitio, que emite tokens de acceso y, opcionalmente, tokens de actualización. |
| `authorizationUrl` | Cadena | La URL del servidor de autorización, donde redirige al usuario para que inicie sesión en la aplicación. |
| `refreshTokenUrl` | Cadena | *Opcional.*: la dirección URL de su lado que emite tokens de actualización. A menudo, `refreshTokenUrl` es el mismo que `accessTokenUrl`. |
| `clientId` | Cadena | El ID de cliente que el sistema asigna a Adobe Experience Platform. |
| `clientSecret` | Cadena | Secreto de cliente que el sistema asigna a Adobe Experience Platform. |
| `scope` | Lista de cadenas | *Opcional*. Establezca el ámbito de lo que el token de acceso permite que Experience Platform realice en los recursos. Ejemplo: &quot;leer, escribir&quot;. |

{style="table-layout:auto"}

## OAuth 2 con concesión de contraseña

Para la concesión de contraseña de OAuth 2 (lea las [especificaciones de los estándares RFC](https://tools.ietf.org/html/rfc6749#section-4.3)), el Experience Platform requiere el nombre de usuario y la contraseña del usuario. En el flujo de autorización, Experience Platform intercambia estas credenciales por un token de acceso y, opcionalmente, un token de actualización.
Adobe utiliza las entradas estándar siguientes para simplificar la configuración de destino, con la capacidad de anular los valores:

| Concesión de OAuth 2 | Entradas | Salidas |
|---------|----------|---------|
| Contraseña | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li><li><b>nombre de usuario</b></li><li><b>contraseña</b></li></ul> | <ul><li><b>token de acceso</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> No es necesario que agregue ningún parámetro para `username` y `password` en la configuración siguiente. Cuando agregue `"grant": "OAUTH2_PASSWORD"` a la configuración de destino, el sistema solicitará al usuario que proporcione un nombre de usuario y una contraseña en la interfaz de usuario del Experience Platform cuando se autentique en el destino.

Para configurar este método de autorización para su destino, agregue las siguientes líneas a su configuración cuando [cree una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `accessTokenUrl` | Cadena | La dirección URL del sitio, que emite tokens de acceso y, opcionalmente, tokens de actualización. |
| `clientId` | Cadena | El ID de cliente que el sistema asigna a Adobe Experience Platform. |
| `clientSecret` | Cadena | Secreto de cliente que el sistema asigna a Adobe Experience Platform. |
| `scope` | Lista de cadenas | *Opcional*. Establezca el ámbito de lo que el token de acceso permite que Experience Platform realice en los recursos. Ejemplo: &quot;leer, escribir&quot;. |

{style="table-layout:auto"}

## OAuth 2 con concesión de credenciales de cliente

Puede configurar un destino de credenciales de cliente de OAuth 2 (lea las [especificaciones de estándares RFC](https://tools.ietf.org/html/rfc6749#section-4.4)), que admita las entradas y salidas estándar que se enumeran a continuación. Tiene la capacidad de personalizar los valores. Consulte [Personalizar la configuración de OAuth 2](#customize-configuration) para obtener más información.

| Concesión de OAuth 2 | Entradas | Salidas |
|---------|----------|---------|
| Credenciales del cliente | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ámbito</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>token de acceso</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Para configurar este método de autorización para su destino, agregue las siguientes líneas a su configuración cuando [cree una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `refreshTokenUrl` | Cadena | *Opcional.*: la dirección URL de su lado que emite tokens de actualización. A menudo, `refreshTokenUrl` es el mismo que `accessTokenUrl`. |
| `clientId` | Cadena | El ID de cliente que el sistema asigna a Adobe Experience Platform. |
| `clientSecret` | Cadena | Secreto de cliente que el sistema asigna a Adobe Experience Platform. |
| `scope` | Lista de cadenas | *Opcional*. Establezca el ámbito de lo que el token de acceso permite que Experience Platform realice en los recursos. Ejemplo: &quot;leer, escribir&quot;. |

{style="table-layout:auto"}

## Personalizar la configuración de OAuth 2 {#customize-configuration}

Las configuraciones descritas en las secciones anteriores describen concesiones de OAuth 2 estándar. Sin embargo, el sistema diseñado por Adobe proporciona flexibilidad para que pueda utilizar parámetros personalizados para cualquier variación en la concesión de OAuth 2. Para personalizar la configuración estándar de OAuth 2, utilice los parámetros `authenticationDataFields`, como se muestra en los ejemplos siguientes.

### Ejemplo 1: Usar `authenticationDataFields` para capturar información proveniente de la respuesta de autorización {#example-1}

En este ejemplo, una plataforma de destino tiene tokens de actualización que caducan después de una determinada cantidad de tiempo. En este caso, el socio configura el campo personalizado `refreshTokenExpiration` para obtener la caducidad del token de actualización del campo `refresh_token_expires_in` en la respuesta de la API.

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

### Ejemplo 2: Usar `authenticationDataFields` para proporcionar un token de actualización especial {#example-2}

En este ejemplo, un socio configura su destino para proporcionar un token de actualización especial. Además, la fecha de caducidad de los tokens de acceso no se devuelve en la respuesta de la API para que puedan codificar un valor predeterminado, en este caso de 3600 segundos.

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

En este ejemplo, en lugar de crear un ID de cliente global y un secreto de cliente, como se muestra en la sección [Requisitos previos de su sistema](#prerequisites), el cliente debe especificar el ID de cliente, el secreto de cliente y el ID de cuenta (el ID que utiliza el cliente para iniciar sesión en el destino)

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



Puede usar los siguientes parámetros en `authenticationDataFields` para personalizar la configuración de OAuth 2:

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authenticationDataFields.name` | Cadena | Nombre del campo personalizado. |
| `authenticationDataFields.title` | Cadena | Un título que puede proporcionar para el campo personalizado. |
| `authenticationDataFields.description` | Cadena | Descripción del campo de datos personalizados que ha configurado. |
| `authenticationDataFields.type` | Cadena | Define el tipo del campo de datos personalizados. <br> Valores aceptados: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Booleano | Especifica si el campo de datos personalizados es necesario en el flujo de autorización. |
| `authenticationDataFields.format` | Cadena | Al seleccionar `"format":"password"`, el Adobe cifra el valor del campo de datos de autorización. Cuando se utiliza con `"fieldType": "CUSTOMER"`, esto también oculta la entrada en la interfaz de usuario cuando el usuario escribe en el campo. |
| `authenticationDataFields.fieldType` | Cadena | Indica si la entrada procede del socio (usted) o del usuario, cuando configuran el destino en Experience Platform. |
| `authenticationDataFields.value` | Cadena. Booleano. Entero | El valor del campo de datos personalizado. El valor coincide con el tipo elegido de `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Cadena | Indica a qué campo de la ruta de respuesta de API se hace referencia. |

{style="table-layout:auto"}

## Actualización de token de acceso {#access-token-refresh}

El Adobe ha diseñado un sistema que actualiza los tokens de acceso caducados sin que sea necesario que el usuario vuelva a iniciar sesión en su plataforma. El sistema puede generar un nuevo token para que la activación en su destino continúe sin problemas para el cliente.

Para configurar la actualización de tokens de acceso, es posible que tenga que configurar una solicitud HTTP con plantilla que permita al Adobe obtener un nuevo token de acceso mediante un token de actualización. Si el token de acceso ha caducado, el Adobe toma la solicitud con plantilla proporcionada por usted y agrega los parámetros proporcionados. Utilice el parámetro `accessTokenRequest` para configurar un mecanismo de actualización de token de acceso.


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

Puede usar los siguientes parámetros en `accessTokenRequest` para personalizar el proceso de actualización de tokens:

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Cadena | Usar `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Cadena | <ul><li>Use `PEBBLE_V1` si usa plantillas para el valor de `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Use `NONE` si el valor del campo `accessTokenRequest.urlBasedDestination.url.value` es una constante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Cadena | Dirección URL donde el Experience Platform solicita el token de acceso. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Cadena | <ul><li>Use `PEBBLE_V1` si usa plantillas para los valores de `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Use `NONE` si el valor del campo `accessTokenRequest.httpTemplate.requestBody.value` es una constante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Cadena | Utilice el lenguaje de plantilla para personalizar los campos de la solicitud HTTP al extremo del token de acceso. Para obtener información sobre cómo usar la creación de plantillas para personalizar campos, consulte la sección [convenciones de creación de plantillas](#templating-conventions). |
| `accessTokenRequest.httpTemplate.httpMethod` | Cadena | Especifica el método HTTP utilizado para llamar al extremo del token de acceso. En la mayoría de los casos, este valor es `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Cadena | Especifica el tipo de contenido de la llamada HTTP al extremo de token de acceso. <br> Por ejemplo: `application/x-www-form-urlencoded` o `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Cadena | Especifica si se deben agregar encabezados a la llamada HTTP al extremo del token de acceso. |
| `accessTokenRequest.responseFields.templatingStrategy` | Cadena | <ul><li>Use `PEBBLE_V1` si usa plantillas para los valores de `accessTokenRequest.responseFields.value`.</li><li> Use `NONE` si el valor del campo `accessTokenRequest.responseFields.value` es una constante. </li></li> |
| `accessTokenRequest.responseFields.value` | Cadena | Utilice el lenguaje de plantilla para acceder a los campos de la respuesta HTTP desde el extremo del token de acceso. Para obtener información sobre cómo usar la creación de plantillas para personalizar campos, consulte la sección [convenciones de creación de plantillas](#templating-conventions). |
| `accessTokenRequest.validations.name` | Cadena | Indica el nombre proporcionado para esta validación. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Cadena | <ul><li>Use `PEBBLE_V1` si usa plantillas para los valores de `accessTokenRequest.validations.actualValue.value`.</li><li> Use `NONE` si el valor del campo `accessTokenRequest.validations.actualValue.value` es una constante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Cadena | Utilice el idioma de plantilla para acceder a los campos de la respuesta HTTP. Para obtener información sobre cómo usar la creación de plantillas para personalizar campos, consulte la sección [convenciones de creación de plantillas](#templating-conventions). |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Cadena | <ul><li>Use `PEBBLE_V1` si usa plantillas para los valores de `accessTokenRequest.validations.expectedValue.value`.</li><li> Use `NONE` si el valor del campo `accessTokenRequest.validations.expectedValue.value` es una constante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Cadena | Utilice el idioma de plantilla para acceder a los campos de la respuesta HTTP. Para obtener información sobre cómo usar la creación de plantillas para personalizar campos, consulte la sección [convenciones de creación de plantillas](#templating-conventions). |

{style="table-layout:auto"}

## Convenciones de plantilla {#templating-conventions}

Según la personalización de la autorización, es posible que deba acceder a los campos de datos de la respuesta de autorización, como se muestra en la sección anterior. Para ello, familiarícese con el [idioma de creación de plantillas Pebble](https://pebbletemplates.io/) que usa el Adobe y consulte las convenciones de creación de plantillas a continuación para personalizar su implementación de OAuth 2.


| Prefijo | Descripción | Ejemplo |
|---------|----------|---------|
| authData | Acceda al valor de cualquier campo de datos de socio o cliente. | ``{{ authData.accessToken }}`` |
| response.body | cuerpo de respuesta HTTP | ``{{ response.body.access_token }}`` |
| response.status | Estado de respuesta HTTP | ``{{ response.status }}`` |
| response.headers | Encabezados de respuesta HTTP | ``{{ response.headers.server[0] }}`` |
| userContext | Acceder a información sobre el intento de autorización actual | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authorization attempt `</li></ul> |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Al leer este artículo, ahora comprende los patrones de autorización de OAuth 2 admitidos por Adobe Experience Platform y sabe cómo configurar su destino con compatibilidad con la autorización de OAuth 2. A continuación, puede configurar el destino compatible con OAuth 2 mediante Destination SDK. Lee [Usar Destination SDK para configurar tu destino](../../guides/configure-destination-instructions.md) para los siguientes pasos.
