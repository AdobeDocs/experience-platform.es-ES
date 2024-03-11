---
title: Configuración del SDK web de Adobe Experience Platform
description: Utilice el comando configure para establecer la configuración necesaria al utilizar el SDK web.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Configuración del SDK web de Adobe Experience Platform

La configuración del SDK web se realiza con `configure` comando. La configuración del SDK web es un paso vital y necesario que debe producirse cada vez que se utiliza la biblioteca o la extensión de etiqueta.

## Configuración del SDK web mediante la extensión de etiqueta {#configure-tag-extension}

Siga los pasos a continuación para configurar el SDK web a través de la extensión de etiqueta.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Vaya a la [Página de configuración de extensión de etiqueta de SDK web](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para obtener información detallada sobre todas las opciones de configuración.

Estos ajustes de configuración se establecen cada vez que se utiliza la extensión para enviar datos al Adobe.

## Configuración del SDK web mediante la biblioteca JavaScript de {#configure-js}

Ejecute el `configure` comando. Este comando es necesario para poder llamar a cualquier otro comando del SDK web, como [`sendEvent`](../sendevent/overview.md).

El [`edgeConfigId`](edgeconfigid.md) y [`orgId`](orgid.md) se requieren las propiedades. Todas las demás propiedades son opcionales, según los requisitos de implementación de su organización.

Consulte la tabla de contenido de esta guía del usuario para obtener información detallada sobre cada uno de los comandos admitidos.

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
