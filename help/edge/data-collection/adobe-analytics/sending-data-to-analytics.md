---
title: Envío de datos a Adobe Analytics mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Analytics mediante el SDK web de Adobe Experience Platform.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;vistas de página;seguimiento de vínculos;vínculos;seguimiento de vínculos;clickCollection;colección de clics;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Envío de datos a Adobe Analytics

Mientras que en el pasado había diferentes funciones para distinguir entre una vista de página y un vínculo (por ejemplo, `s.t(), s.tl()`), en el SDK web sólo hay el comando `sendEvent`. Los datos que envía con un evento determinan si deben ser una vista de página o un vínculo. [Obtenga más información sobre los vínculos](../track-links.md) de seguimiento.

## Envío de una vista de página

Puede especificar una vista de página estableciendo la variable `web.webPageDetails.pageViews.value=1`.

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
