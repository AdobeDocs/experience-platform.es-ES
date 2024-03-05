---
title: edgeDomain
description: Determine el dominio raíz al que desea enviar los datos.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

El `edgeDomain` permite cambiar el dominio al que el SDK web envía los datos. Esta propiedad la utilizan con frecuencia organizaciones que utilizan [cookies de origen](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=es). Los datos se envían al dominio propio de la organización y, a continuación, un registro CNAME reenvía esos datos al Adobe.

Su organización determina el valor correcto de esta propiedad al configurarla [cookies de origen](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=es). Una organización suele utilizar un subdominio dedicado para este fin. Por ejemplo, si utiliza el dominio `example.com`, puede configurar cookies de origen en `data.example.com`.

## Configuración de un dominio perimetral mediante la extensión de etiqueta del SDK web

Configure las variables **[!UICONTROL Dominio de Edge]** campo de texto cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Busque el campo de texto **[!UICONTROL Dominio de Edge]**, luego introduzca el valor deseado.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Configuración de un dominio Edge mediante la biblioteca JavaScript del SDK web

Configure las variables `edgeDomain` cadena al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK, el valor predeterminado es `edge.adobedc.net`. Establezca este valor si desea anular el dominio al que el SDK web envía los datos.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
