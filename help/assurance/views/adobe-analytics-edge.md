---
title: Eventos de Analytics 2.0 en Assurance
description: En esta guía se explica cómo utilizar Adobe Analytics y la vista de Edge de Analytics con Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
source-git-commit: f707554ea89731fbd3f013d6065fde27ba7fa811
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 19%

---

# Eventos de Analytics 2.0 en Assurance

Analytics Events 2.0 proporciona una vista más completa de los eventos del SDK a los usuarios que depuran y validan su implementación de Adobe Analytics. La vista muestra los eventos enviados a Adobe Analytics desde el [SDK de Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) así como el [SDK de Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/). La vista también incluye un panel de detalles, que proporciona contexto sobre cómo el SDK de cliente ha procesado el evento, así como los servicios de flujo ascendente después de que abandonara el dispositivo.

## Introducción

Para utilizar esta vista, complete los siguientes pasos:

1. [Configuración de Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Creación y conexión a una sesión de Assurance](../tutorials/using-assurance.md).
3. En la interfaz de usuario de Assurance, vaya a navegación izquierda **Inicio** menú ver, seleccione **Eventos de Analytics 2.0 (beta)**. Si no ve esta opción, seleccione **Configurar** en la parte inferior izquierda de la ventana, añada el **Eventos de Analytics 2.0 (beta)** y seleccione **Guardar**.

## Vista de eventos de Analytics

Utilice la Vista de eventos de Analytics si está utilizando **Adobe Analytics** extensión móvil. Esta vista le permite ver fácilmente los eventos de Analytics enviados desde su cliente conectado, incluidos los eventos de seguimiento de acción, seguimiento de estado y ciclo vital. Al seleccionar uno de los eventos de Analytics en la tabla, se pueden ver los detalles de cómo se procesaron los eventos en el panel derecho.

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

- Un evento de solicitud de SDK Analytics de origen.
- Datos de metadatos y contexto de la solicitud, como el ID del grupo de informes, las versiones de extensión del SDK y los datos de contexto.
- Información posprocesada sobre el evento de Analytics que contiene la asignación de variables, evars y props.

### Validación de vista de Analytics

La vista de validación le permite ver fácilmente los resultados de los scripts de validación relacionados con Analytics. Los errores mostrados por los validadores pueden contener vínculos a dónde deben corregirse o mostrar eventos que están en estado de error.

![Imagen que muestra la pestaña validadores en la vista de Analytics.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Vista de Analytics Edge

Utilice la vista de Edge de Analytics si está utilizando **Red perimetral** o **Edge Bridge** extensiones móviles. Para habilitar esta vista, seleccione la opción &quot;Analytics Edge (Beta)&quot; en la parte superior derecha para ver los eventos de Analytics enviados a través de la red de Edge en la sesión actual. Esto incluye todos los eventos activados por la extensión del ciclo vital, las solicitudes de Edge o los eventos de Edge Bridge basados en los estados de seguimiento de acción y seguimiento.

![Imagen que muestra el conmutador que se utiliza para cambiar entre la vista de Analytics y la vista de Edge de Analytics.](./images/adobe-analytics-edge/analytics-view-toggle.png)

La vista de Edge de Analytics contiene información sobre las solicitudes de Edge relacionadas con Analytics y los métodos de ciclo de vida que envía el cliente. Al elegir un evento en la lista, el panel derecho muestra los eventos procesados por el SDK de cliente, así como por el servicio ascendente después de que abandonaron el dispositivo, para que pueda ver fácilmente la cadena de eventos que resultaron de una llamada.

![Imagen que muestra diferentes componentes en la vista de Edge de Analytics.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Validación de Edge de Analytics

La vista de validación de Edge de Analytics permite ver fácilmente los resultados de los scripts de validación relacionados con Edge de Analytics. Los errores mostrados por los validadores pueden contener vínculos a dónde deben corregirse o mostrar eventos que están en estado de error.

![Imagen que muestra la pestaña validadores en la vista de Analytics Edge.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
