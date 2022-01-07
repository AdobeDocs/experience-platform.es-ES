---
description: En esta página se describen todas las operaciones de API que se pueden realizar con el extremo de API `/authoring/credentials`.
title: Operaciones de API de extremo de credenciales
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 5%

---

# Operaciones de API de extremo de credenciales {#credentials}

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

En esta página se enumeran y describen todas las operaciones de API que puede realizar mediante la `/authoring/credentials` extremo de API.

## Cuándo usar la variable `/credentials` Punto de conexión de API {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, usted *no* es necesario usar la variable `/credentials` extremo de API. En su lugar, puede configurar la información de autenticación de su destino mediante la variable `customerAuthenticationConfigurations` parámetros de la variable `/destinations` punto final. Lectura [Configuración de autenticación](./authentication-configuration.md#when-to-use) para obtener más información.

Utilice este extremo de API y seleccione `PLATFORM_AUTHENTICATION` en el [configuración de destino](./destination-configuration.md#destination-delivery) si hay un sistema de autenticación global entre el Adobe y el destino y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la variable `/credentials` extremo de API.

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## Introducción a las operaciones de API de configuración de credenciales {#get-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Crear una configuración de credenciales {#create}

Puede crear una nueva configuración de credenciales realizando una solicitud de POST al `/authoring/credentials` punto final.

**Formato de API**


```http
POST /authoring/credentials
```

**Solicitud**

La siguiente solicitud crea una nueva configuración de credenciales, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por la variable `/authoring/credentials` punto final. Tenga en cuenta que no es necesario agregar todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `username` | Cadena | nombre de usuario de inicio de sesión de configuración de credenciales |
| `password` | Cadena | contraseña de inicio de sesión de configuración de credenciales |
| `url` | Cadena | URL del proveedor de autorización |
| `clientId` | Cadena | ID de cliente de credenciales de cliente/aplicación |
| `clientSecret` | Cadena | Secreto de cliente de las credenciales de cliente/aplicación |
| `accessToken` | Cadena | Token de acceso proporcionado por el proveedor de autorización |
| `expiration` | Cadena | El tiempo de vida del token de acceso |
| `refreshToken` | Cadena | Actualizar token proporcionado por el proveedor de autorización |
| `header` | Cadena | Cualquier encabezado necesario para la autorización |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

## Enumerar configuraciones de credenciales {#retrieve-list}

Puede recuperar una lista de todas las configuraciones de credenciales para su organización IMS realizando una solicitud de GET al `/authoring/credentials` punto final.

**Formato de API**


```http
GET /authoring/credentials
```

**Solicitud**

La siguiente solicitud recuperará la lista de configuraciones de credenciales a las que tiene acceso, según la configuración de la organización y el entorno limitado de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de configuraciones de credenciales a las que tiene acceso, según el ID de organización de IMS y el nombre del simulador para pruebas que utilizó. One `instanceId` corresponde a la plantilla para una configuración de credenciales. La respuesta se trunca para su brevedad.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## Actualizar una configuración de credenciales existente {#update}

Puede actualizar una configuración de credenciales existente realizando una solicitud de PUT al `/authoring/credentials` y proporcionando el ID de instancia de la configuración de credenciales que desea actualizar. En el cuerpo de la llamada, proporcione la configuración de credenciales actualizada.

**Formato de API**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración de credenciales que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza una configuración de credenciales existente, configurada por los parámetros proporcionados en la carga útil.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```





## Recuperar una configuración de credenciales específica {#get}

Puede recuperar información detallada sobre una configuración de credenciales específica realizando una solicitud de GET al `/authoring/credentials` y proporcionando el ID de instancia de la configuración de credenciales que desea actualizar.

**Formato de API**


```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración de credenciales que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la configuración de credenciales especificada.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```


## Eliminar una configuración de credenciales específica {#delete}

Puede eliminar la configuración de credenciales especificada realizando una solicitud de DELETE al `/authoring/credentials` y proporcionando el ID de la configuración de credenciales que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | La variable `id` de la configuración de credenciales que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cuándo utilizar el extremo de credenciales y cómo configurar una configuración de credenciales utilizando la variable `/authoring/credentials` Punto final de API o `/authoring/destinations` punto final. Lectura [cómo usar Destination SDK para configurar el destino](./configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
