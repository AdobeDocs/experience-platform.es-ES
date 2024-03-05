---
title: idMigrationEnabled
description: Permite al SDK web leer cookies AMCV.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

El `idMigrationEnabled` permite al SDK web leer cookies AMCV establecidas por implementaciones de Adobe Experience Cloud anteriores. Si su organización actualiza la implementación al SDK web, esta configuración permite una transición más suave al servicio de Adobe Experience Cloud ID actual. Esta configuración es valiosa para que no observe un marcado aumento de visitantes únicos al actualizar al SDK web.

Si su organización ejecuta una implementación nueva del SDK web, habilitar esta configuración no afecta a la recopilación de datos ni a la identificación del visitante. No hay inconvenientes en dejarlo habilitado para todas las implementaciones.

## Habilitar la migración de ID con la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Migración de ECID de VisitorAPI al SDK web]** casilla de verificación cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Busque el [!UICONTROL Identidad] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Migración de ECID de VisitorAPI al SDK web]**.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Habilitar la migración de ID mediante la biblioteca JavaScript del SDK web

Configure las variables `idMigrationEnabled` booleano al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `true`. Establezca esta propiedad si desea deshabilitar la capacidad de leer cookies AMCV establecidas por la API de visitante. La mayoría de las organizaciones no necesitan establecer esta propiedad.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
