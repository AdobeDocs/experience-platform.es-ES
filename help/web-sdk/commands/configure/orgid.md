---
title: orgId
description: La propiedad orgId es una cadena que indica al Adobe a qué organización se envían esos datos.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

La propiedad `orgId` es una cadena que indica al Adobe a qué organización se envían esos datos. **Esta propiedad es necesaria para todos los datos enviados mediante el SDK web.**

Para localizar su `orgID`:

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. En cualquier lugar de Adobe Experience Cloud, presione **`[Ctrl]`** + **`[I]`**. Se abre una ventana de [!UICONTROL Depurador de datos de usuario].
1. Haga clic en **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) junto al [!UICONTROL identificador de organización actual], o haga clic en la ficha **[!UICONTROL Organizaciones asignadas]** para ver otros identificadores de organización a los que puede acceder.
1. Cuando termine de buscar la información deseada, haga clic en **[!UICONTROL Cerrar]**.

Los identificadores de organización siempre son cadenas alfanuméricas de 24 caracteres y siempre terminan en `@AdobeOrg`.

## Configurar un(a) `orgID` mediante la extensión de etiqueta del SDK web

Escriba el identificador de organización en el campo de texto **[!UICONTROL ID de organización de IMS]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Escriba el identificador de organización deseado en el campo de texto [!UICONTROL ID de organización de IMS], cerca de la parte superior.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Configurar un(a) `orgID` mediante la biblioteca JavaScript del SDK web

Establezca la cadena `orgId` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK web, este genera un error de consola y los datos no se envían al Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
