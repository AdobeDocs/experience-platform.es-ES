---
title: downloadLinkQualifier
description: Ayuda a determinar cómo el seguimiento automático de vínculos clasifica los vínculos de descarga.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Si habilita el seguimiento automático de vínculos mediante [`clickCollectionEnabled`](clickcollectionenabled.md), la propiedad `downloadLinkQualifier` ayuda a determinar los criterios para que una dirección URL se considere un vínculo de descarga.

Esta propiedad es una cadena regex. Si la dirección URL donde se hizo clic coincide con esta regex, `xdm.web.webInteraction.type` se establece en `"download"`. Los vínculos también se clasifican inmediatamente como vínculos de descarga si incluyen un atributo de HTML `download`. Si `clickCollectionEnabled` no está habilitado, esta propiedad no hace nada.

## Descargar calificador de vínculos mediante la extensión de etiqueta del SDK web

Habilite la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]** y, a continuación, escriba el texto deseado en **[!UICONTROL Calificador de vínculos de descarga]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Recopilación de datos] y, a continuación, active la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Una vez habilitado, aparecerá el cuadro de texto **[!UICONTROL Cualificador de vínculo de descarga]**. Introduzca el valor deseado. También hay botones disponibles para probar la regex y restaurar el valor predeterminado.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Descargar calificador de vínculos mediante la biblioteca JavaScript del SDK web

Establezca la cadena `downloadLinkQualifier` al ejecutar el comando `configure`. Si omite esta propiedad, el valor predeterminado es el siguiente:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Si desea utilizar criterios diferentes para calificar los vínculos de descarga, establezca esta propiedad al valor regex deseado.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
