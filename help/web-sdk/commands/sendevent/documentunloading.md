---
title: documentUnloading
description: Utilice la API sendBeacon de JavaScript para enviar datos al Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

La propiedad `documentUnloading` le permite utilizar el método [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) de JavaScript para enviar datos al Adobe. Si una solicitud típica tarda demasiado, el explorador puede cancelarla. Puede indicar al SDK web que use `sendBeacon` para que la solicitud se ejecute en segundo plano después de salir de la página. Habilite esta propiedad para evitar que el explorador cancele las solicitudes de datos al descargar.

Varios exploradores imponen un límite de 64 KB a la cantidad de datos que se pueden enviar con `sendBeacon` al mismo tiempo. Si el explorador rechaza el evento porque la carga útil es demasiado grande, el SDK web vuelve a utilizar su método de transporte normal.

## Configurar la descarga de documentos mediante la extensión de etiqueta del SDK web

Habilitar la casilla de verificación **[!UICONTROL Documento descargará]** dentro de las acciones de una regla de etiqueta.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send event]**.
1. Habilitar la casilla de verificación **[!UICONTROL Documento descargará]** en la sección [!UICONTROL Datos].
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

## Configurar la descarga de documentos mediante la biblioteca JavaScript del SDK web

Establezca el booleano `documentUnloading` al ejecutar el comando `sendEvent`. Su valor predeterminado es `false`. Establezca esta propiedad en `true` si desea utilizar el método `sendBeacon` para enviar datos al Adobe.

>[!IMPORTANT]
>
>La propiedad `documentUnloading` no es compatible con la propiedad [`renderDecisions`](renderdecisions.md). No debe establecer ambas propiedades en `true` simultáneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
