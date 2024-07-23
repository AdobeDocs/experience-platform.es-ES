---
title: targetMigrationEnabled
description: Permita que el SDK web lea y escriba cookies de Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

La propiedad `targetMigrationEnabled` es un booleano que permite al SDK web leer y escribir las cookies mbox y mboxEdgeCluster que utilizan las bibliotecas Adobe Target 1.x y 2.x. Esta opción le permite conservar el perfil del visitante entre páginas que utilizan implementaciones anteriores de Adobe Target y páginas que utilizan el SDK web.

## Habilitar la migración de Target desde at.js mediante la extensión de etiqueta del SDK web

Seleccione la casilla de verificación **[!UICONTROL Migrar Target de at.js al SDK web]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Personalization] y, a continuación, active la casilla de verificación **[!UICONTROL Migrar Target de at.js al SDK web]**.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Habilitar la migración de Target desde at.js mediante la biblioteca JavaScript del SDK web

Establezca el booleano `targetMigrationEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `false`. Establezca este valor en `true` si tiene algunas páginas que todavía usan las bibliotecas Adobe Target 1.x o 2.x.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```
