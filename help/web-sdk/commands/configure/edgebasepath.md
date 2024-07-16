---
title: edgeBasePath
description: Ruta base del extremo que se utiliza para interactuar con los servicios de Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

La propiedad `edgeBasePath` modifica la ruta de destino al interactuar con los servicios de Adobe. La mayoría de las organizaciones no necesitan establecer o modificar esta propiedad.

## Ruta base de Edge mediante la extensión de etiqueta del SDK web

Escriba el texto deseado en el campo de texto **[!UICONTROL ruta de acceso base de Edge]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Configuración avanzada] y, a continuación, escriba el valor deseado en el campo de texto **[!UICONTROL Ruta de acceso base de Edge]**.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Ruta base de Edge mediante la biblioteca JavaScript del SDK web

Establezca el campo de texto `edgeBasePath` al ejecutar el comando `configure`. Si omite esta propiedad, el valor predeterminado será `ee`. El Adobe recomienda omitir esta propiedad en la mayoría de las configuraciones.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
