---
title: Vista de Adobe Analytics para medios de streaming en Assurance
description: En esta guía se explica cómo utilizar Adobe Analytics para medios de streaming con Adobe Experience Platform Assurance.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# Vista de Adobe Analytics para medios de streaming en Assurance

Con la integración entre Adobe Analytics para medios de streaming y Adobe Experience Platform Assurance, ahora puede validar la implementación de Media Analytics en su aplicación móvil. Las vistas de Media Analytics muestran lo que se rastrea en la sesión de medios, como:

- Evento de inicio de sesión que contiene todas las propiedades de metadatos de contenido principal, estándar y personalizadas, así como eventos de fin de sesión y de finalización de sesión.
- Los eventos de inicio y de inicio de las pausas publicitarias con todas las propiedades de publicidad adjuntas, así como los eventos de omisión y finalización para ambos.
- El capítulo comienza con todas las propiedades adjuntas, así como los eventos Chapter Skip y Chapter Complete.
- Todos los eventos de cambio de reproducción (reproducción, pausa, búfer, errores, cambio de velocidad de bits).
- Todos los eventos de seguimiento de cambios de estado del reproductor (inicio, fin).

Una vez que los datos se procesan en Analytics, el estado y los datos posteriores al procesamiento, como el tiempo invertido en contenido y la duración total de la pausa, también están disponibles en la vista de detalles del evento.

## Primeros pasos

Antes de continuar, asegúrese de que dispone de los siguientes servicios:

- El [IU de recopilación de datos Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para obtener información sobre cómo instalar Assurance en su aplicación, lea la [implementación de la guía Assurance](../tutorials/implement-assurance.md).

## Use Assurance con Adobe Analytics para medios de streaming

Una vez que se haya conectado y haya configurado la aplicación para Adobe Analytics, estará listo para configurarla para Streaming Media Analytics. En la parte inferior del panel izquierdo, seleccione **[!UICONTROL Configurar]** para añadir la vista Eventos de Media Analytics y **Guardar** it.

![Configurar](./images/adobe-analytics-streaming-media/configure.png)

Una vez añadida, seleccione la **[!UICONTROL Eventos de Media Analytics]** ver en la **[!UICONTROL Adobe Analytics]** para validar el seguimiento de la sesión.

![Seleccionar](./images/adobe-analytics-streaming-media/select.png)

En el **[!UICONTROL Eventos de Media Analytics]** Ver, puede buscar y filtrar por ID de sesión (VSID) para ver una sesión de medios específica. Para ver detalles de evento adicionales, seleccione un evento específico.

![Eventos de contenidos](./images/adobe-analytics-streaming-media/media-events.png)

Para obtener una vista más sucinta de las llamadas a la API, también puede ocultar los eventos de actualización del cabezal de reproducción seleccionando la variable **[!UICONTROL Ocultar eventos de actualización del cabezal de reproducción]** filtro.

![Ocultar cabezal de reproducción](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>La visualización de datos de análisis de medios posprocesados requiere el uso de versiones del SDK: Android Media 2.1.2 y iOS AEPMedia 3.0.1 (o superior)

Para ver los datos posprocesados, busque el evento de inicio de sesión y valide en la columna de estado que la sesión se ha completado. Si se completa, haga clic en el evento para ver un resumen de la sesión de medios en la vista de detalles del evento. Para obtener más información, desplácese hacia abajo para buscar los detalles posteriores al procesamiento.

![Vista posterior al procesamiento](./images/adobe-analytics-streaming-media/post-processed-view.png)
