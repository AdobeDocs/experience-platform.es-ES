---
title: thirdPartyCookiesEnabled
description: Permitir el uso de cookies de terceros para identificar a los visitantes.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

La propiedad `thirdPartyCookiesEnabled` es un booleano que determina si Web SDK establece cookies en un contexto de terceros. Habilitar esta opción resulta útil si desea identificar visitantes entre subdominios o dominios que pertenecen a su organización. Sin embargo, muchos exploradores modernos limitan la configuración y la caducidad de las cookies de terceros. Si el explorador de un visitante no admite cookies de terceros, esta propiedad no hace nada.

La propiedad `thirdPartyCookiesEnabled` también controla si se puede solicitar un [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) en las llamadas a [`getIdentity`](../getidentity.md).

Cuando esta opción está habilitada, Web SDK utiliza Adobe Audience Manager para ayudar a identificar a un visitante. Cuando esta opción está desactivada, la llamada a Audience Manager está desactivada. Consulte [Explicación de las llamadas al dominio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=es) en la guía del usuario de Audience Manager para obtener más información.

Establezca el booleano `thirdPartyCookiesEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar Web SDK, el valor predeterminado es `true`. Establezca este valor en `false` si no desea que Web SDK utilice Audience Manager para identificar a los visitantes.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## Habilitar las cookies de terceros mediante la extensión de etiquetas de Web SDK

Esta opción se puede configurar en la extensión de etiquetas Web SDK con [parámetros de configuración de identidad](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies).
