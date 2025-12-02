---
title: onBeforeEventSend
description: Obtenga información sobre cómo configurar Web SDK para registrar una función de JavaScript que pueda alterar los datos que envía justo antes de que se envíen a Adobe.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# `onBeforeEventSend`

La llamada de retorno `onBeforeEventSend` le permite registrar una función de JavaScript que puede modificar los datos que envía justo antes de que dichos datos se envíen a Adobe. Esta llamada de retorno le permite manipular el objeto `xdm` o `data`, incluida la capacidad de agregar, editar o quitar elementos. También puede cancelar de forma condicional el envío de datos, por ejemplo, con el tráfico de bots del lado del cliente detectado.

>[!WARNING]
>
>Esta llamada de retorno permite el uso de código personalizado. Si algún código que incluya en la llamada de retorno genera una excepción no detectada, el procesamiento del evento se detiene y **los datos no se envían a Adobe.**

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

## Configurar en antes de la devolución de llamada del envío de eventos mediante la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [Opciones de configuración de recopilación de datos](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback).
