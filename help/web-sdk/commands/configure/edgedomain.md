---
title: edgeDomain
description: Determine el dominio raíz al que desea enviar los datos.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

La propiedad `edgeDomain` le permite cambiar el dominio al que el SDK web envía los datos. Las organizaciones que usan [cookies de origen](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=es) suelen usar esta propiedad. Los datos se envían al dominio propio de la organización y, a continuación, un registro CNAME reenvía esos datos al Adobe.

Su organización determina el valor correcto de esta propiedad al configurar [cookies de origen](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=es). Una organización suele utilizar un subdominio dedicado para este fin. Por ejemplo, si usa el dominio `example.com`, puede configurar cookies de origen en `data.example.com`.

## Configuración de un dominio perimetral mediante la extensión de etiqueta del SDK web

Establezca el campo de texto **[!UICONTROL dominio de Edge]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Busque el campo de texto **[!UICONTROL dominio de Edge]** y luego ingrese el valor deseado.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Configuración de un dominio perimetral mediante la biblioteca JavaScript del SDK web

Establezca la cadena `edgeDomain` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK, el valor predeterminado es `edge.adobedc.net`. Establezca este valor si desea anular el dominio al que el SDK web envía los datos.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
