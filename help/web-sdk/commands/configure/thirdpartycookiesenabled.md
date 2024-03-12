---
title: thirdPartyCookiesEnabled
description: Permitir el uso de cookies de terceros para identificar a los visitantes.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [ha anunciado](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) planea interrumpir la compatibilidad de Chrome con cookies de terceros en el segundo semestre de 2024. Por lo tanto, las cookies de terceros ya no serán compatibles con ninguno de los exploradores principales.
>
>Cuando se implemente este cambio, el Adobe dejará de admitir el `demdex` que se admite actualmente en el SDK web.


El `thirdPartyCookiesEnabled` es un booleano que determina si el SDK web establece cookies en un contexto de terceros. Habilitar esta opción resulta útil si desea identificar visitantes entre subdominios o dominios que pertenecen a su organización. Sin embargo, muchos exploradores modernos limitan la configuración y la caducidad de las cookies de terceros.

Cuando esta opción está habilitada, el SDK web utiliza Adobe Audience Manager para ayudar a identificar a un visitante. Cuando esta opción está desactivada, la llamada al Audience Manager está desactivada. Consulte [Explicación de las llamadas al dominio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=es) en la guía del usuario del Audience Manager para obtener más información.

## Habilitar cookies de terceros mediante la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Uso de cookies de terceros]** casilla de verificación cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Identidad] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Uso de cookies de terceros]**.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Habilitar las cookies de terceros mediante la biblioteca JavaScript del SDK web

Configure las variables `thirdPartyCookiesEnabled` booleano al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `true`. Establezca este valor en `false` si no desea que el SDK web utilice Audience Manager para ayudar a identificar a los visitantes.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
