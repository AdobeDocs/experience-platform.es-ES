---
title: onBeforeLinkClickSend
description: Llamada de retorno que se ejecuta justo antes de que se envíen los datos de seguimiento de vínculos.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Esta llamada de retorno está obsoleta. Utilice [`filterClickDetails`](clickcollection.md) en su lugar.

La llamada de retorno `onBeforeLinkClickSend` le permite registrar una función de JavaScript que puede alterar los datos de seguimiento de vínculos que envía justo antes de que dichos datos se envíen al Adobe. Esta llamada de retorno le permite manipular el objeto `xdm` o `data`, incluida la capacidad de agregar, editar o quitar elementos. También puede cancelar de forma condicional el envío de datos, por ejemplo, con el tráfico de bots del lado del cliente detectado. Es compatible con el SDK web 2.15.0 o posterior.

Esta devolución de llamada solo se ejecuta cuando [`clickCollectionEnabled`](clickcollectionenabled.md) está habilitado y [`filterClickDetails`](clickcollection.md) no contiene una función registrada. Si `clickCollectionEnabled` está deshabilitado o si `filterClickDetails` contiene una función registrada, esta devolución de llamada no se ejecutará. Si `onBeforeEventSend` y `onBeforeLinkClickSend` contienen funciones registradas, `onBeforeLinkClickSend` se ejecuta primero.

>[!WARNING]
>
>Esta llamada de retorno permite el uso de código personalizado. Si algún código que incluya en la llamada de retorno genera una excepción no detectada, se detendrá el procesamiento del evento. Los datos no se envían al Adobe.

## Configure en antes de que el vínculo haga clic en enviar llamada de retorno mediante la extensión de etiqueta del SDK web {#tag-extension}

Seleccione el botón **[!UICONTROL Proporcionar antes de hacer clic en el vínculo para enviar el código de devolución de llamada]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Este botón abre una ventana modal donde puede insertar el código deseado.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Recopilación de datos] y, a continuación, active la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Seleccione el botón con la etiqueta **[!UICONTROL Proporcionar antes de hacer clic en el vínculo para enviar el código de devolución de llamada]**.
1. Este botón abre una ventana modal con un editor de código. Inserte el código deseado y luego haga clic en **[!UICONTROL Guardar]** para cerrar la ventana modal.
1. Haga clic en **[!UICONTROL Guardar]** en la configuración de la extensión y publique los cambios.

En el editor de código, tiene acceso a las siguientes variables:

* **`content.clickedElement`**: el elemento DOM donde se hizo clic.
* **`content.xdm`**: la carga útil XDM para el evento.
* **`content.data`**: la carga del objeto de datos para el evento.
* **`return true`**: salga inmediatamente de la llamada de retorno con los valores de las variables actuales. La llamada de retorno `onBeforeEventSend` se ejecuta si contiene una función registrada.
* **`return false`**: salga inmediatamente de la llamada de retorno y anule el envío de datos al Adobe. No se ejecuta la devolución de llamada `onBeforeEventSend`.

Se puede usar cualquier variable definida fuera de `content`, pero no se incluye en la carga útil enviada al Adobe.

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

De forma similar a [`onBeforeEventSend`](onbeforeeventsend.md), puede `return true` para completar la función inmediatamente o `return false` para anular el envío de datos al Adobe. Si anula el envío de datos en `onBeforeLinkClickSend` cuando `onBeforeEventSend` y `onBeforeLinkClickSend` contienen funciones registradas, la función `onBeforeEventSend` no se ejecuta.

## Activar la configuración antes de hacer clic en el vínculo para enviar la llamada de retorno mediante la biblioteca JavaScript del SDK web {#library}

Registre la llamada de retorno `onBeforeLinkClickSend` al ejecutar el comando `configure`. Puede cambiar el nombre de la variable `content` a cualquier valor que desee mediante el cambio de la variable de parámetro dentro de la función en línea.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

También puede registrar su propia función en lugar de una función en línea.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
