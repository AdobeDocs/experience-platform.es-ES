---
title: Configuración del SDK web de Adobe Experience Platform
description: Utilice el comando configure para establecer la configuración necesaria al utilizar el SDK web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configuración del SDK web de Adobe Experience Platform

La configuración del SDK web se realiza con `configure` comando. La configuración del SDK web es un paso vital y necesario que debe producirse cada vez que se utiliza la biblioteca o la extensión de etiqueta.

## Ajustes de configuración que utilizan la extensión de etiqueta del SDK web

Vaya a [página de configuración de extensión de etiquetas](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.

Estos ajustes de configuración se establecen cada vez que se utiliza la extensión para enviar datos al Adobe.

## Ajustes de configuración que utilizan la biblioteca JavaScript del SDK web

Ejecute el `configure` comando. Este comando es necesario para poder llamar a cualquier otro comando del SDK web, como [`sendEvent`](../sendevent/overview.md). Las propiedades [`edgeConfigId`](edgeconfigid.md) y [`orgId`](orgid.md) son obligatorios. Todas las demás propiedades son opcionales, según los requisitos de implementación de su organización.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
