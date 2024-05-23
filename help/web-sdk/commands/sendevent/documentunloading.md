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

El `documentUnloading` permite utilizar la propiedad de JavaScript [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) para enviar datos al Adobe. Si una solicitud típica tarda demasiado, el explorador puede cancelarla. Puede indicar al SDK web que utilice `sendBeacon` para que la solicitud se ejecute en segundo plano después de salir de la página. Habilite esta propiedad para evitar que el explorador cancele las solicitudes de datos al descargar.

Varios exploradores imponen un límite de 64 KB a la cantidad de datos que se pueden enviar con `sendBeacon` al mismo tiempo. Si el explorador rechaza el evento porque la carga útil es demasiado grande, el SDK web vuelve a utilizar su método de transporte normal.

## Configurar la descarga de documentos mediante la extensión de etiqueta del SDK web

Habilite la **[!UICONTROL Se descargará el documento]** dentro de las acciones de una regla de etiqueta.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Habilite la **[!UICONTROL Se descargará el documento]** casilla de verificación en la [!UICONTROL Datos] sección.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Configurar la descarga de documentos mediante la biblioteca JavaScript del SDK web

Configure las variables `documentUnloading` booleano al ejecutar el `sendEvent` comando. Su valor predeterminado es `false`. Establezca esta propiedad como `true` si desea utilizar la variable `sendBeacon` para enviar datos al Adobe.

>[!IMPORTANT]
>
>El `documentUnloading` La propiedad no es compatible con [`renderDecisions`](renderdecisions.md) propiedad. No debe establecer ambas propiedades en `true` simultáneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
