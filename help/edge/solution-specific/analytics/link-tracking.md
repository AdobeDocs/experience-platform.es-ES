---
title: Seguimiento de vínculos y páginas con Adobe Analytics
seo-title: Seguimiento de vínculos a Adobe Analytics con Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo enviar datos de vínculos a Adobe Analytics con el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo enviar datos de vínculos a Adobe Analytics con el SDK web de Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8840e00ec3aa28d43c371b793da4a4b9bfc8d259
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Envío de datos a Adobe Analytics

Mientras que en el pasado había diferentes funciones para distinguir entre una vista de página y un vínculo (por ejemplo, `s.t(), s.tl()`), en el SDK web hay sólo el `sendEvent` comando. Los datos que envía con un evento determinan si deben ser una vista de página o un vínculo.

## Envío de una vista de página

Puede especificar una vista de página configurando la `web.webPageDetails.pageViews.value=1` variable.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Aunque Analytics registra técnicamente una vista de página aunque esta variable no esté configurada, se recomienda configurar esta variable siempre que se desee registrar una vista de página para que sea explícita en los datos y para futuras pruebas en la implementación.

## Vínculos de seguimiento

Los vínculos se pueden configurar manualmente o rastrear [automáticamente](#automaticLinkTracking). El seguimiento manual se realiza agregando los detalles en la parte del `web.webInteraction` esquema. Existen tres variables requeridas: `web.webInteraction.name`, `web.webInteraction.type` y `web.webInteraction.linkClicks.value`.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
      }
    }
  }
});
```

El tipo de vínculo puede ser uno de los tres valores:

* **`other`::** Un vínculo personalizado
* **`download`::** Un vínculo de descarga
* **`exit`::** Un vínculo de salida

### Seguimiento automático de vínculos {#automaticLinkTracking}

De forma predeterminada, el SDK web captura, [etiqueta](#labelingLinks)y [registra](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) clics en etiquetas de vínculos [válidas](#qualifyingLinks) . Los clics se capturan con un detector de eventos de [captura](https://www.w3.org/TR/uievents/#capture-phase) que se adjunta al documento.

Para desactivar el seguimiento automático de vínculos, [configure](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) el SDK web.

```javascript
clickCollectionEnabled: false
```

#### ¿Qué etiquetas califican para el seguimiento de vínculos?{#qualifyingLinks}

El seguimiento automático de vínculos se realiza para las etiquetas de anclaje `A` y `AREA` etiquetas. Sin embargo, estas etiquetas no se tienen en cuenta para el seguimiento de vínculos si tienen un `onclick` controlador adjunto.

#### ¿Cómo se etiquetan los vínculos?{#labelingLinks}

Los vínculos se etiquetan como vínculo de descarga si la etiqueta delimitadora incluye un atributo de descarga o si el vínculo termina con una extensión de archivo popular. El calificador de vínculo de descarga se puede [configurar](../../fundamentals/configuring-the-sdk.md) con una expresión regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Los vínculos se etiquetan como vínculos de salida si el dominio de destinatario del vínculo difiere del actual `window.location.hostname`.

Los vínculos que no se consideran vínculos de descarga o de salida se etiquetan como &quot;otros&quot;.
