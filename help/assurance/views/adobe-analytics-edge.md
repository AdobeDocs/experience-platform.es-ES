---
title: Eventos de Analytics 2.0 en Assurance
description: En esta guía se explica cómo utilizar la vista de Edge de Adobe Analytics y Analytics con Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
exl-id: faaa2c1d-3471-4d86-9a25-03265b996e31
source-git-commit: fcef41a1cf3f082a437e2ceeb9203793c6a20c36
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 15%

---

# Eventos de Analytics 2.0 en Assurance

Analytics Events 2.0 proporciona una vista más completa de los eventos del SDK a los usuarios que depuran y validan su implementación de Adobe Analytics. La vista muestra eventos enviados a Adobe Analytics desde [Adobe Experience Platform Edge Network SDK](https://developer.adobe.com/client-sdks/edge/edge-network/) así como el [SDK de Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/solution/adobe-analytics/). La vista también incluye un panel de detalles, que proporciona contexto sobre cómo el SDK de cliente y los servicios de flujo ascendente procesaron el evento después de que abandonara el dispositivo.

## Introducción

Para utilizar esta vista, complete los siguientes pasos:

1. [Configurar Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Crear y conectarse a una sesión de Assurance](../tutorials/using-assurance.md).
3. En la interfaz de usuario de Assurance del menú de vista de navegación izquierda **Inicio**, seleccione **Eventos de Analytics 2.0 (Beta)**. Si no ve esta opción, seleccione **Configure** en la parte inferior izquierda de la ventana, agregue **Analytics Events 2.0 (Beta)** y seleccione **Guardar**.

## Vista de Edge de Analytics

Use la vista Edge de Analytics si usa las extensiones móviles **Edge Network** o **Edge Bridge**. Esta vista se activa cuando se activa el conmutador &quot;Analytics Edge (Beta)&quot; en la esquina superior derecha, y muestra los eventos de Analytics enviados a través de la red de Edge en la sesión actual. Esto incluye todos los eventos activados por la extensión de ciclo vital, la extensión de Edge o la extensión de Edge Bridge.

![Imagen que muestra la opción que cambió a la vista de Analytics Edge.](./images/adobe-analytics-edge/edge-analytics-view-toggle.png)

La vista de Edge de Analytics contiene información sobre los eventos de Edge relacionados con Analytics y los eventos de ciclo de vida que envía el cliente. Al elegir un evento en la lista, el panel de vista de detalles de evento de la derecha muestra los eventos procesados por el SDK de cliente y por el servicio ascendente después de que abandonaron el dispositivo. Esto permite ver fácilmente la cadena de eventos que resultaron de una llamada a.

![Imagen que muestra diferentes componentes en la vista de Edge de Analytics para el escenario de Edge Bridge.](./images/adobe-analytics-edge/edgebridge-analytics-events.png)

El evento **Datos posteriores al procesamiento** de la lista confirma que los datos se han procesado y enviado correctamente a Adobe Analytics. Si falta este evento o cualquier dato procesado, los usuarios pueden expandir cada evento de la lista para ver información de depuración detallada.

### Vista de detalles de evento de Analytics Edge

Para un evento de solicitud de Edge o un evento de seguimiento de Analytics, la vista detallada contiene las siguientes partes:

* Detalles del evento: un evento de solicitud perimetral del SDK de origen.
* Solicitud de Edge Bridge: un evento exclusivamente para el flujo de trabajo de la extensión de Edge Bridge.
* Flujo de datos: un evento representado para el flujo de datos de esta sesión.
* Visita recibida de Edge: representa la visita recibida de Edge.
* Visita de Edge procesada: representa la visita procesada en Edge.
* Visita de Analytics: Representa la visita recibida de Analytics.
* Asignación de Analytics: representa el estado de asignación de datos en Analytics.
* Analytics respondido: estado de respuesta de Analytics.
* Datos posteriores al proceso: Información sobre el evento que contiene la asignación de variables, evars y props.

### Validación de Edge de Analytics

La vista de validación de Edge de Analytics permite ver fácilmente los resultados de los scripts de validación relacionados con Edge de Analytics. Los errores mostrados por los validadores pueden contener vínculos a dónde deben corregirse o mostrar eventos que están en estado de error.

![Imagen que muestra la ficha validadores en la vista Edge de Analytics.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)

## Vista de eventos de Analytics

Utilice la vista de eventos de Analytics si utiliza la extensión móvil **Adobe Analytics**. Esta vista le permite ver fácilmente los eventos de Analytics enviados desde su cliente conectado, incluidos los eventos de seguimiento de acción, seguimiento de estado y ciclo vital. Esta vista está activa mientras que la opción &quot;Analytics Edge (Beta)&quot; de la parte superior derecha está desactivada.

![Imagen que muestra la opción que cambió a la vista de Analytics.](./images/adobe-analytics-edge/direct-analytics-view-toggle-button.png)

Al seleccionar uno de los eventos de Analytics en la tabla de eventos, se pueden ver los detalles de cómo se procesaron los eventos en el panel derecho.

![Imagen que muestra diferentes componentes en la vista Eventos de Analytics.](./images/adobe-analytics-edge/analytics-events.png)

### Estado posterior al procesamiento

Una vez que el SDK realiza una solicitud de red con Adobe Analytics, el estado le dirá si Assurance pudo recuperar la información de posprocesamiento de la solicitud de Adobe Analytics. La vista Eventos de Analytics debe permanecer activa mientras el estado posterior al procesamiento esté en funcionamiento una vez activada la solicitud.

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

### Vista de detalles del evento

Para un evento de seguimiento de Analytics, la vista detallada contiene las siguientes partes:

* Un evento de solicitud de SDK Analytics de origen.
* Datos de metadatos y contexto de la solicitud, como el ID del grupo de informes, las versiones de extensión del SDK y los datos de contexto.
* Información posprocesada sobre el evento de Analytics que contiene la asignación de variables, evars y props.

### Validación de vista de Analytics

La vista de validación le permite ver fácilmente los resultados de los scripts de validación relacionados con Analytics. Los errores mostrados por los validadores pueden contener vínculos a dónde deben corregirse o mostrar eventos que están en estado de error.

![Imagen que muestra la ficha validadores en la vista de Analytics.](./images/adobe-analytics-edge/analytics-validation-view.png)