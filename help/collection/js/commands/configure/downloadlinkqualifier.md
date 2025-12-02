---
title: downloadLinkQualifier
description: Ayuda a determinar cómo el seguimiento automático de vínculos clasifica los vínculos de descarga.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

Si habilita el seguimiento automático de vínculos mediante [`clickCollectionEnabled`](clickcollectionenabled.md), la propiedad `downloadLinkQualifier` ayuda a determinar los criterios para que una dirección URL se considere un vínculo de descarga.

Esta propiedad es una cadena regex. Si la dirección URL donde se hizo clic coincide con esta regex, `xdm.web.webInteraction.type` se establece en `"download"`. Los vínculos también se clasifican inmediatamente como vínculos de descarga si incluyen un atributo HTML `download`. Si `clickCollectionEnabled` no está habilitado, esta propiedad no hace nada.

Establezca la cadena `downloadLinkQualifier` al ejecutar el comando `configure`. Si omite esta propiedad, el valor predeterminado es el siguiente:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Si desea utilizar criterios diferentes para calificar los vínculos de descarga, establezca esta propiedad al valor regex deseado.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## Descargar calificador de vínculos con la extensión de etiquetas Web SDK

El equivalente de la extensión de etiquetas Web SDK de este campo se encuentra en [Configuración de la recopilación de datos](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier) al configurar la extensión de etiquetas.
