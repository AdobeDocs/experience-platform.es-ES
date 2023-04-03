---
title: Vista de Adobe Analytics para medios de streaming en Assurance
description: En esta guía se explica cómo utilizar Adobe Analytics para medios de streaming con Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 1%

---


# Vista de Adobe Analytics para medios de streaming en Assurance

Con la integración entre Adobe Analytics para medios de streaming y Adobe Experience Platform Assurance, ahora puede validar la implementación de Media Analytics en su aplicación móvil. Las vistas de Media Analytics muestran el seguimiento realizado en la sesión de contenido, como por ejemplo:

- Evento de inicio de sesión que contiene todo el contenido principal, los metadatos estándar y las propiedades de metadatos personalizadas, así como los eventos de fin de sesión y de finalización de sesión.
- Eventos Inicio de desglose de anuncios e Inicio de anuncio con todas las propiedades de anuncio adjuntas, así como eventos de Omisión y Finalización para ambos.
- Inicio del capítulo con todas las propiedades adjuntas, así como los eventos Omisión del capítulo y Finalización del capítulo .
- Todos los eventos de cambio de reproducción (reproducción, pausa, búfer, errores, cambio de velocidad de bits).
- Todos los eventos de seguimiento de cambios de estado del reproductor (inicio, final).

Una vez procesados los datos en Analytics, el estado y los datos posteriores al procesamiento, como el tiempo invertido en los medios y la duración total de la pausa, también están disponibles en la vista de detalles del evento.

## Primeros pasos

Antes de continuar, asegúrese de que dispone de los siguientes servicios:

- La variable [Interfaz de usuario de recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para aprender a instalar Assurance en su aplicación, lea la [guía de implementación de Assurance](../tutorials/implement-assurance.md).

## Uso de Assurance con Adobe Analytics para medios de streaming

Una vez que se haya conectado y configurado la aplicación para Adobe Analytics, estará listo para configurarla para Streaming Media Analytics. En la parte inferior del panel izquierdo, seleccione **[!UICONTROL Configurar]** para agregar la vista Eventos de Media Analytics y **Guardar** es así.

![Configurar](./images/adobe-analytics-streaming-media/configure.png)

Una vez añadida, seleccione la opción **[!UICONTROL Eventos de Media Analytics]** en la **[!UICONTROL Adobe Analytics]** para validar el seguimiento de sesión.

![Seleccionar](./images/adobe-analytics-streaming-media/select.png)

En el **[!UICONTROL Eventos de Media Analytics]** , puede buscar y filtrar por ID de sesión (VSID) para ver una sesión de medios específica. Para ver detalles de eventos adicionales, seleccione un evento específico.

![Eventos de contenidos](./images/adobe-analytics-streaming-media/media-events.png)

Para obtener una vista más concisa de las llamadas a la API, también puede ocultar los eventos de actualización del cursor de reproducción al seleccionar la opción **[!UICONTROL Ocultar eventos de actualización del cabezal de reproducción]** filtro.

![Ocultar cabezal de reproducción](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>La visualización de datos de análisis de medios posprocesados requiere el uso de versiones de SDK: Android Media 2.1.2 y iOS AEPMedia 3.0.1 (o superior)

Para ver los datos posteriores al procesamiento, busque el evento de inicio de sesión y valide en la columna de estado que la sesión se completó. Si se completa, haga clic en el evento para ver un resumen de la sesión de medios en la vista de detalles del evento. Para obtener más información, desplácese hacia abajo para encontrar los detalles posteriores al procesamiento.

![Vista posterior al procesamiento](./images/adobe-analytics-streaming-media/post-processed-view.png)
