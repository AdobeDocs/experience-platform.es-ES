---
description: Esta página ejemplifica la llamada de API utilizada para eliminar una configuración de servidor de destino existente a través de Adobe Experience Platform Destination SDK.
title: Eliminar una configuración de servidor de destino
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---

# Eliminar una configuración de servidor de destino

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una configuración de servidor de destino existente mediante el extremo de API `/authoring/destination-servers`.

Para obtener una descripción detallada de las funciones que puede eliminar a través de este extremo, lea los siguientes artículos:

* [Especificaciones del servidor para destinos creados con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Plantillas de especificaciones para destinos creados con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del mensaje](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuración de formato de archivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API del servidor de destino {#get-started}

Antes de continuar, revisa la [guía de introducción](../../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Eliminar una configuración de servidor de destino {#delete}

Puede eliminar una configuración de servidor de destino [existente](create-destination-server.md) realizando una solicitud `DELETE` al extremo `/authoring/destination-servers` con el `{INSTANCE_ID}`de la configuración de servidor de destino que desea eliminar.

>[!TIP]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Para obtener una configuración de servidor de destino existente y su correspondiente `{INSTANCE_ID}`, vea el artículo acerca de [recuperar una configuración de servidor de destino](retrieve-destination-server.md).

**Formato de API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` de la configuración del servidor de destino que desea eliminar. |

+++Solicitud

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo eliminar un servidor de destino existente a través del extremo de la API de Destination SDK `/authoring/destination-servers`.

Para obtener más información acerca de lo que puede hacer con este extremo, consulte los siguientes artículos:

* [Crear una configuración de servidor de destino](create-destination-server.md)
* [Recuperar una configuración de servidor de destino](retrieve-destination-server.md)
* [Actualizar la configuración de un servidor de destino](update-destination-server.md)
