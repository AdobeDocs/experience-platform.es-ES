---
title: orgId
description: La propiedad orgId es una cadena que indica al Adobe a qué organización se envían esos datos.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

El `orgId` es una cadena que indica al Adobe a qué organización se envían esos datos. **Esta propiedad es necesaria para todos los datos enviados mediante el SDK web.**

Para localizar su `orgID`:

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. En cualquier lugar de Adobe Experience Cloud, pulse **`[Ctrl]`** + **`[I]`**. A [!UICONTROL Depurador de datos de usuario] se abre.
1. Clic **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) junto al [!UICONTROL ID de organización actual], o haga clic en **[!UICONTROL Organizaciones asignadas]** para ver otros ID de organización a los que puede acceder.
1. Cuando haya terminado de localizar la información deseada, haga clic en **[!UICONTROL Cerrar]**.

Los ID de organización siempre son cadenas alfanuméricas de 24 caracteres y siempre terminan en `@AdobeOrg`.

## Configuración de un `orgID` uso de la extensión de etiqueta del SDK web

Introduzca el identificador de organización en la variable **[!UICONTROL ID de organización IMS]** campo de texto cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Introduzca el ID de organización deseado en [!UICONTROL ID de organización IMS] Campo de texto cerca de la parte superior.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Configuración de un `orgID` uso de la biblioteca JavaScript del SDK web

Configure las variables `orgId` cadena al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK web, este genera un error de consola y los datos no se envían al Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
