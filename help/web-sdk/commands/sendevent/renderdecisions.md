---
title: renderDecisions
description: Procesar contenido personalizado que pueda procesarse automáticamente.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

La propiedad `renderDecisions` le permite forzar al SDK web a procesar cualquier contenido personalizado que sea apto para el procesamiento automático.

## Representar contenido personalizado con la extensión de etiqueta del SDK web

Seleccione la casilla de verificación **[!UICONTROL Procesar decisiones de personalización visuales]** dentro de las acciones de una regla de etiqueta.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send event]**.
1. Desplácese hacia abajo hasta la sección [!UICONTROL Personalization] y, a continuación, active la casilla de verificación **[!UICONTROL Procesar decisiones de personalización visuales]**.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

## Representar contenido personalizado mediante la biblioteca de JavaScript del SDK web

Establezca el booleano `renderDecisions` al ejecutar el comando `sendEvent`. Si se omite, el valor predeterminado de esta propiedad es `false`. Establezca esta propiedad en `true` si desea procesar automáticamente el contenido personalizado.

>[!IMPORTANT]
>
>La propiedad `renderDecisions` no es compatible con la propiedad [`documentUnloading`](documentunloading.md). No debe establecer ambas propiedades en `true` simultáneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
