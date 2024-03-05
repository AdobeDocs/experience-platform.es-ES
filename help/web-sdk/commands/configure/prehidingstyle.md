---
title: prehiddenStyle
description: Cree una definición de CSS que permita que el contenido personalizado se cargue sin parpadeos.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

El `prehidingStyle` permite definir un selector de CSS para ocultar contenido personalizado hasta que se cargue. Esta propiedad es útil en implementaciones sincrónicas de SDK web para evitar parpadeos. El Adobe recomienda utilizar la variable [preocultar fragmento](../../personalization/manage-flicker.md) para implementaciones asincrónicas de SDK web.

Los selectores CSS que defina en esta propiedad empiezan a ocultar contenido al ejecutar el primer [`sendEvent`](../sendevent/overview.md) en una página. El contenido se muestra cuando se recibe una respuesta del Adobe, que generalmente incluye contenido personalizado. El contenido también se muestra si la variable `sendEvent` se produce un error o se agota el tiempo de espera.

Si incluye ambos `prehidingStyle` y el fragmento preocultado en la implementación, el fragmento preocultado tiene prioridad sobre esta propiedad de configuración.

## Preocultación de estilo mediante la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Proporcionar estilo de preocultación]** botón cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Personalización] , luego seleccione el botón **[!UICONTROL Proporcionar estilo de preocultación]**.
1. Este botón abre una ventana modal con un editor CSS. Inserte el selector CSS y el bloque de declaración deseados y haga clic en **[!UICONTROL Guardar]** para cerrar la ventana modal.
1. Clic **[!UICONTROL Guardar]** en configuración de la extensión, publique los cambios.

## Preocultación de estilo mediante la biblioteca JavaScript del SDK web

Configure las variables `prehidingStyle` cadena al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK web, no se oculta nada al ejecutar el primero `sendEvent` en una página. Establezca este valor en el selector CSS y el bloque de declaración deseados para las bibliotecas cargadas sincrónicamente.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
