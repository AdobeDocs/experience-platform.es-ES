---
title: Seguimiento de vínculos mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos de vínculos a Adobe Analytics con el SDK web de Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;vistas de página;seguimiento de vínculos;vínculos;seguimiento de vínculos;clickCollection;colección de clics;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Seguimiento de vínculos

Los vínculos se pueden configurar manualmente o rastrear [automáticamente](#automaticLinkTracking). El seguimiento manual se realiza agregando los detalles en la parte `web.webInteraction` del esquema. Existen tres variables requeridas:

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
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
      }
    }
  }
});
```

El tipo de vínculo puede ser uno de los tres valores:

* **`other`:** Un vínculo personalizado
* **`download`:** Un vínculo de descarga
* **`exit`:** Un vínculo de salida

## Seguimiento automático de vínculos {#automaticLinkTracking}

De forma predeterminada, el SDK web captura, etiqueta y registra los clics en las etiquetas de vínculo que cumplen los requisitos. Los clics se capturan con un detector de evento [captura](https://www.w3.org/TR/uievents/#capture-phase) que se adjunta al documento.

El seguimiento automático de vínculos se puede deshabilitar [configurando](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) el SDK web.

```javascript
clickCollectionEnabled: false
```

### ¿Qué etiquetas califican para el seguimiento de vínculos?{#qualifyingLinks}

El seguimiento automático de vínculos se realiza para las etiquetas `A` y `AREA` delimitadoras. Sin embargo, estas etiquetas no se tienen en cuenta para el seguimiento de vínculos si tienen un controlador `onclick` adjunto.

### ¿Cómo se etiquetan los vínculos?{#labelingLinks}

Los vínculos se etiquetan como vínculo de descarga si la etiqueta delimitadora incluye un atributo de descarga o si el vínculo termina con una extensión de archivo popular. El calificador de vínculo de descarga puede [configurarse](../fundamentals/configuring-the-sdk.md) con una expresión regular:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Los vínculos se etiquetan como vínculos de salida si el dominio de destinatario del vínculo difiere del `window.location.hostname` actual.

Los vínculos que no se consideran vínculos de descarga o de salida se etiquetan como &quot;otros&quot;.
