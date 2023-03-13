---
description: Esta página describe todas las operaciones de API que puede realizar mediante el punto final de API /authoring/credentials.
title: Operaciones de API de extremo de credenciales
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 5%

---

# Operaciones de API de extremo de credenciales {#credentials}

>[!IMPORTANT]
>
>**Extremo de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página enumera y describe todas las operaciones de API que puede realizar con la variable `/authoring/credentials` Extremo de API.

Para obtener una descripción de la funcionalidad admitida por este extremo, lea:

* [Configuración de destino de streaming](destination-configuration.md) para la funcionalidad, puede configurar para destinos de flujo continuo.
* [Configuración de destino basada en archivos](file-based-destination-configuration.md) para la funcionalidad, puede configurar para destinos basados en archivos.

## Cuándo usar el `/credentials` Extremo de API {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, *no* necesita usar el `/credentials` Extremo de API. En su lugar, puede configurar la información de autenticación para su destino mediante el `customerAuthenticationConfigurations` parámetros del `/destinations` punto final. Leer [Configuración de autenticación](./authentication-configuration.md#when-to-use) para obtener más información.

Utilice este extremo de API y seleccione `PLATFORM_AUTHENTICATION` en el [configuración de destino](./destination-configuration.md#destination-delivery) si existe un sistema de autenticación global entre el Adobe y el destino y el [!DNL Platform] el cliente no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe crear un objeto de credenciales utilizando la variable `/credentials` Extremo de API.

## Introducción a las operaciones de la API de configuración de credenciales {#get-started}

Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Crear una configuración de credenciales {#create}

Puede crear una nueva configuración de credenciales realizando una solicitud de POST al `/authoring/credentials` punto final.

**Formato de API**

```http
POST /authoring/credentials
```

**Solicitud**

La siguiente solicitud crea una nueva configuración de credenciales, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por el `/authoring/credentials` punto final. Tenga en cuenta que no tiene que añadir todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `username` | Cadena | Nombre de usuario de inicio de sesión de configuración |
| `password` | Cadena | Contraseña de inicio de sesión de configuración de credenciales |
| `url` | Cadena | URL del proveedor de autorización |
| `clientId` | Cadena | ID de cliente de la credencial de cliente/aplicación |
| `clientSecret` | Cadena | Secreto de cliente de credenciales de cliente/aplicación |
| `accessToken` | Cadena | Token de acceso proporcionado por el proveedor de autorización |
| `expiration` | Cadena | Tiempo de vida del token de acceso |
| `refreshToken` | Cadena | Actualizar token proporcionado por el proveedor de autorización |
| `header` | Cadena | Cualquier encabezado necesario para la autorización. |
| `accessId` | Cadena | ID de acceso de Amazon S3 |
| `secretKey` | Cadena | Clave secreta de Amazon S3 |
| `sshKey` | Cadena | Clave SSH para SFTP con autenticación SSH |
| `tenant` | Cadena | inquilino de Azure Data Lake Storage |
| `servicePrincipalId` | Cadena | ID principal del servicio de Azure para el almacenamiento de Azure Data Lake |
| `servicePrincipalKey` | Cadena | Clave principal del servicio de Azure para el almacenamiento de Azure Data Lake |
| `connectionString` | Cadena | Cadena de conexión de Azure Blob Storage |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

## Enumerar configuraciones de credenciales {#retrieve-list}

Puede recuperar una lista de todas las configuraciones de credenciales de su organización IMS realizando una solicitud de GET a la `/authoring/credentials` punto final.

**Formato de API**


```http
GET /authoring/credentials
```

**Solicitud**

La siguiente solicitud recuperará la lista de configuraciones de credenciales a las que tiene acceso, en función de la organización de IMS y la configuración de la zona protegida.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de configuraciones de credenciales a las que tiene acceso, en función del ID de organización de IMS y el nombre de la zona protegida que ha utilizado. Uno `instanceId` corresponde a la plantilla de una configuración de credenciales. La respuesta se trunca por su brevedad.

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

Puede actualizar una configuración de credenciales existente realizando una solicitud de PUT al `/authoring/credentials` y proporciona el ID de instancia de la configuración de credenciales que desea actualizar. En el cuerpo de la llamada, proporcione la configuración de credenciales actualizada.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Puede recuperar información detallada sobre una configuración de credenciales específica realizando una solicitud de GET al `/authoring/credentials` y proporciona el ID de instancia de la configuración de credenciales que desea actualizar.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Puede eliminar la configuración de credenciales especificada realizando una solicitud de DELETE al `/authoring/credentials` y proporciona el ID de la configuración de credenciales que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | El `id` de la configuración de credenciales que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

## Administración de errores de API

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cuándo usar el punto de conexión de credenciales y cómo establecer una configuración de credenciales mediante `/authoring/credentials` Punto final de API para `/authoring/destinations` punto final. Leer [cómo utilizar Destination SDK para configurar el destino](./configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración del destino.
