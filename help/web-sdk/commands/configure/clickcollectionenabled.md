---
title: clickCollectionEnabled
description: Obtenga información sobre cómo configurar el SDK web para determinar si los datos de clics en vínculos se recopilan automáticamente.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

El `clickCollectionEnabled` es un booleano que determina si el SDK web recopila automáticamente los datos de vínculos. Si no establece esta variable, su valor predeterminado es `true` lo que significa que los datos de seguimiento de vínculos se recopilan automáticamente de forma predeterminada. Estableciendo esta propiedad en `false` es útil en los casos en los que prefiere rastrear los datos de vínculos manualmente.

Cuándo `clickCollectionEnabled` está activada, los siguientes elementos XDM se rellenan automáticamente con datos:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Los vínculos internos, de descarga y de salida se rastrean automáticamente de forma predeterminada cuando este booleano está habilitado. Si desea tener más control sobre el seguimiento automático de vínculos, Adobe recomienda utilizar la variable [`clickCollection`](clickcollection.md) objeto.

## Lógica de seguimiento de vínculos automática

El SDK web rastrea todos los clics en `<a>` y `<area>` elementos de HTML si no tiene un `onClick` atributo. Los clics se capturan con una [captar](https://www.w3.org/TR/uievents/#capture-phase) haga clic en el detector de eventos adjunto al documento. Cuando se hace clic en un vínculo válido, se ejecuta la siguiente lógica en orden:

1. Si el vínculo coincide con los criterios basados en los valores de [`downloadLinkQualifier`](downloadlinkqualifier.md), o si el vínculo contiene un `download` atributo de HTML, `xdm.web.webInteraction.type` se establece en `"download"` (if `clickCollection.downloadLinkEnabled` está activada).
1. Si el dominio de destino del vínculo difiere del actual `window.location.hostname`, `xdm.web.webInteraction.type` se establece en `"exit"` (if `clickCollection.exitLinkEnabled` está activada).
1. Si el vínculo no cumple los requisitos de ninguno de los dos `"download"` o `"exit"`, `xdm.web.webInteraction.type` se establece en `"other"`.

En todos los casos, `xdm.web.webInteraction.name` se establece en la etiqueta de texto del vínculo y `xdm.web.webInteraction.URL` se establece en la dirección URL de destino del vínculo. Si también desea establecer el nombre del vínculo en la dirección URL, puede anular este campo XDM con la variable `filterClickDetails` devolución de llamada en `clickCollection` objeto.

## Habilitar el seguimiento automático de vínculos mediante la extensión de etiqueta del SDK web {#tag-extension}

Seleccione el **[!UICONTROL Habilitar la recopilación de datos de clics]** casilla de verificación cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Recopilación de datos] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Habilitar el seguimiento automático de vínculos mediante la biblioteca de JavaScript del SDK web {#library}

Configure las variables `clickCollectionEnabled` booleano al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `true`. Establezca este valor en `false` si prefiere configurar `xdm.web.webInteraction.type` y `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
