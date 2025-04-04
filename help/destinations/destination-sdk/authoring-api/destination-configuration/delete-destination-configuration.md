---
description: Esta página ejemplifica la llamada de API utilizada para eliminar una configuración de destino existente a través de Adobe Experience Platform Destination SDK.
title: Eliminar una configuración de destino
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 2%

---

# Eliminar una configuración de destino

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una configuración de destino existente mediante el extremo de API `/authoring/destinations`.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de la API de configuración de destino {#get-started}

Antes de continuar, revisa la [guía de introducción](../../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Eliminar una configuración de destino {#delete}

Puede eliminar una configuración de servidor de destino [existente](create-destination-configuration.md) realizando una solicitud `DELETE` al extremo `/authoring/destinations` con el `{INSTANCE_ID}`de la configuración de destino que desea eliminar.

>[!TIP]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Para obtener una configuración de destino existente y su `{INSTANCE_ID}` correspondiente, vea el artículo acerca de [recuperar una configuración de destino](retrieve-destination-configuration.md).

**Formato de API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` de la configuración de destino que desea eliminar. |

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

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo eliminar una configuración de destino existente a través del extremo de la API de Destination SDK `/authoring/destinations`.

Para obtener más información acerca de lo que puede hacer con este extremo, consulte los siguientes artículos:

* [Crear una configuración de destino](create-destination-configuration.md)
* [Recuperación de una configuración de destino](retrieve-destination-configuration.md)
* [Actualizar una configuración de destino](update-destination-configuration.md)
