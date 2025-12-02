---
title: idMigrationEnabled
description: Permite que Web SDK lea cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

La propiedad `idMigrationEnabled` permite que Web SDK lea cookies AMCV establecidas por implementaciones de Adobe Experience Cloud anteriores. Si su organización actualiza la implementación a Web SDK, esta configuración permite una transición más suave al servicio de Adobe Experience Cloud ID actual. Esta configuración es valiosa para que no observe un marcado aumento de visitantes únicos al actualizar a Web SDK.

Si su organización ejecuta una implementación nueva de Web SDK, habilitar esta configuración no tiene ningún impacto en la recopilación de datos ni en la identificación de visitantes. No hay inconvenientes en dejarlo habilitado para todas las implementaciones.

Establezca el booleano `idMigrationEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar Web SDK, el valor predeterminado es `true`. Establezca esta propiedad si desea deshabilitar la capacidad de leer cookies AMCV establecidas por la API de visitante. La mayoría de las organizaciones no necesitan establecer esta propiedad.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Habilitar la migración de ID de visitantes con la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [opciones de configuración de identidad](/help/tags/extensions/client/web-sdk/configure/identity.md).
