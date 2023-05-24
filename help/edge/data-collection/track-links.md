---
title: Seguimiento de vínculos mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos de vínculo a Adobe Analytics con el SDK web de Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;interacción web;vistas de página;seguimiento de vínculos;vínculos de seguimiento;clickCollection;colección de clics;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Seguimiento de vínculos

Los vínculos se pueden configurar manualmente o rastrear [automáticamente](#automaticLinkTracking). El seguimiento manual se realiza añadiendo los detalles en la `web.webInteraction` forma parte del esquema. Hay tres variables requeridas:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

A partir de la versión 2.15.0, el SDK web captura el `region` del elemento de HTML donde se hizo clic. Esto habilita el [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=es) funciones de informes en Adobe Analytics.

El tipo de vínculo puede tener uno de estos tres valores:

* **`other`:** Un vínculo personalizado
* **`download`:** Un vínculo de descarga
* **`exit`:** Un vínculo de salida

Estos valores son [asignado automáticamente](adobe-analytics/automatically-mapped-vars.md) en Adobe Analytics si [configurado](adobe-analytics/analytics-overview.md) para ello.

## Seguimiento automático de vínculos {#automaticLinkTracking}

De forma predeterminada, el SDK web captura, etiqueta y registra los clics en las etiquetas de vínculo correspondiente. Los clics se capturan con una [captar](https://www.w3.org/TR/uievents/#capture-phase) haga clic en el detector de eventos adjunto al documento.

El seguimiento automático de vínculos se puede desactivar mediante [configuración](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) el SDK web.

```javascript
clickCollectionEnabled: false
```

### ¿Qué etiquetas cumplen los requisitos para el seguimiento de vínculos?{#qualifyingLinks}

El seguimiento automático de vínculos se realiza para el anclaje `A` y `AREA` etiquetas. Sin embargo, estas etiquetas no se consideran para el seguimiento de vínculos si tienen un adjunto `onclick` controlador.

### ¿Cómo se etiquetan los vínculos?{#labelingLinks}

Los vínculos se etiquetan como vínculo de descarga si la etiqueta de anclaje incluye un atributo de descarga o si el vínculo termina con una extensión de archivo popular. El calificador del vínculo de descarga puede ser [configurado](../fundamentals/configuring-the-sdk.md) con una expresión regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Los vínculos se etiquetan como vínculos de salida si el dominio de destino del vínculo difiere del actual `window.location.hostname`.

Los vínculos que no cumplen los requisitos como vínculos de descarga o salida están etiquetados como &quot;otro&quot;.

### ¿Cómo se pueden filtrar los valores de seguimiento de vínculos?

Los datos recopilados con el seguimiento automático de vínculos se pueden inspeccionar y filtrar mediante una [función de devolución de llamada onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

Filtrar los datos de seguimiento de vínculos puede resultar útil al preparar los datos para los informes de Analytics. El seguimiento automático de vínculos captura tanto el nombre como la dirección URL del vínculo. En los informes de Analytics, el nombre del vínculo tiene prioridad sobre la dirección URL del vínculo. Si desea informar de la dirección URL del vínculo, es necesario eliminar el nombre del vínculo. El siguiente ejemplo muestra un `onBeforeEventSend` función que elimina el nombre del vínculo para los vínculos de descarga:

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

A partir de la versión 2.15.0 del SDK web, los datos recopilados con el seguimiento automático de vínculos se pueden inspeccionar, aumentar o filtrar mediante un [función de devolución de llamada onBeforeLinkClickSend](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

Esta función de llamada de retorno solo se ejecuta cuando se produce un evento automático de clic en vínculo.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

Al filtrar los eventos de seguimiento de vínculos utilizando `onBeforeLinkClickSend` comando, el Adobe recomienda volver `false` para los clics en vínculos que no deben rastrearse. Cualquier otra respuesta hará que el SDK web envíe los datos a la red perimetral.


>[!NOTE]
>
>** Cuando tanto la variable `onBeforeEventSend` y `onBeforeLinkClickSend` Cuando se establecen las funciones de devolución de llamada, el SDK web ejecuta `onBeforeLinkClickSend` función de llamada de retorno para filtrar y aumentar el evento de interacción de clic en vínculo, seguido del evento `onBeforeEventSend` función de llamada de retorno.