---
title: documentUnloading
description: Utilice la API sendBeacon de JavaScript para enviar datos a Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

La propiedad `documentUnloading` le permite utilizar el método [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) de JavaScript para enviar datos a Adobe. Si una solicitud típica tarda demasiado, el explorador puede cancelarla. Puede indicar a Web SDK que use `sendBeacon` para que la solicitud se ejecute en segundo plano después de salir de la página. Habilite esta propiedad para evitar que el explorador cancele las solicitudes de datos al descargar.

Varios exploradores imponen un límite de 64 KB a la cantidad de datos que se pueden enviar con `sendBeacon` al mismo tiempo. Si el explorador rechaza el evento porque la carga útil es demasiado grande, Web SDK vuelve a utilizar su método de transporte normal. Incluso si un explorador determinado permite cargas útiles más grandes, los servidores de recopilación de datos de Adobe truncan las cargas útiles a 64 KB.

Establezca el booleano `documentUnloading` al ejecutar el comando `sendEvent`. Su valor predeterminado es `false`. Establezca esta propiedad en `true` si desea utilizar el método `sendBeacon` para enviar datos a Adobe.

>[!IMPORTANT]
>
>La propiedad `documentUnloading` no es compatible con la propiedad [`renderDecisions`](renderdecisions.md). Evite establecer ambas propiedades en `true` simultáneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## Descarga de documentos con la extensión de etiquetas Web SDK

La casilla de verificación **[!UICONTROL Document will unload]** está disponible al configurar una acción [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) al utilizar la extensión de etiqueta Web SDK.
