---
title: orgId
description: La propiedad orgId es una cadena que indica a Adobe a qué organización se envían esos datos.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

La propiedad `orgId` es una cadena que indica a Adobe a qué organización se envían esos datos. **Esta propiedad es necesaria para todos los datos enviados mediante Web SDK.**

Para localizar su `orgID`:

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. En cualquier lugar de Adobe Experience Cloud, presione **`[Ctrl]`** + **`[I]`**. Se abre una ventana de [!UICONTROL User Data Debugger].
1. Haga clic en **[!UICONTROL Copy]** ![Copiar](../../assets/copy.png) al lado de [!UICONTROL Current Org ID] o haga clic en la ficha **[!UICONTROL Assigned Orgs]** para ver otros identificadores de organización a los que puede acceder.
1. Cuando termine de buscar la información deseada, haga clic en **[!UICONTROL Close]**.

Los identificadores de organización siempre son cadenas alfanuméricas de 24 caracteres y siempre terminan en `@AdobeOrg`.

Establezca la cadena `orgId` al ejecutar el comando `configure`. Si omite esta propiedad al configurar Web SDK, Web SDK genera un error de consola y los datos no se envían a Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## Establecimiento del ID de organización con la extensión de etiquetas Web SDK

Esta opción se puede configurar en la extensión de etiquetas Web SDK con [opciones de configuración de instancias de SDK](/help/tags/extensions/client/web-sdk/configure/general.md). El campo se rellena automáticamente en función de la organización en la que se creó la propiedad de etiqueta.
