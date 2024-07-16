---
title: idMigrationEnabled
description: Permite al SDK web leer cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

La propiedad `idMigrationEnabled` permite al SDK web leer cookies AMCV establecidas por implementaciones de Adobe Experience Cloud anteriores. Si su organización actualiza la implementación al SDK web, esta configuración permite una transición más suave al servicio de Adobe Experience Cloud ID actual. Esta configuración es valiosa para que no observe un marcado aumento de visitantes únicos al actualizar al SDK web.

Si su organización ejecuta una implementación nueva del SDK web, habilitar esta configuración no afecta a la recopilación de datos ni a la identificación del visitante. No hay inconvenientes en dejarlo habilitado para todas las implementaciones.

## Habilitar la migración de ID con la extensión de etiqueta del SDK web

Seleccione la casilla de verificación **[!UICONTROL Migrar ECID de VisitorAPI al SDK web]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Busque la sección [!UICONTROL Identidad] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Migrar ECID de VisitorAPI al SDK web]**.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Habilitar la migración de ID mediante la biblioteca de JavaScript del SDK web

Establezca el booleano `idMigrationEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `true`. Establezca esta propiedad si desea deshabilitar la capacidad de leer cookies AMCV establecidas por la API de visitante. La mayoría de las organizaciones no necesitan establecer esta propiedad.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
