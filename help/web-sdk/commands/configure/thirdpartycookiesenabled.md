---
title: thirdPartyCookiesEnabled
description: Permitir el uso de cookies de terceros para identificar a los visitantes.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

La propiedad `thirdPartyCookiesEnabled` es un booleano que determina si el SDK web establece cookies en un contexto de terceros. Habilitar esta opción resulta útil si desea identificar visitantes entre subdominios o dominios que pertenecen a su organización. Sin embargo, muchos exploradores modernos limitan la configuración y la caducidad de las cookies de terceros.

La propiedad `thirdPartyCookiesEnabled` también controla si se puede solicitar un [`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk) en las llamadas a [`getIdentity`](../getidentity.md).

Cuando esta opción está habilitada, el SDK web utiliza Adobe Audience Manager para ayudar a identificar a un visitante. Cuando esta opción está desactivada, la llamada al Audience Manager está desactivada. Consulte [Explicación de las llamadas al dominio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=es) en la guía del usuario del Audience Manager para obtener más información.

## Habilitar cookies de terceros mediante la extensión de etiqueta del SDK web

Seleccione la casilla de verificación **[!UICONTROL Usar cookies de terceros]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Identidad] y, a continuación, active la casilla de verificación **[!UICONTROL Usar cookies de terceros]**.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Habilitar cookies de terceros mediante la biblioteca JavaScript del SDK web

Establezca el booleano `thirdPartyCookiesEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK web, el valor predeterminado es `true`. Establezca este valor en `false` si no desea que el SDK web use Audience Manager para ayudar a identificar a los visitantes.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```
