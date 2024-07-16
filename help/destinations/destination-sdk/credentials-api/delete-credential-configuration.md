---
description: Esta página ejemplifica la llamada de API utilizada para eliminar un Adobe Experience Platform Destination SDK de configuración de credenciales.
title: Eliminar una configuración de credenciales
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# Eliminar una configuración de credenciales

>[!IMPORTANT]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una configuración de credenciales mediante el extremo de API `/authoring/credentials`.

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

## Eliminar una configuración de credenciales {#delete}

Puede eliminar una configuración de credencial [existing](create-credential-configuration.md) realizando una solicitud `DELETE` al extremo `/authoring/credentials` con el `{INSTANCE_ID}`de la configuración de credencial que desea eliminar.

Para obtener una configuración de destino existente y sus `{INSTANCE_ID}` correspondientes, vea el artículo acerca de [recuperar una configuración de credencial](retrieve-credential-configuration.md).

**Formato de API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | El `ID` de la configuración de credenciales que desea eliminar. |

La siguiente solicitud elimina una configuración de credenciales definida por el parámetro `{INSTANCE_ID}`.

+++Solicitud

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

+++

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo eliminar una configuración de credenciales mediante el extremo de API `/authoring/credentials`. Lee [cómo usar el Destination SDK para configurar tu destino](../guides/configure-destination-instructions.md) para saber dónde encaja este paso en el proceso de configuración de tu destino.
