---
title: Notas de la versión de Adobe Experience Platform Web SDK
seo-title: Notas de la versión de Adobe Experience Platform Web SDK
description: Notas de la versión de Adobe Experience Platform Web SDK.
seo-description: Notas de la versión de Adobe Experience Platform Web SDK.
translation-type: tm+mt
source-git-commit: c1cb64dc297d9133a8e3ef18c97cbd5fac5b0cd6
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# Notas de la versión

## Versión 2.1.0

* Compatibilidad con IAB 2.0 Consent Standard.
* Compatibilidad con la transmisión de ID adicionales en el `setConsent` comando.
* Compatibilidad con la anulación del `datasetId` comando en el `sendEvent` .
* Quite el `syncIdentity` comando y admita la transferencia de esos ID en el `sendEvent` comando.
* Monitores de aleación de soporte ([Más información)](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Pasar `environment: browser` los datos de contexto de detalles de implementación.
