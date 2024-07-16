---
title: eventType
description: Establece el tipo de evento para una llamada a sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

La propiedad `eventType` le permite definir el tipo de evento que envía mediante el SDK web. Este campo finalmente rellena el campo `xdm.eventType`. Resulta útil cuando desea diferenciar los tipos de evento que envía al Adobe.

El Adobe proporciona algunos tipos de eventos predefinidos que puede utilizar. Consulte [Valores disponibles para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) en la guía del usuario de XDM para obtener una lista completa de los valores predefinidos. También puede utilizar sus propios valores si lo prefiere.

Si establece `type` aquí y `xdm.eventType` en el objeto [`xdm`](xdm.md), el valor de este campo tiene prioridad.

## Configurar el tipo de evento con la extensión de etiqueta del SDK web

Establezca el campo desplegable **[!UICONTROL Tipo]** dentro de las acciones de una regla de etiqueta.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send event]**.
1. Use el menú desplegable debajo del campo **[!UICONTROL Tipo]** o ingrese su propio valor.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

## Configuración del tipo de evento mediante la biblioteca de JavaScript del SDK web

Establezca la propiedad de cadena `eventType` al ejecutar el comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
