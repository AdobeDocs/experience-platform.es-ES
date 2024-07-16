---
description: Esta página ejemplifica la llamada de API utilizada para crear un Adobe Experience Platform Destination SDK de configuración de credenciales.
title: Crear una configuración de credenciales
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 6%

---

# Crear una configuración de credenciales

>[!IMPORTANT]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para crear una configuración de credenciales mediante el extremo de API `/authoring/credentials`.

## Cuándo usar el extremo de API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, ***no*** necesita usar el extremo de la API `/credentials`. En su lugar, puede configurar la información de autenticación para su destino a través de los parámetros `customerAuthenticationConfigurations` del extremo `/destinations`.
> 
>Lea [Configuración de autenticación de cliente](../functionality/destination-configuration/customer-authentication.md) para obtener información detallada sobre los tipos de autenticación admitidos.

Use este extremo de API para crear una configuración de credenciales únicamente si existe un sistema de autenticación global entre la Adobe y la plataforma de destino y el cliente [!DNL Platform] no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear una configuración de credenciales utilizando el extremo de API `/credentials`.

Cuando use un sistema de autenticación global, debe establecer `"authenticationRule":"PLATFORM_AUTHENTICATION"` en la configuración de [envío de destino](../functionality/destination-configuration/destination-delivery.md) al [crear una nueva configuración de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de credenciales {#get-started}

Antes de continuar, revisa la [guía de introducción](../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Crear una configuración de credenciales {#create}

Puede crear una nueva configuración de credenciales realizando una solicitud `POST` al extremo `/authoring/credentials`.

**Formato de API**

```http
POST /authoring/credentials
```

Las siguientes solicitudes crean nuevas configuraciones de credenciales, definidas por los parámetros proporcionados en la carga útil.

Seleccione cada pestaña a continuación para ver la carga útil correspondiente.

>[!BEGINTABS]

>[!TAB Básico]

**Crear una configuración de credenciales básica**

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `url` | Cadena | URL del proveedor de autorización |
| `username` | Cadena | Nombre de usuario de inicio de sesión de configuración |
| `password` | Cadena | Contraseña de inicio de sesión de configuración de credenciales |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!TAB Amazon S3]

**Crear una configuración de credencial [!DNL Amazon S3]**

+++**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `accessId` | Cadena | [!DNL Amazon S3] ID de acceso |
| `secretKey` | Cadena | clave secreta [!DNL Amazon S3] |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!TAB SSH]

**Crear una configuración de credenciales SSH**

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `username` | Cadena | Nombre de usuario de inicio de sesión de configuración |
| `sshKey` | Cadena | Clave SSH para SFTP con autenticación SSH |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!TAB Almacenamiento de Azure Data Lake]

**Crear una configuración de credencial [!DNL Azure Data Lake Storage]**

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `url` | Cadena | URL del proveedor de autorización |
| `tenant` | Cadena | inquilino de Azure Data Lake Storage |
| `servicePrincipalId` | Cadena | ID principal del servicio de Azure para el almacenamiento de Azure Data Lake |
| `servicePrincipalKey` | Cadena | Clave principal del servicio de Azure para el almacenamiento de Azure Data Lake |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!TAB Almacenamiento de blob de Azure]

**Crear una configuración de credencial [!DNL Azure Blob Storage]**

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| Parámetro | Tipo | Descripción |
| -------- | ----------- | ----------- |
| `connectionString` | Cadena | [!DNL Azure Blob Storage] cadena de conexión |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!ENDTABS]

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, sabe cuándo usar el extremo de credenciales y cómo establecer una configuración de credenciales mediante el extremo de API `/authoring/credentials`. Lea [cómo usar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para saber dónde encaja este paso en el proceso de configuración del destino.
