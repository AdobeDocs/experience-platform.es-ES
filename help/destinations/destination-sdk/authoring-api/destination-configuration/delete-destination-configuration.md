---
description: Esta página ejemplifica la llamada de API utilizada para eliminar una configuración de destino existente a través del Adobe Experience Platform Destination SDK.
title: Eliminar una configuración de destino
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---


# Eliminar una configuración de destino

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una configuración de destino existente mediante `/authoring/destinations` Extremo de API.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de la API de configuración de destino {#get-started}

Antes de continuar, consulte la [guía de introducción](../../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Eliminar una configuración de destino {#delete}

Puede eliminar un [existente](create-destination-configuration.md) configuración del servidor de destino realizando una `DELETE` solicitud a la `/authoring/destinations` punto final con `{INSTANCE_ID}`de la configuración de destino que desea eliminar.

>[!TIP]
>
>**Extremo de API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obtener una configuración de destino existente y su correspondiente `{INSTANCE_ID}`, consulte el artículo sobre [recuperación de una configuración de destino](retrieve-destination-configuration.md).

**Formato de API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | El `ID` de la configuración de destino que desea eliminar. |

+++Solicitud

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.


## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo eliminar una configuración de destino existente a través del Destination SDK `/authoring/destinations` Extremo de API.

Para obtener más información acerca de lo que puede hacer con este extremo, consulte los siguientes artículos:

* [Crear una configuración de destino](create-destination-configuration.md)
* [Recuperación de una configuración de destino](retrieve-destination-configuration.md)
* [Actualizar una configuración de destino](update-destination-configuration.md)

