---
title: eventType
description: Establece el tipo de evento para una llamada a sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

El `eventType` permite definir el tipo de evento que envía mediante el SDK web. Este campo rellena finalmente la variable `xdm.eventType` field. Resulta útil cuando desea diferenciar los tipos de evento que envía al Adobe.

El Adobe proporciona algunos tipos de eventos predefinidos que puede utilizar. Consulte [Valores disponibles para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) en la guía del usuario de XDM para obtener una lista completa de los valores predefinidos. También puede utilizar sus propios valores si lo prefiere.

Si establece ambas `type` aquí y `xdm.eventType` en el [`xdm`](xdm.md) , el valor de este campo tiene prioridad.

## Configurar el tipo de evento con la extensión de etiqueta del SDK web

Configure las variables **[!UICONTROL Tipo]** campo desplegable dentro de las acciones de una regla de etiqueta.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Utilice el menú desplegable debajo de **[!UICONTROL Tipo]** o introduzca su propio valor.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Configurar el tipo de evento mediante la biblioteca JavaScript del SDK web

Configure las variables `eventType` propiedad de cadena al ejecutar el `sendEvent` comando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
