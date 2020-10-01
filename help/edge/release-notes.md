---
title: Notas de la versión de Adobe Experience Platform Web SDK
seo-title: Notas de la versión de Adobe Experience Platform Web SDK
description: Notas de la versión de Adobe Experience Platform Web SDK.
seo-description: Notas de la versión de Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 738dfe782ee7d6bef06d14910e0c26540b0ec734
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Notas de la versión

## Versión 2.2.0

* Corrección de errores: El objeto de inclusión bloqueaba a Alloy de realizar llamadas cuando `idMigrationEnabled` lo está `true`.
* Corrección de errores: Haga que Alloy tenga en cuenta las solicitudes que deben devolver ofertas de personalización para evitar un problema parpadeante.

## Versión 2.1.0

* Quite el `syncIdentity` comando y admita la transferencia de esos ID en el `sendEvent` comando.
* Compatibilidad con IAB 2.0 Consent Standard.
* Compatibilidad con la transmisión de ID adicionales en el `setConsent` comando.
* Compatibilidad con la anulación del `datasetId` comando en el `sendEvent` .
* Monitores de aleación de soporte ([Más](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)información)
* Pasar `environment: browser` los datos de contexto de detalles de implementación.
