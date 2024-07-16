---
title: clickCollectionEnabled
description: Obtenga información sobre cómo configurar el SDK web para determinar si los datos de clics en vínculos se recopilan automáticamente.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

La propiedad `clickCollectionEnabled` es un booleano que determina si el SDK web recopila automáticamente los datos de vínculos. Si no establece esta variable, su valor predeterminado es `true`, lo que significa que los datos de seguimiento de vínculos se recopilan automáticamente de manera predeterminada. Es útil establecer esta propiedad en `false` en los casos en que prefiera rastrear los datos de vínculos manualmente.

Cuando `clickCollectionEnabled` está habilitado, los siguientes elementos XDM se rellenan automáticamente con datos:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Los vínculos internos, de descarga y de salida se rastrean automáticamente de forma predeterminada cuando este booleano está habilitado. Si desea tener más control sobre el seguimiento automático de vínculos, Adobe recomienda utilizar el objeto [`clickCollection`](clickcollection.md).

## Lógica de seguimiento de vínculos automática

El SDK web rastrea todos los clics en `<a>` y `<area>` elementos del HTML si no tiene un atributo `onClick`. Los clics se capturan con un detector de eventos de clic [capture](https://www.w3.org/TR/uievents/#capture-phase) que está adjunto al documento. Cuando se hace clic en un vínculo válido, se ejecuta la siguiente lógica en orden:

1. Si el vínculo coincide con criterios basados en valores de [`downloadLinkQualifier`](downloadlinkqualifier.md), o si el vínculo contiene un atributo de HTML `download`, `xdm.web.webInteraction.type` se establece en `"download"` (si `clickCollection.downloadLinkEnabled` está habilitado).
1. Si el dominio de destino del vínculo difiere del actual `window.location.hostname`, `xdm.web.webInteraction.type` se establece en `"exit"` (si `clickCollection.exitLinkEnabled` está habilitado).
1. Si el vínculo no cumple los requisitos para `"download"` o `"exit"`, `xdm.web.webInteraction.type` se establece en `"other"`.

En todos los casos, `xdm.web.webInteraction.name` se establece en la etiqueta de texto del vínculo y `xdm.web.webInteraction.URL` se establece en la dirección URL de destino del vínculo. Si también desea establecer el nombre del vínculo en la dirección URL, puede anular este campo XDM con la llamada de retorno `filterClickDetails` en el objeto `clickCollection`.

## Habilitar el seguimiento automático de vínculos mediante la extensión de etiqueta del SDK web {#tag-extension}

Seleccione la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Recopilación de datos] y, a continuación, active la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Habilitar el seguimiento automático de vínculos mediante la biblioteca de JavaScript del SDK web {#library}

Establezca el booleano `clickCollectionEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `true`. Establezca este valor en `false` si prefiere establecer `xdm.web.webInteraction.type` y `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
