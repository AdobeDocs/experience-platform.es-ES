---
title: Configuración del SDK web de Adobe Experience Platform
description: Utilice el comando configure para establecer la configuración necesaria al utilizar el SDK web.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 1c614ef525d55d7476d037c6838b35c3471e4501
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Configuración del SDK web de Adobe Experience Platform

La configuración del SDK web se completó con el comando `configure`. La configuración del SDK web es un paso vital y necesario que debe producirse cada vez que se utiliza la biblioteca o la extensión de etiqueta.

## Configuración del SDK web mediante la extensión de etiqueta {#configure-tag-extension}

Siga los pasos a continuación para configurar el SDK web a través de la extensión de etiqueta.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la [página de configuración de la extensión de etiquetas del SDK web](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para obtener información detallada sobre todas las opciones de configuración.

Estos ajustes de configuración se establecen cada vez que se utiliza la extensión para enviar datos al Adobe.

## Configuración del SDK web mediante la biblioteca de JavaScript {#configure-js}

Ejecute el comando `configure`. Este comando es necesario para poder llamar a cualquier otro comando del SDK web, como [`sendEvent`](../sendevent/overview.md).

Se requieren las propiedades [`edgeConfigId`](edgeconfigid.md) y [`orgId`](orgid.md). Todas las demás propiedades son opcionales, según los requisitos de implementación de su organización.

Consulte la tabla de contenido de esta guía del usuario para obtener información detallada sobre cada uno de los comandos admitidos.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
