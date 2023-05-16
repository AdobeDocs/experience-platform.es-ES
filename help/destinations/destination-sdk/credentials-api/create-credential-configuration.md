---
description: Esta página ejemplifica la llamada de API utilizada para crear un Adobe Experience Platform Destination SDK de configuración de credenciales.
title: Crear una configuración de credencial
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 8%

---


# Crear una configuración de credencial

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para crear una configuración de credenciales utilizando la variable `/authoring/credentials` extremo de API.

## Cuándo usar la variable `/credentials` Punto de conexión de API {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, usted ***no*** es necesario usar la variable `/credentials` extremo de API. En su lugar, puede configurar la información de autenticación de su destino mediante la variable `customerAuthenticationConfigurations` parámetros de la variable `/destinations` punto final.
> 
>Lectura [Configuración de autenticación de cliente](../functionality/destination-configuration/customer-authentication.md) para obtener información detallada sobre los tipos de autenticación admitidos.

Utilice este extremo de API para crear una configuración de credenciales solo si existe un sistema de autenticación global entre el Adobe y la plataforma de destino, y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear una configuración de credenciales utilizando la variable `/credentials` extremo de API.

Al utilizar un sistema de autenticación global, debe establecer `"authenticationRule":"PLATFORM_AUTHENTICATION"` en el [envío de destino](../functionality/destination-configuration/destination-delivery.md) configuración, cuando [creación de una nueva configuración de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de credenciales {#get-started}

Antes de continuar, revise la [guía de introducción](../getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Crear una configuración de credenciales {#create}

Puede crear una nueva configuración de credenciales realizando una `POST` solicitud al `/authoring/credentials` punto final.

**Formato de API**

```http
POST /authoring/credentials
```

Las siguientes solicitudes crean nuevas configuraciones de credenciales, definidas por los parámetros proporcionados en la carga útil.

Seleccione cada pestaña a continuación para ver la carga útil correspondiente.

>[!BEGINTABS]

>[!TAB Básico]

**Crear una configuración de credencial básica**

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
| `username` | Cadena | Credenciales configuración nombre de usuario inicio de sesión |
| `password` | Cadena | Credenciales configuración contraseña de inicio de sesión |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!TAB Amazon S3]

**Cree un [!DNL Amazon S3] configuración de credenciales**

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
| `secretKey` | Cadena | [!DNL Amazon S3] clave secreta |

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
| `username` | Cadena | Credenciales configuración nombre de usuario inicio de sesión |
| `sshKey` | Cadena | Clave SSH para SFTP con autenticación SSH |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!TAB Almacenamiento de Azure Data Lake]

**Cree un [!DNL Azure Data Lake Storage] configuración de credenciales**

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
| `tenant` | Cadena | Inquilino de almacenamiento de Azure Data Lake |
| `servicePrincipalId` | Cadena | ID principal de Azure Service para el almacenamiento de Azure Data Lake |
| `servicePrincipalKey` | Cadena | Clave principal de Azure Service para el almacenamiento de Azure Data Lake |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de credenciales recién creada.

+++

>[!TAB Almacenamiento de Azure Blob]

**Cree un [!DNL Azure Blob Storage] configuración de credenciales**

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

## Gestión de errores de API {#error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cuándo utilizar el extremo de credenciales y cómo configurar una configuración de credenciales utilizando la variable `/authoring/credentials` Lectura de extremo de API [cómo usar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
