---
title: Vista de Adobe Analytics en Assurance
description: En esta guía se explica cómo utilizar Adobe Analytics con Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---


# Vista de Adobe Analytics en Assurance

La integración de Adobe Experience Platform Assurance con Adobe Analytics proporciona una vista más completa de los eventos de SDK para los usuarios que depuran y validan su implementación de Adobe Analytics. La vista ahora muestra los eventos de ciclo vital y de acción/estado enviados a Adobe Analytics desde el [SDK de Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). La vista también incluye detalles de &quot;respuesta&quot; que proporcionan información sobre cómo se procesaron los eventos después de la aplicación de las reglas de procesamiento de cada grupo de informes respectivo.

![](./images/adobe-analytics/overview.png)

## Primeros pasos

Antes de continuar, asegúrese de que dispone de los siguientes servicios:

- La variable [Interfaz de usuario de recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para aprender a instalar Assurance en su aplicación, lea la [guía de implementación de Assurance](../tutorials/implement-assurance.md).

## Estado posprocesado

Una vez que el SDK haya realizado una solicitud de red con Adobe Analytics, el estado le indicará si Assurance ha podido recuperar la información posterior al procesamiento de la solicitud de Adobe Analytics.

Tenga en cuenta que para recuperar la información posterior al procesamiento, el usuario que ha iniciado sesión debe tener acceso al grupo de informes correspondiente.

| Estado | Descripción |
| :----- | :---------- |
| `Queued` | La solicitud de red está recuperando la información posterior al procesamiento. |
| `Processed` | La solicitud de red se realizó correctamente y se recibe la información posterior al procesamiento. |
| `Delayed` | Se ha superado el número máximo de solicitudes de reintentos para recuperar la información posterior al procesamiento. |
| `Error` | Un error provocó que la solicitud de red fallara. En la vista de detalles del evento se muestran más detalles sobre el error. |
| `Unauthorized` | El usuario no tiene acceso al grupo de informes de Adobe Analytics. |
| `Unavailable` | La solicitud de Adobe Analytics no tiene una `AnalyticsResponse` evento. |
| `No Debug Flag` | Es posible que la versión actual del SDK de Adobe Analytics o Assurance no admita la función de depuración de Analytics. Para obtener más información, lea la [Guía de resolución de problemas](../troubleshooting.md). |
| `Expired` | La variable `AnalyticsTrack` o `LifecycleStart` es mayor de 24 horas. |

## Vista de detalles del evento

Para un evento de seguimiento de Analytics, la vista detallada contiene las siguientes partes valiosas:

- Un evento de solicitud de SDK Analytics de origen.
- Los metadatos de OOTB y los datos de contexto de la solicitud, como el ID del grupo de informes, las versiones de la extensión de SDK, los datos de contexto de OOTB, etc.
- Información posprocesada sobre el evento de Analytics que contiene la asignación de revars, evars, props, etc.
