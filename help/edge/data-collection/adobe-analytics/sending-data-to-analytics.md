---
title: Envío de datos a Adobe Analytics mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Analytics mediante el SDK web de Adobe Experience Platform.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;interacción web;vistas de página;seguimiento de vínculos;vínculos de seguimiento;clickCollection;colección de clics;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Envío de datos a Adobe Analytics

Mientras que en el pasado existían diferentes funciones para distinguir entre una vista de página y un vínculo (por ejemplo, `s.t(), s.tl()`), en el SDK web solo está el `sendEvent` comando. Los datos que envía con un evento determinan si debe ser una vista de página o un vínculo. [Más información sobre los vínculos de seguimiento](../track-links.md).

## Envío de una vista de página

Puede especificar una vista de página configurando la variable `web.webPageDetails.pageViews.value=1` variable.

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

Aunque técnicamente Analytics registra una vista de página aunque no se haya configurado esta variable, se recomienda configurarla siempre que desee registrar una vista de página para que sea explícita en los datos y para futuras pruebas de la implementación.
