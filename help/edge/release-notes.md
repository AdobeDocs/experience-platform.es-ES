---
title: Notas de la versión del SDK web de Adobe Experience Platform
description: Últimas notas de la versión del SDK web de Adobe Experience Platform.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;notas de la versión;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 5%

---


# Notas de la versión

## Versión 2.3.0

* Se añadió la compatibilidad nonce para permitir políticas de seguridad de contenido más estrictas.
* Añadida compatibilidad con la personalización para aplicaciones de una sola página.
* Se ha mejorado la compatibilidad con otros códigos JavaScript en la página que pueden estar sobrescribiendo las `window.console` API.
* Corrección de errores: `sendBeacon` no se estaba utilizando cuando `documentUnloading` se configuró en `true` o cuando se rastrearon automáticamente los clics en vínculos.
* Corrección de errores: Un vínculo no se seguiría automáticamente si el elemento de anclaje contenía contenido HTML.
* Corrección de errores: Algunos errores del explorador que contenían una propiedad `message` de sólo lectura no se gestionaban correctamente, lo que daba como resultado que se mostrara un error diferente al cliente.
* Corrección de errores: Si se ejecuta el SDK en un iframe, se producirá un error si la página HTML del iframe procede de un subdominio diferente al de la página HTML de la ventana principal.

## Versión 2.2.0

* Corrección de errores: El objeto de inclusión bloqueaba que Alloy realizara llamadas cuando `idMigrationEnabled` es `true`.
* Corrección de errores: Haga que Alloy tenga en cuenta las solicitudes que deben devolver ofertas de personalización para evitar un problema parpadeante.

## Versión 2.1.0

* Quite el comando `syncIdentity` y admita que se pasen esos ID en el comando `sendEvent`.
* Compatibilidad con IAB 2.0 Consent Standard.
* Admitir la transmisión de ID adicionales en el comando `setConsent`.
* Compatibilidad con la anulación de `datasetId` en el comando `sendEvent`.
* Monitores de aleación de soporte ([Más información](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pase `environment: browser` en los datos de contexto de detalles de implementación.
