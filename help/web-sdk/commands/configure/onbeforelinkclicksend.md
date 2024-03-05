---
title: onBeforeLinkClickSend
description: Llamada de retorno que se ejecuta justo antes de que se envíen los datos de seguimiento de vínculos.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

El `onBeforeLinkClickSend` La devolución de llamada le permite registrar una función de JavaScript que puede alterar los datos de seguimiento de vínculos que envía justo antes de que esos datos se envíen al Adobe. Esta llamada de retorno le permite manipular la variable `xdm` o `data` , incluida la posibilidad de agregar, editar o eliminar elementos. También puede cancelar de forma condicional el envío de datos, por ejemplo, con el tráfico de bots del lado del cliente detectado. Es compatible con el SDK web 2.15.0 o posterior.

Esta llamada de retorno solo se ejecuta cuando [`clickCollectionEnabled`](clickcollectionenabled.md) está activada. If `clickCollectionEnabled` está deshabilitada, esta llamada de retorno no se ejecuta. Si ambos `onBeforeEventSend` y `onBeforeLinkClickSend` contener funciones registradas, la variable `onBeforeLinkClickSend` La función se ejecuta primero. Una vez que `onBeforeLinkClickSend` La función finaliza, la función `onBeforeEventSend` a continuación, ejecuta.

>[!WARNING]
>
>Esta llamada de retorno permite el uso de código personalizado. Si algún código que incluya en la llamada de retorno genera una excepción no detectada, se detendrá el procesamiento del evento. Los datos no se envían al Adobe.

## En antes del vínculo, haga clic en Enviar llamada de retorno mediante la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Proporcionar antes del código de devolución de llamada de envío de evento de clic de vínculo]** botón cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Este botón abre una ventana modal donde puede insertar el código deseado.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Recopilación de datos] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Seleccione el botón denominado **[!UICONTROL Proporcionar antes del código de devolución de llamada de envío de evento de clic de vínculo]**.
1. Este botón abre una ventana modal con un editor de código. Inserte el código deseado y haga clic en **[!UICONTROL Guardar]** para cerrar la ventana modal.
1. Clic **[!UICONTROL Guardar]** en configuración de la extensión, publique los cambios.

En el editor de código, puede agregar, editar o eliminar elementos dentro de la variable `content` objeto. Este objeto contiene la carga útil enviada al Adobe. No es necesario definir la variable `content` o ajuste cualquier código dentro de una función. Cualquier variable definida fuera de `content` se pueden usar, pero no se incluyen en la carga útil enviada al Adobe.

>[!TIP]
>
>Los objetos `content.xdm`, `content.data`, y `content.clickedElement` siempre están definidos en este contexto, por lo que no es necesario comprobar si existen. Algunas variables dentro de estos objetos dependen de la implementación y de la capa de datos. El Adobe recomienda buscar valores no definidos dentro de estos objetos para evitar errores de JavaScript.

Por ejemplo, supongamos que desea realizar las siguientes acciones:

* Modificar la dirección URL de la página actual
* Captura del elemento donde se hizo clic en un eVar de Adobe Analytics
* Cambiar el tipo de vínculo de &quot;otro&quot; a &quot;descargar&quot;

El código equivalente dentro de la ventana modal sería el siguiente:

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

De forma similar a [`onBeforeEventSend`](onbeforeeventsend.md), puede `return true` para completar inmediatamente la función, o `return false` para cancelar inmediatamente el envío de datos. Si cancela el envío de datos en `onBeforeLinkClickSend` cuando ambos `onBeforeEventSend` y `onBeforeLinkClickSend` contener funciones registradas, la variable `onBeforeEventSend` La función no se ejecuta.

## En antes del vínculo, haga clic en Enviar llamada de retorno mediante la biblioteca JavaScript del SDK web

Registre el `onBeforeLinkClickSend` devolución de llamada al ejecutar `configure` comando. Puede cambiar el `content` nombre de la variable a cualquier valor que desee cambiando la variable del parámetro dentro de la función dentro de la línea.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
