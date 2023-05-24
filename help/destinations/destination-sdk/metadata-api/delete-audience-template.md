---
description: Esta página ejemplifica la llamada de API utilizada para eliminar una plantilla de audiencia existente a través del Adobe Experience Platform Destination SDK.
title: Eliminación de una plantilla de audiencia
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---


# Eliminación de una plantilla de audiencia

>[!IMPORTANT]
>
>**Extremo de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una plantilla de audiencia mediante `/authoring/audience-templates` Extremo de API.

Para obtener una descripción detallada de las funciones que puede configurar a través de este extremo, consulte [gestión de metadatos de audiencia](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de plantillas de audiencia {#get-started}

Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Eliminación de una plantilla de audiencia {#delete}

Puede eliminar un [existente](create-audience-template.md) plantilla de audiencia creando un `DELETE` solicitud a la `/authoring/audience-templates` punto final con `{INSTANCE_ID}`de la plantilla de audiencia que desea eliminar.

Para obtener una plantilla de audiencia existente y su correspondiente `{INSTANCE_ID}`, consulte el artículo sobre [recuperación de una plantilla de audiencia](retrieve-audience-template.md).

**Formato de API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | El `ID` de la plantilla de audiencia que desea eliminar. |

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

## Administración de errores de API {#error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo eliminar una plantilla de audiencia utilizando `/authoring/audience-templates` Extremo de API. Leer [cómo utilizar Destination SDK para configurar el destino](../guides/configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración del destino.
