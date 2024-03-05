---
title: renderDecisions
description: Procesar contenido personalizado que pueda procesarse automáticamente.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# `renderDecisions`

El `renderDecisions` permite forzar el SDK web para procesar cualquier contenido personalizado que sea apto para el procesamiento automático.

## Representar contenido personalizado con la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Procesar decisiones de personalización visuales]** dentro de las acciones de una regla de etiqueta.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Desplácese hacia abajo hasta el [!UICONTROL Personalización] , luego seleccione la **[!UICONTROL Procesar decisiones de personalización visuales]** casilla de verificación
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Representar contenido personalizado mediante la biblioteca JavaScript del SDK web

Configure las variables `renderDecisions` booleano al ejecutar el `sendEvent` comando. Si se omite, el valor predeterminado de esta propiedad es `false`. Establezca esta propiedad como `true` si desea procesar automáticamente el contenido personalizado.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
