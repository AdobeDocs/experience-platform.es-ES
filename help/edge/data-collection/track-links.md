---
title: Seguimiento de vínculos mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos de vínculo a Adobe Analytics con el SDK web de Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;interacción web;vistas de página;seguimiento de vínculos;vínculos;seguimiento de vínculos;rastreo de vínculos;clickCollection;colección de clics;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: b22eccb34e98ca2da47fe849492ee464d679d2a0
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Seguimiento de vínculos

Los vínculos se pueden configurar manualmente o rastrear [automáticamente](#automaticLinkTracking). El seguimiento manual se realiza añadiendo los detalles en la parte `web.webInteraction` del esquema. Hay tres variables requeridas:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", // Name that shows up in the custom links report
      "URL":"https://myurl.com", // The URL of the link
      "type":"other", // values: other, download, exit
      }
    }
  }
});
```

El tipo de vínculo puede tener uno de estos tres valores:

* **`other`:** Un vínculo personalizado
* **`download`:** Un vínculo de descarga
* **`exit`:** Un vínculo de salida

Estos valores [se asignan automáticamente](adobe-analytics/automatically-mapped-vars.md) a Adobe Analytics si [está configurado](adobe-analytics/analytics-overview.md) para hacerlo.

## Seguimiento automático de vínculos {#automaticLinkTracking}

De forma predeterminada, el SDK web captura, etiqueta y registra los clics en etiquetas de vínculo cualificadas. Los clics se capturan con un detector de eventos de [captura](https://www.w3.org/TR/uievents/#capture-phase) clic adjunto al documento.

El seguimiento automático de vínculos se puede deshabilitar configurando [el SDK web.](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)

```javascript
clickCollectionEnabled: false
```

### ¿Qué etiquetas cumplen los requisitos para el seguimiento de vínculos?{#qualifyingLinks}

El seguimiento automático de vínculos se realiza con las etiquetas `A` y `AREA` delimitadoras. Sin embargo, estas etiquetas no se tienen en cuenta para el seguimiento de vínculos si tienen un controlador `onclick` adjunto.

### ¿Cómo se etiquetan los vínculos?{#labelingLinks}

Los vínculos se etiquetan como vínculos de descarga si la etiqueta de anclaje incluye un atributo de descarga o si el vínculo termina con una extensión de archivo popular. El calificador del vínculo de descarga puede estar [configurado](../fundamentals/configuring-the-sdk.md) con una expresión regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Los vínculos se etiquetan como vínculos de salida si el dominio de destino del vínculo difiere del `window.location.hostname` actual.

Los vínculos que no se califican como vínculos de descarga o salida se etiquetan como &quot;otros&quot;.

### ¿Cómo se pueden filtrar los valores de seguimiento de vínculos?

Los datos recopilados con el seguimiento automático de vínculos se pueden inspeccionar y filtrar proporcionando una función de llamada de retorno [onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

El filtrado de datos de seguimiento de vínculos puede resultar útil al preparar los datos para los informes de Analytics. El seguimiento automático de vínculos captura tanto el nombre del vínculo como la dirección URL del vínculo. En los informes de Analytics, el nombre del vínculo tiene prioridad sobre la dirección URL del vínculo. Si desea informar de la dirección URL del vínculo, es necesario eliminar el nombre del vínculo. El siguiente ejemplo muestra una función `onBeforeEventSend` que elimina el nombre del vínculo para los vínculos de descarga:

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

