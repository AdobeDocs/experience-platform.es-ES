---
description: Esta página ejemplifica la llamada de API utilizada para eliminar una configuración de servidor de destino existente a través del Adobe Experience Platform Destination SDK.
title: Eliminar una configuración del servidor de destino
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 3%

---


# Eliminar una configuración del servidor de destino

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una configuración de servidor de destino existente mediante el uso de la variable `/authoring/destination-servers` extremo de API.

Para obtener una descripción detallada de las capacidades que puede eliminar a través de este punto final, lea los siguientes artículos:

* [Especificaciones del servidor para los destinos creados con el Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Plantillas de especificaciones para destinos creados con el Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del mensaje](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuración de formato de archivo](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Introducción a las operaciones de API del servidor de destino {#get-started}

Antes de continuar, revise la [guía de introducción](../../getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Eliminar una configuración del servidor de destino {#delete}

Puede eliminar un [existente](create-destination-server.md) configuración del servidor de destino realizando una `DELETE` solicitud al `/authoring/destination-servers` punto final con la variable `{INSTANCE_ID}`de la configuración del servidor de destino que desea eliminar.

>[!TIP]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Para obtener una configuración de servidor de destino existente y su correspondiente `{INSTANCE_ID}`, consulte el artículo sobre [recuperación de una configuración del servidor de destino](retrieve-destination-server.md).

**Formato de API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | La variable `ID` de la configuración del servidor de destino que desea eliminar. |

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

## Gestión de errores de API {#error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo eliminar un servidor de destino existente a través del Destination SDK `/authoring/destination-servers` extremo de API.

Para obtener más información sobre lo que puede hacer con este punto final, consulte los siguientes artículos:

* [Crear una configuración de servidor de destino](create-destination-server.md)
* [Recuperar una configuración del servidor de destino](retrieve-destination-server.md)
* [Actualizar la configuración del servidor de destino](update-destination-server.md)

