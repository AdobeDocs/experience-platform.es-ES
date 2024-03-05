---
title: edgeBasePath
description: Ruta base del extremo que se utiliza para interactuar con los servicios de Adobe.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

El `edgeBasePath` modifica la ruta de destino al interactuar con los servicios de Adobe. La mayoría de las organizaciones no necesitan establecer o modificar esta propiedad.

## Ruta base de Edge mediante la extensión de etiqueta del SDK web

Introduzca el texto deseado en la **[!UICONTROL Ruta base del borde]** campo de texto cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Configuración avanzada] , luego introduzca el valor deseado en la sección **[!UICONTROL Ruta base del borde]** campo de texto.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Ruta base de Edge mediante la biblioteca JavaScript del SDK web

Configure las variables `edgeBasePath` campo de texto al ejecutar el `configure` comando. Si omite esta propiedad, el valor predeterminado es el valor `ee`. El Adobe recomienda omitir esta propiedad en la mayoría de las configuraciones.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
