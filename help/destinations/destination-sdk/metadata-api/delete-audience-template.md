---
description: Esta página ejemplifica la llamada de API utilizada para eliminar una plantilla de audiencia existente a través del Adobe Experience Platform Destination SDK.
title: Eliminar una plantilla de audiencia
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---


# Eliminar una plantilla de audiencia

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una plantilla de audiencia mediante el uso de `/authoring/audience-templates` extremo de API.

Para obtener una descripción detallada de las capacidades que puede configurar a través de este extremo, consulte [gestión de metadatos de audiencia](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de plantilla de audiencia {#get-started}

Antes de continuar, revise la [guía de introducción](../getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Eliminar una plantilla de audiencia {#delete}

Puede eliminar un [existente](create-audience-template.md) plantilla de audiencia haciendo una `DELETE` solicitud al `/authoring/audience-templates` punto final con la variable `{INSTANCE_ID}`de la plantilla de audiencia que desea eliminar.

Para obtener una plantilla de audiencia existente y su correspondiente `{INSTANCE_ID}`, consulte el artículo sobre [recuperación de una plantilla de audiencia](retrieve-audience-template.md).

**Formato de API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | La variable `ID` de la plantilla de audiencia que desea eliminar. |

+++Solicitud

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

+++

## Gestión de errores de API {#error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo eliminar una plantilla de audiencia usando la variable `/authoring/audience-templates` extremo de API. Lectura [cómo usar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
