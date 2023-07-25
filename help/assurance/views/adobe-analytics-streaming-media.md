---
title: Vista de Adobe Analytics para medios de streaming en Assurance
description: En esta guía se explica cómo utilizar Adobe Analytics para medios de streaming con Adobe Experience Platform Assurance.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '412'
ht-degree: 100%

---

# Vista de Adobe Analytics para medios de streaming en Assurance

Con la integración entre Adobe Analytics para medios de streaming y Adobe Experience Platform Assurance, ahora puede validar la implementación de análisis de medios en su aplicación móvil. Las vistas de análisis de medios muestran lo que se rastrea en la sesión de medios, como lo siguiente:

- Evento de inicio de sesión que contiene todas las propiedades de metadatos de contenido principal, estándar y personalizadas, así como eventos de fin de sesión y sesión completa.
- Los eventos de Inicio de pausa para anuncios y de Inicio de anuncio con todas las propiedades de anuncios adjuntas, así como los eventos de Omitir y Completar para ambos.
- Inicio de capítulo con todas las propiedades adjuntas, así como los eventos Omitir capítulo y Capítulo completo.
- Todos los eventos de cambio de reproducción (reproducción, pausa, búfer, errores, cambio de velocidad de bits).
- Todos los eventos de seguimiento de cambios de estado del reproductor (inicio, fin).

Una vez que los datos se procesan en Analytics, el estado y los datos posprocesados, como el tiempo invertido en medios y la duración total de la pausa, también están disponibles en la vista de detalles del evento.

## Introducción

Antes de continuar, asegúrese de que dispone de los siguientes servicios:

- La [IU de recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para obtener información sobre cómo instalar Assurance en su aplicación, lea la [Guía de implementación de Assurance](../tutorials/implement-assurance.md).

## Uso de Assurance con Adobe Analytics para medios de streaming

Una vez que se haya conectado y haya configurado la aplicación para Adobe Analytics, podrá configurarla para el análisis de medios de streaming. En la parte inferior del panel izquierdo, seleccione **[!UICONTROL Configurar]** para añadir la vista Eventos de análisis de medios y **Guardar**.

![Configurar](./images/adobe-analytics-streaming-media/configure.png)

Una vez añadida, seleccione la vista **[!UICONTROL Eventos de análisis de medios]** en la sección **[!UICONTROL Adobe Analytics]** para validar el seguimiento de sesiones.

![Seleccionar](./images/adobe-analytics-streaming-media/select.png)

En la vista **[!UICONTROL Eventos de análisis de medios]**, puede buscar y filtrar por ID de sesión (VSID) para ver una sesión de medios específica. Para consultar detalles adicionales del evento, seleccione uno específico.

![Eventos de contenidos](./images/adobe-analytics-streaming-media/media-events.png)

Para obtener una vista más sucinta de las llamadas a la API, también puede ocultar los eventos de actualización del cabezal de reproducción seleccionando el filtro **[!UICONTROL Ocultar eventos de actualización del cabezal de reproducción]**.

![Ocultar cabezal de reproducción](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>La visualización de datos de análisis de medios posprocesados requiere el uso de dos versiones del SDK: Android Media 2.1.2 y iOS AEPMedia 3.0.1 (o superior)

Para ver los datos posprocesados, busque el evento de inicio de sesión y valide en la columna de estado que la sesión se ha completado. Si se ha completado, haga clic en el evento para ver un resumen de la sesión de medios en la vista detallada del evento. Para obtener más información, desplácese hacia abajo para buscar los detalles de posprocesamiento.

![Vista de posprocesamiento](./images/adobe-analytics-streaming-media/post-processed-view.png)
