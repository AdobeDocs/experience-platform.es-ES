---
title: targetMigrationEnabled
description: Permitir que Web SDK lea y escriba cookies de Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: dade74bf4a5cfd7b60eaf216583deb67b93a61db
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# `targetMigrationEnabled`

La propiedad `targetMigrationEnabled` es un booleano que permite a Web SDK leer y escribir las cookies [`mbox` y `mboxEdgeCluster`](https://experienceleague.adobe.com/es/docs/core-services/interface/data-collection/cookies/web-sdk) que utilizan las bibliotecas Adobe Target 1.x y 2.x. Esta opción le permite conservar el perfil del visitante entre páginas que utilizan implementaciones anteriores de Adobe Target y páginas que utilizan Web SDK.

Establezca el booleano `targetMigrationEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar Web SDK, el valor predeterminado es `false`. Establezca este valor en `true` si tiene algunas páginas que todavía usan las bibliotecas Adobe Target 1.x o 2.x.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Habilitar la migración de Target mediante la extensión de etiquetas Web SDK

Esta opción se puede configurar en la extensión de etiquetas Web SDK con [opciones de configuración de Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
