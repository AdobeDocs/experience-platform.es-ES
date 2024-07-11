---
title: onBeforeEventSend
description: Obtenga información sobre cómo configurar el SDK web para registrar una función de JavaScript que pueda alterar los datos que envía justo antes de que se envíen al Adobe.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# `onBeforeEventSend`

El `onBeforeEventSend` la devolución de llamada le permite registrar una función de JavaScript que puede alterar los datos que envía justo antes de que se envíen al Adobe. Esta llamada de retorno le permite manipular la variable `xdm` o `data` , incluida la posibilidad de agregar, editar o eliminar elementos. También puede cancelar de forma condicional el envío de datos, por ejemplo, con el tráfico de bots del lado del cliente detectado.

>[!WARNING]
>
>Esta llamada de retorno permite el uso de código personalizado. Si algún código que incluya en la llamada de retorno genera una excepción no detectada, se detendrá el procesamiento del evento. Los datos no se envían al Adobe.

## Configure en antes de la devolución de llamada de envío de evento mediante la extensión de etiqueta del SDK web {#tag-extension}

Seleccione el **[!UICONTROL Proporcionar antes del código de devolución de llamada de envío de evento]** botón cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Este botón abre una ventana modal donde puede insertar el código deseado.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Recopilación de datos] , luego seleccione el botón **[!UICONTROL Proporcionar antes del código de devolución de llamada de envío de evento]**.
1. Este botón abre una ventana modal con un editor de código. Inserte el código deseado y haga clic en **[!UICONTROL Guardar]** para cerrar la ventana modal.
1. Clic **[!UICONTROL Guardar]** en configuración de la extensión, publique los cambios.

En el editor de código, tiene acceso a las siguientes variables:

* **`content.xdm`**: La [XDM](../sendevent/xdm.md) carga útil para el evento.
* **`content.data`**: La [datos](../sendevent/data.md) carga útil del objeto para el evento.
* **`return true`**: Salga inmediatamente de la llamada de retorno y envíe datos al Adobe con los valores actuales en la `content` objeto.
* **`return false`**: Salga inmediatamente de la llamada de retorno y anule el envío de datos al Adobe.

Cualquier variable definida fuera de `content` se pueden usar, pero no se incluyen en la carga útil enviada al Adobe.

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Evite volver `false` en el primer evento de una página. Retorno `false` en el primer evento puede afectar negativamente a la personalización.

## Configurar en antes de la devolución de llamada de envío de evento mediante la biblioteca JavaScript del SDK web {#library}

Registre el `onBeforeEventSend` devolución de llamada al ejecutar `configure` comando. Puede cambiar el `content` nombre de la variable a cualquier valor que desee cambiando la variable del parámetro dentro de la función dentro de la línea.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

También puede registrar su propia función en lugar de una función en línea.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
