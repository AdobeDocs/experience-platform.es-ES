---
description: Esta página ejemplifica la llamada de API utilizada para recuperar una configuración de credenciales a través del Adobe Experience Platform Destination SDK.
title: Recuperar una configuración de credenciales
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---


# Recuperar una configuración de credenciales

>[!IMPORTANT]
>
>**Extremo de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para recuperar una configuración de credenciales mediante `/authoring/credentials` Extremo de API.

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

## Recuperar una configuración de credenciales {#retrieve}

Puede recuperar un [existente](create-credential-configuration.md) configuración de credenciales realizando una `GET` solicitud a la `/authoring/credentials` punto final.

**Formato de API**

Utilice el siguiente formato de API para recuperar todas las configuraciones de credenciales de su cuenta.

```http
GET /authoring/credentials
```

Utilice el siguiente formato de API para recuperar una configuración de credenciales específica, definida por la variable `{INSTANCE_ID}` parámetro.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Las dos solicitudes siguientes recuperan todas las configuraciones de credenciales de la organización IMS o una configuración de credenciales específica, en función de si pasa la variable `INSTANCE_ID` en la solicitud.

Seleccione cada pestaña a continuación para ver la carga útil correspondiente.

>[!BEGINTABS]

>[!TAB Recuperar todas las configuraciones de credenciales]

+++Solicitud

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con una lista de configuraciones de credenciales a las que tiene acceso, en función de la variable [!DNL IMS Org ID] y el nombre de la zona protegida que ha utilizado. Uno `instanceId` corresponde a una configuración de credenciales.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB Recuperar una configuración de credenciales específica]

+++Solicitud

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración de credenciales que desea recuperar. |

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con los detalles de la configuración de credenciales correspondientes a `instanceId` proporcionados en la solicitud.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo recuperar detalles sobre las configuraciones de credenciales mediante el `/authoring/credentials` Extremo de API. Leer [cómo utilizar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración del destino.
