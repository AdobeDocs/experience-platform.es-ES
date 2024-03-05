---
title: targetMigrationEnabled
description: Permita que el SDK web lea y escriba cookies de Adobe Target.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

El `targetMigrationEnabled` La propiedad es un booleano que permite al SDK web leer y escribir las cookies mbox y mboxEdgeCluster que utilizan las bibliotecas Adobe Target 1.x y 2.x. Esta opción le permite conservar el perfil del visitante entre páginas que utilizan implementaciones anteriores de Adobe Target y páginas que utilizan el SDK web.

## Habilitar la migración de Target desde at.js mediante la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Migración de Target de at.js al SDK web]** casilla de verificación cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Personalización] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Migración de Target de at.js al SDK web]**.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Habilitar la migración de Target desde at.js mediante la biblioteca JavaScript del SDK web

Configure las variables `targetMigrationEnabled` booleano al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `false`. Establezca este valor en `true` si tiene páginas que todavía utilizan las bibliotecas Adobe Target 1.x o 2.x.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
