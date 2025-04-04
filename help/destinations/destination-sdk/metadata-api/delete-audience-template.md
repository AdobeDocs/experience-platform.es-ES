---
description: Esta página ejemplifica la llamada de API utilizada para eliminar una plantilla de audiencia existente a través de Adobe Experience Platform Destination SDK.
title: Eliminación de una plantilla de audiencia
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 2%

---

# Eliminación de una plantilla de audiencia

>[!IMPORTANT]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para eliminar una plantilla de audiencia mediante el extremo de API `/authoring/audience-templates`.

Para obtener una descripción detallada de las funcionalidades que puede configurar a través de este extremo, consulte [gestión de metadatos de audiencia](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de plantillas de audiencia {#get-started}

Antes de continuar, revisa la [guía de introducción](../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Eliminación de una plantilla de audiencia {#delete}

Puede eliminar una plantilla de audiencia [existing](create-audience-template.md) realizando una solicitud `DELETE` al extremo `/authoring/audience-templates` con el `{INSTANCE_ID}`de la plantilla de audiencia que desea eliminar.

Para obtener una plantilla de audiencia existente y sus `{INSTANCE_ID}` correspondientes, consulte el artículo acerca de [recuperar una plantilla de audiencia](retrieve-audience-template.md).

**Formato de API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` de la plantilla de audiencia que desea eliminar. |

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

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo eliminar una plantilla de audiencia mediante el extremo de API `/authoring/audience-templates`. Lee [cómo usar Destination SDK para configurar tu destino](../guides/configure-destination-instructions.md) para saber dónde encaja este paso en el proceso de configuración de tu destino.
