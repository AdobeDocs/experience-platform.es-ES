---
description: Esta página ejemplifica la llamada de API utilizada para actualizar una configuración de credenciales existente a través del Adobe Experience Platform Destination SDK.
title: Actualizar una configuración de credenciales
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 8%

---


# Actualizar una configuración de credenciales

>[!IMPORTANT]
>
>**Extremo de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para actualizar una configuración de credenciales existente mediante `/authoring/credentials` Extremo de API.

## Cuándo usar el `/credentials` Extremo de API {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, ***no*** necesita usar el `/credentials` Extremo de API. En su lugar, puede configurar la información de autenticación para su destino mediante el `customerAuthenticationConfigurations` parámetros del `/destinations` punto final.
> 
>Leer [Configuración de autenticación del cliente](../functionality/destination-configuration/customer-authentication.md) para obtener información detallada sobre los tipos de autenticación admitidos.

Utilice este extremo de API para crear una configuración de credenciales solo si hay un sistema de autenticación global entre el Adobe y la plataforma de destino, y la variable [!DNL Platform] el cliente no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe crear una configuración de credenciales de utilizando `/credentials` Extremo de API.

Al utilizar un sistema de autenticación global, debe establecer `"authenticationRule":"PLATFORM_AUTHENTICATION"` en el [envío de destino](../functionality/destination-configuration/destination-delivery.md) configuración, cuando [creación de una nueva configuración de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de credenciales {#get-started}

Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Actualizar una configuración de credenciales {#update}

Puede actualizar un [existente](create-credential-configuration.md) configuración de credenciales realizando una `PUT` solicitud a la `/authoring/credentials` punto final con la carga útil actualizada.

Para obtener una configuración de credenciales existente y sus correspondientes `{INSTANCE_ID}`, consulte el artículo sobre [recuperar una configuración de credenciales](retrieve-credential-configuration.md).

**Formato de API**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración de credenciales que desea actualizar. Para obtener una configuración de credenciales existente y sus correspondientes `{INSTANCE_ID}`, consulte [Recuperar una configuración de credenciales](retrieve-credential-configuration.md). |

Las siguientes solicitudes actualizan las configuraciones de credenciales existentes, definidas por los parámetros proporcionados en la carga útil.

Seleccione cada pestaña a continuación para ver la carga útil correspondiente.

>[!BEGINTABS]

>[!TAB Básico]

**Actualizar una configuración de credenciales básica**

+++Solicitud

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la configuración de credenciales actualizada.

+++

>[!TAB Amazon S3]

**Actualizar un [!DNL Amazon S3] configuración de credenciales**

+++Solicitud

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la configuración de credenciales actualizada.

+++

>[!TAB SSH]

**Actualizar un [!DNL SSH] configuración de credenciales**

+++Solicitud

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `sshKey` | Cadena | [!DNL SSH] clave para [!DNL SFTP] con [!DNL SSH] authentication |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la configuración de credenciales actualizada.

+++

>[!TAB Azure Data Lake Storage]

**Actualizar un [!DNL Azure Data Lake Storage] configuración de credenciales**

+++Solicitud

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `servicePrincipalId` | Cadena | [!DNL Azure Service Principal] ID para [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Cadena | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la configuración de credenciales actualizada.

+++

>[!TAB Almacenamiento de Azure Blob]

**Actualizar un [!DNL Azure Blob] configuración de credenciales**

+++Solicitud

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la configuración de credenciales actualizada.

+++

>[!ENDTABS]

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo actualizar una configuración de credenciales con la variable `/authoring/credentials` Extremo de API. Leer [cómo utilizar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración del destino.
