---
title: Vista de Adobe Analytics en Assurance
description: En esta guía se explica cómo utilizar Adobe Analytics con Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '359'
ht-degree: 100%

---

# Vista de Adobe Analytics en Assurance

La integración de Adobe Experience Platform Assurance con Adobe Analytics ofrece una vista más completa de los eventos de SDK a los usuarios que depuran y validan la implementación de Adobe Analytics. La vista ahora muestra los eventos de ciclo vital y acción/estado enviados a Adobe Analytics desde el [SDK de Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). La vista también incluye detalles de “respuesta” que proporcionan información sobre cómo se procesaron los eventos después de la aplicación de las reglas de procesamiento de cada grupo de informes respectivo.

![](./images/adobe-analytics/overview.png)

## Introducción

Antes de continuar, asegúrese de que dispone de los siguientes servicios:

- El [IU de recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para obtener información sobre cómo instalar Assurance en su aplicación, lea la [guía de implementación de Assurance](../tutorials/implement-assurance.md).

## Estado posterior al procesamiento

Una vez que el SDK realiza la solicitud de red con Adobe Analytics, el estado le dirá si Assurance pudo recuperar la información posterior al procesamiento de la solicitud de Adobe Analytics.

Tenga en cuenta que para recuperar la información posterior al procesamiento, el usuario que ha iniciado sesión debe tener acceso al grupo de informes correspondiente.

| Estado | Descripción |
| :----- | :---------- |
| `Queued` | La solicitud de red está recuperando la información posterior al procesamiento. |
| `Processed` | La solicitud de red se realizó correctamente y se recibe la información posterior al procesamiento. |
| `Delayed` | Se ha superado el número máximo de reintentos de solicitudes para recuperar la información posterior al procesamiento. |
| `Error` | Un error ha provocado el fallo de la solicitud de red. En la vista de los detalles del evento se muestran más detalles del error. |
| `Unauthorized` | El usuario no tiene acceso al grupo de informes de Adobe Analytics. |
| `Unavailable` | La solicitud de Adobe Analytics no tiene un evento de `AnalyticsResponse` correspondiente. |
| `No Debug Flag` | Es posible que la versión actual del SDK de Adobe Analytics o Assurance no admita la función de depuración de Analytics. Para obtener más información, lea la [guía de resolución de problemas](../troubleshooting.md). |
| `Expired` | El evento `AnalyticsTrack` o `LifecycleStart` tiene más de 24 horas. |

## Vista de detalles del evento

Para un evento de seguimiento de Analytics, la vista detallada contiene las siguientes partes útiles:

- Un evento de solicitud de SDK Analytics de origen.
- Metadatos de OOTB y datos de contexto de la solicitud, como el ID del grupo de informes, las versiones de extensión del SDK, los datos de contexto de OOTB, etc.
- Información posprocesada sobre el evento de Analytics que contiene la asignación de revars, evars, props, etc.
