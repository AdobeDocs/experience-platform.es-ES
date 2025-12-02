---
title: prehiddenStyle
description: Cree una definición de CSS que permita que el contenido personalizado se cargue sin parpadeos.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

La propiedad `prehidingStyle` le permite definir un selector de CSS para ocultar contenido personalizado hasta que se cargue. Esta propiedad es útil en implementaciones sincrónicas de Web SDK para evitar parpadeos. Adobe recomienda usar el [fragmento preocultado](/help/collection/use-cases/personalization/manage-flicker.md) para implementaciones asincrónicas de Web SDK.

Los selectores CSS que define en esta propiedad empiezan a ocultar contenido cuando ejecuta el primer comando [`sendEvent`](../sendevent/overview.md) en una página. El contenido se muestra cuando se recibe una respuesta de Adobe, que generalmente incluye contenido personalizado. El contenido también se muestra si el comando `sendEvent` falla o se agota el tiempo de espera.

Si incluye `prehidingStyle` y el fragmento de preocultación en la implementación, el fragmento de preocultación tiene prioridad sobre esta propiedad de configuración.

Establezca la cadena `prehidingStyle` al ejecutar el comando `configure`. Si omite esta propiedad al configurar Web SDK, no se oculta nada al ejecutar el primer comando `sendEvent` en una página. Establezca este valor en el selector CSS y el bloque de declaración deseados para las bibliotecas cargadas sincrónicamente.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## Preocultación de estilo mediante la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [opciones de configuración de Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md).
