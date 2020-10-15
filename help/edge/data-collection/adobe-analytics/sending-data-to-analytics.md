---
title: Seguimiento de vínculos y páginas con Adobe Analytics
seo-title: Seguimiento de vínculos a Adobe Analytics con Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo enviar datos de vínculos a Adobe Analytics con el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo enviar datos de vínculos a Adobe Analytics con el SDK web de Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 9e1ad05285b27a9fc8b56db903609add3fef144e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Envío de datos a Adobe Analytics

Mientras que en el pasado había diferentes funciones para distinguir entre una vista de página y un vínculo (por ejemplo, `s.t(), s.tl()`), en el SDK web hay sólo el `sendEvent` comando. Los datos que envía con un evento determinan si deben ser una vista de página o un vínculo. [Más información sobre los vínculos de seguimiento](../track-links.md)

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
