---
title: eventType
description: Establece el tipo de evento para una llamada a sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

La propiedad `eventType` le permite definir el tipo de evento que envía mediante Web SDK. Este campo finalmente rellena el campo `xdm.eventType`. Resulta útil cuando desea diferenciar los tipos de evento que envía a Adobe.

Adobe proporciona algunos tipos de eventos predefinidos que puede utilizar. Consulte [Valores disponibles para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) en la guía del usuario de XDM para obtener una lista completa de los valores predefinidos. También puede utilizar sus propios valores si lo prefiere.

Si establece `type` aquí y `xdm.eventType` en el objeto [`xdm`](xdm.md), el valor de este campo tiene prioridad.

Establezca la propiedad de cadena `eventType` al ejecutar el comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Tipo de evento con la extensión de etiqueta Web SDK

La extensión de etiquetas Web SDK equivalente a esta propiedad es el menú desplegable [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) al configurar una acción &quot;[!UICONTROL Send event]&quot;.
