---
title: Seguimiento de vínculos y páginas con Adobe Analytics
seo-title: Seguimiento de vínculos a Adobe Analytics con Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo enviar datos de vínculos a Adobe Analytics con el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo enviar datos de vínculos a Adobe Analytics con el SDK web de Experience Platform
translation-type: tm+mt
source-git-commit: b50082405cd0392ff827a83ad82091fbcd370b21
workflow-type: tm+mt
source-wordcount: '236'
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
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

Aunque Analytics registra técnicamente una vista de página aunque esta variable no esté configurada, se recomienda configurar esta variable siempre que se desee registrar una vista de página para que sea explícita en los datos y para que en el futuro se pueda comprobar la implementación.

## Vínculos de seguimiento

Los vínculos se pueden configurar agregando los detalles en la parte del `web.webInteraction` esquema. Existen tres variables requeridas: `web.webInteraction.name`, `web.webInteraction.type` y `web.webInteraction.linkClicks.value`.

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
});
```

El tipo de vínculo puede ser uno de los tres valores:

* **`other`::** Un vínculo personalizado
* **`download`::** Vínculo de descarga (la biblioteca puede seguirlos automáticamente)
* **`exit`::** Un vínculo de salida

### Seguimiento automático de vínculos

El SDK web puede rastrear automáticamente todos los clics en vínculos activando [clickCollection](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled).

Los vínculos de descarga se detectan automáticamente en función de los tipos de archivo más conocidos. Se puede configurar la lógica para la clasificación de las descargas.
