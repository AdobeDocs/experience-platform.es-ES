---
title: clickCollectionEnabled
description: Determine si los datos sobre clics en vínculos se recopilan automáticamente.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# `clickCollectionEnabled`

El `clickCollectionEnabled` es un booleano que determina si el SDK web recopila automáticamente los datos de vínculos. Esta propiedad es útil en los casos en los que prefiere rastrear manualmente los datos de vínculos.

Si no está desactivado, los siguientes elementos XDM se rellenan automáticamente con datos:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

## Lógica de seguimiento de vínculos automática

El SDK web rastrea todos los clics en `<a>` y `<area>` elementos de HTML si no tiene un `onClick` atributo. Los clics se capturan con una [captar](https://www.w3.org/TR/uievents/#capture-phase) haga clic en el detector de eventos adjunto al documento. Cuando se hace clic en un vínculo válido, se ejecuta la siguiente lógica en orden:

1. Si el vínculo coincide con los criterios basados en los valores de [`downloadLinkQualifier`](downloadlinkqualifier.md), o si el vínculo contiene un `download` atributo de HTML, `xdm.web.webInteraction.type` se establece en `"download"`.
1. Si el dominio de destino del vínculo difiere del actual `window.location.hostname`, `xdm.web.webInteraction.type` se establece en `"exit"`.
1. Si el vínculo no cumple los requisitos de ninguno de los dos `"download"` o `"exit"`, `xdm.web.webInteraction.type` se establece en `"other"`.

En todos los casos, `xdm.web.webInteraction.name` se establece en la etiqueta de texto del vínculo y `xdm.web.webInteraction.URL` se establece en la dirección URL de destino del vínculo. Si también desea establecer el nombre del vínculo en la dirección URL, puede anular este campo XDM mediante [`onBeforeLinkClickSend`](onbeforelinkclicksend.md).

## Habilitar el seguimiento automático de vínculos mediante la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Habilitar la recopilación de datos de clics]** casilla de verificación cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Recopilación de datos] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Habilitar el seguimiento automático de vínculos mediante la biblioteca JavaScript del SDK web

Configure las variables `clickCollectionEnabled` booleano al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `true`. Establezca este valor en `false` si prefiere configurar manualmente `xdm.web.webInteraction.type` y `xdm.web.webInteraction.value`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false
});
```
