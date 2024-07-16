---
title: prehiddenStyle
description: Cree una definición de CSS que permita que el contenido personalizado se cargue sin parpadeos.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

La propiedad `prehidingStyle` le permite definir un selector de CSS para ocultar contenido personalizado hasta que se cargue. Esta propiedad es útil en implementaciones sincrónicas de SDK web para evitar parpadeos. El Adobe recomienda usar el [fragmento preocultado](../../personalization/manage-flicker.md) para implementaciones asincrónicas de SDK web.

Los selectores CSS que define en esta propiedad empiezan a ocultar contenido cuando ejecuta el primer comando [`sendEvent`](../sendevent/overview.md) en una página. El contenido se muestra cuando se recibe una respuesta del Adobe, que generalmente incluye contenido personalizado. El contenido también se muestra si el comando `sendEvent` falla o se agota el tiempo de espera.

Si incluye `prehidingStyle` y el fragmento de preocultación en la implementación, el fragmento de preocultación tiene prioridad sobre esta propiedad de configuración.

## Preocultación de estilo mediante la extensión de etiqueta del SDK web

Seleccione el botón **[!UICONTROL Proporcionar estilo de ocultamiento previo]** al [configurar la extensión de la etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Personalization] y, a continuación, seleccione el botón **[!UICONTROL Proporcionar estilo de ocultamiento previo]**.
1. Este botón abre una ventana modal con un editor CSS. Inserte el selector CSS y el bloque de declaración deseados y luego haga clic en **[!UICONTROL Guardar]** para cerrar la ventana modal.
1. Haga clic en **[!UICONTROL Guardar]** en la configuración de la extensión y publique los cambios.

## Preocultación de estilo mediante la biblioteca de JavaScript del SDK web

Establezca la cadena `prehidingStyle` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK web, no se oculta nada al ejecutar el primer comando `sendEvent` en una página. Establezca este valor en el selector CSS y el bloque de declaración deseados para las bibliotecas cargadas sincrónicamente.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
