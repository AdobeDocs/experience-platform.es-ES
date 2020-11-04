---
title: Notas de la versión de Adobe Experience Platform Web SDK
seo-title: Notas de la versión de Adobe Experience Platform Web SDK
description: Notas de la versión de Adobe Experience Platform Web SDK.
seo-description: Notas de la versión de Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---


# Notas de la versión

## Versión 2.3.0

* Se añadió la compatibilidad nonce para permitir políticas de seguridad de contenido más estrictas.
* Añadida compatibilidad con la personalización para aplicaciones de una sola página.
* Se ha mejorado la compatibilidad con otros códigos JavaScript en la página que pueden estar sobrescribiendo `window.console` las API.
* Corrección de errores: `sendBeacon` no se usaba cuando `documentUnloading` se establecía en `true` o cuando se rastreaban automáticamente los clics en vínculos.
* Corrección de errores: Un vínculo no se seguiría automáticamente si el elemento de anclaje contenía contenido HTML.
* Corrección de errores: Algunos errores del explorador que contenían una propiedad de sólo lectura no se gestionaban correctamente, lo que daba como resultado que se mostrara un error diferente al cliente. `message`
* Corrección de errores: Si se ejecuta el SDK en un iframe, se producirá un error si la página HTML del iframe procede de un subdominio diferente al de la página HTML de la ventana principal.

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
