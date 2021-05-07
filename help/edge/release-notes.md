---
title: Notas de la versión del SDK web de Adobe Experience Platform
description: Últimas notas de la versión del SDK web de Adobe Experience Platform.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;notas de la versión;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 5%

---

# Notas de la versión

## Versión 2.4.0, marzo de 2021

* El SDK ahora puede [instalarse como un paquete npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Se agregó compatibilidad con una opción `out` al [configurar el consentimiento predeterminado](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), que descarta todos los eventos hasta que se recibe el consentimiento (la opción `pending` existente coloca en cola los eventos y los envía una vez que se recibe el consentimiento).
* Ahora se puede utilizar la [devolución de llamada onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) para evitar que se envíe un evento.
* Ahora utiliza un grupo de campos de esquema XDM en lugar de `meta.personalization` al enviar eventos sobre el contenido personalizado que se está procesando o haciendo clic en él.
* El comando [getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) ahora devuelve el ID de región perimetral junto con la identidad.
* Las advertencias y los errores recibidos del servidor se han mejorado y se gestionan de forma más adecuada.
* Se agregó compatibilidad con el estándar [Consent 2.0 del Adobe](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Las preferencias de consentimiento, cuando se reciben, se colocan en hash y se almacenan en el almacenamiento local para lograr una integración optimizada entre CMP, Platform Web SDK y Platform Edge Network. Si está recopilando preferencias de consentimiento, ahora le recomendamos que llame a `setConsent` en cada carga de página.
* Se han añadido dos [enlaces de monitorización](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` y `onCommandRejected`.
* Corrección de errores: Los eventos de notificación de interacción de personalización contendrían información duplicada sobre la misma actividad cuando un usuario navegaba a una nueva vista de aplicación de una sola página, regresaba a la vista original y hacía clic en un elemento que cumplía los requisitos para la conversión.
* Corrección de errores: Si el primer evento enviado por el SDK tenía `documentUnloading` establecido en `true`, [`sendBeacon`](https://developer.mozilla.org/es-ES/docs/Web/API/Navigator/sendBeacon) se utilizaría para enviar el evento, lo que provocaba un error en cuanto a la identidad que no se estaba estableciendo.

## Versión 2.3.0, noviembre de 2020

* Se ha agregado compatibilidad nonce para permitir políticas de seguridad de contenido más estrictas.
* Se ha agregado compatibilidad con la personalización para aplicaciones de una sola página.
* Se ha mejorado la compatibilidad con otros códigos JavaScript en la página que pueden estar sobrescribiendo las API `window.console`.
* Corrección de errores: `sendBeacon` no se estaba usando cuando `documentUnloading` estaba establecido en `true` o cuando se rastreaban automáticamente los clics en vínculos.
* Corrección de errores: Un vínculo no se seguiría automáticamente si el elemento de anclaje contuviera contenido HTML.
* Corrección de errores: Algunos errores del explorador que contenían una propiedad `message` de solo lectura no se gestionaban correctamente, lo que provocaba que se mostrara un error diferente al cliente.
* Corrección de errores: Si se ejecuta el SDK dentro de un iframe, se producirá un error si la página HTML del iframe procede de un subdominio diferente al de la página HTML de la ventana principal.

## Versión 2.2.0, octubre de 2020

* Corrección de errores: El objeto Opt-in impedía que Alloy realizara llamadas cuando `idMigrationEnabled` es `true`.
* Corrección de errores: Haga que Alloy tenga en cuenta las solicitudes que deben devolver ofertas de personalización para evitar un problema que parpadee.

## Versión 2.1.0, agosto de 2020

* Elimine el comando `syncIdentity` y permita que se pasen esos ID en el comando `sendEvent`.
* Compatibilidad con el estándar de consentimiento IAB 2.0.
* Compatibilidad para pasar ID adicionales en el comando `setConsent`.
* Compatibilidad con la anulación de `datasetId` en el comando `sendEvent`.
* Monitores de alertas de soporte ([Más información](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pase `environment: browser` en los datos de contexto de los detalles de implementación.
