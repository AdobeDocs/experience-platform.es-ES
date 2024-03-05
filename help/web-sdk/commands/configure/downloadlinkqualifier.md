---
title: downloadLinkQualifier
description: Ayuda a determinar cómo el seguimiento automático de vínculos clasifica los vínculos de descarga.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Si habilita el seguimiento automático de vínculos mediante [`clickCollectionEnabled`](clickcollectionenabled.md), el `downloadLinkQualifier` La propiedad ayuda a determinar los criterios para que una dirección URL se considere un vínculo de descarga.

Esta propiedad es una cadena regex. Si la dirección URL donde se hizo clic coincide con esta regex, `xdm.web.webInteraction.type` se establece en `"download"`. Los vínculos también se clasifican inmediatamente como vínculos de descarga si incluyen una `download` atributo del HTML. If `clickCollectionEnabled` no está activada, esta propiedad no hace nada.

## Descargar calificador de vínculos mediante la extensión de etiqueta del SDK web

Habilite la **[!UICONTROL Habilitar la recopilación de datos de clics]** , a continuación, introduzca el texto deseado en **[!UICONTROL Descargar calificador de vínculo]** cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Recopilación de datos] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Una vez activada, la variable **[!UICONTROL Descargar calificador de vínculo]** aparece un cuadro de texto. Introduzca el valor deseado. También hay botones disponibles para probar la regex y restaurar el valor predeterminado.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Descargar calificador de vínculos mediante la biblioteca JavaScript del SDK web

Configure las variables `downloadLinkQualifier` cadena al ejecutar el `configure` comando. Si omite esta propiedad, el valor predeterminado es el siguiente:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Si desea utilizar criterios diferentes para calificar los vínculos de descarga, establezca esta propiedad al valor regex deseado.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
