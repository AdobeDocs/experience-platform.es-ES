---
title: onBeforeEventSend
description: Obtenga información sobre cómo configurar el SDK web para registrar una función de JavaScript que pueda alterar los datos que envía justo antes de que se envíen al Adobe.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# `onBeforeEventSend`

La llamada de retorno `onBeforeEventSend` le permite registrar una función de JavaScript que puede modificar los datos que envía justo antes de que dichos datos se envíen al Adobe. Esta llamada de retorno le permite manipular el objeto `xdm` o `data`, incluida la capacidad de agregar, editar o quitar elementos. También puede cancelar de forma condicional el envío de datos, por ejemplo, con el tráfico de bots del lado del cliente detectado.

>[!WARNING]
>
>Esta llamada de retorno permite el uso de código personalizado. Si algún código que incluya en la llamada de retorno genera una excepción no detectada, se detendrá el procesamiento del evento. Los datos no se envían al Adobe.

## Configure en antes de la devolución de llamada de envío de evento mediante la extensión de etiqueta del SDK web {#tag-extension}

Seleccione el botón **[!UICONTROL Proporcionar antes del código de devolución de llamada de envío de evento]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Este botón abre una ventana modal donde puede insertar el código deseado.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Recopilación de datos] y, a continuación, seleccione el botón **[!UICONTROL Proporcionar antes del código de devolución de llamada de envío de evento]**.
1. Este botón abre una ventana modal con un editor de código. Inserte el código deseado y luego haga clic en **[!UICONTROL Guardar]** para cerrar la ventana modal.
1. Haga clic en **[!UICONTROL Guardar]** en la configuración de la extensión y publique los cambios.

En el editor de código, tiene acceso a las siguientes variables:

* **`content.xdm`**: la carga [XDM](../sendevent/xdm.md) para el evento.
* **`content.data`**: la carga del objeto [data](../sendevent/data.md) para el evento.
* **`return true`**: salga inmediatamente de la llamada de retorno y envíe datos al Adobe con los valores actuales en el objeto `content`.
* **`return false`**: salga inmediatamente de la llamada de retorno y anule el envío de datos al Adobe.

Se puede usar cualquier variable definida fuera de `content`, pero no se incluye en la carga útil enviada al Adobe.

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
>Evite devolver `false` en el primer evento de una página. Devolver `false` en el primer evento puede afectar negativamente a la personalización.

## Configurar en antes de la devolución de llamada de envío de evento mediante la biblioteca JavaScript del SDK web {#library}

Registre la llamada de retorno `onBeforeEventSend` al ejecutar el comando `configure`. Puede cambiar el nombre de la variable `content` a cualquier valor que desee mediante el cambio de la variable de parámetro dentro de la función en línea.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
