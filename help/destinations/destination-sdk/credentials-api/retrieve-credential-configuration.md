---
description: Esta página ejemplifica la llamada de API utilizada para recuperar una configuración de credenciales a través de Adobe Experience Platform Destination SDK.
title: Recuperar una configuración de credenciales
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Recuperar una configuración de credenciales

>[!IMPORTANT]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para recuperar una configuración de credenciales mediante el extremo de API `/authoring/credentials`.

## Cuándo usar el extremo de API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>En la mayoría de los casos, ***no*** necesita usar el extremo de la API `/credentials`. En su lugar, puede configurar la información de autenticación para su destino a través de los parámetros `customerAuthenticationConfigurations` del extremo `/destinations`.
> 
>Lea [Configuración de autenticación de cliente](../functionality/destination-configuration/customer-authentication.md) para obtener información detallada sobre los tipos de autenticación admitidos.

Use este extremo de API para crear una configuración de credenciales únicamente si existe un sistema de autenticación global entre Adobe y la plataforma de destino y el cliente [!DNL Experience Platform] no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe crear una configuración de credenciales utilizando el extremo de API `/credentials`.

Cuando use un sistema de autenticación global, debe establecer `"authenticationRule":"PLATFORM_AUTHENTICATION"` en la configuración de [envío de destino](../functionality/destination-configuration/destination-delivery.md) al [crear una nueva configuración de destino](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de credenciales {#get-started}

Antes de continuar, revisa la [guía de introducción](../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Recuperar una configuración de credenciales {#retrieve}

Puede recuperar una configuración de credencial [existing](create-credential-configuration.md) realizando una solicitud `GET` al extremo `/authoring/credentials`.

**Formato de API**

Utilice el siguiente formato de API para recuperar todas las configuraciones de credenciales de su cuenta.

```http
GET /authoring/credentials
```

Utilice el siguiente formato de API para recuperar una configuración de credenciales específica, definida por el parámetro `{INSTANCE_ID}`.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Las dos solicitudes siguientes recuperan todas las configuraciones de credenciales de su organización de IMS o una configuración de credenciales específica, en función de si pasa el parámetro `INSTANCE_ID` en la solicitud.

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

Una respuesta correcta devuelve el estado HTTP 200 con una lista de configuraciones de credenciales a las que tiene acceso, en función del [!DNL IMS Org ID] y el nombre de la zona protegida que ha utilizado. Un(a) `instanceId` corresponde a una configuración de credenciales.

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

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo recuperar detalles acerca de las configuraciones de credenciales mediante el extremo de API `/authoring/credentials`. Lee [cómo usar Destination SDK para configurar tu destino](../guides/configure-destination-instructions.md) para saber dónde encaja este paso en el proceso de configuración de tu destino.
