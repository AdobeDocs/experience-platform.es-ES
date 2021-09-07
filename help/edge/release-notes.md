---
title: Notas de la versión del SDK web de Adobe Experience Platform
description: Últimas notas de la versión del SDK web de Adobe Experience Platform.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;notas de la versión;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: f5d3c5911357d4b76e4d38564bf637e2549469d6
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 4%

---

# Notas de la versión

## Versión 2.6.4: 7 de septiembre de 2021

* Se ha corregido un problema en el cual las acciones de Adobe Target HTML definidas aplicadas al elemento `head` reemplazaban todo el contenido `head`. Ahora, las acciones HTML definidas aplicadas al elemento `head` se cambian para anexar HTML.

## Versión 2.6.3: 16 de agosto de 2021

* Se ha corregido un problema que hacía que los objetos que no estaban pensados para uso público se mostraran mediante la promesa resuelta del comando `configure`.

## Versión 2.6.2: 4 de agosto de 2021

* Se ha corregido un problema que hacía que se registrara en la consola una advertencia sobre la desaprobación de `result.decisions` (proporcionada por el comando `sendEvent`) incluso cuando no se accedía a la propiedad `result.decisions` . No se registrará ninguna advertencia al acceder a la propiedad `result.decisions`, pero la propiedad sigue en desuso.

## Versión 2.6.1: 29 de julio de 2021

* Se ha corregido un problema en el cual la personalización de renderización para una vista de aplicación de una sola página que no tiene contenido de personalización generaba un error y provocaba que se rechazara la promesa devuelta por el comando `sendEvent`.

## Versión 2.6.0: 27 de julio de 2021

* Proporciona más contenido de personalización en la promesa resuelta `sendEvent`, incluidos los tokens de respuesta de Adobe Target. Cuando se ejecuta el comando `sendEvent`, se devuelve una promesa, que finalmente se resuelve con un objeto `result` que contiene información recibida del servidor. Anteriormente, este objeto de resultado incluía una propiedad denominada `decisions`. Esta propiedad `decisions` ha quedado obsoleta. Se ha agregado una nueva propiedad, `propositions`. Esta nueva propiedad proporciona a los clientes acceso a más contenido de personalización, incluidos [tokens de respuesta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Versión 2.5.0: junio de 2021

* Se ha agregado compatibilidad con ofertas de personalización de redireccionamiento.
* Los anchos y las alturas de las ventanillas que se recopilan automáticamente y que son valores negativos ya no se enviarán al servidor.
* Cuando se cancela un evento devolviendo `false` una llamada de retorno `onBeforeEventSend`, ahora se registra un mensaje.
* Se ha corregido un problema por el cual partes específicas de datos XDM destinados a un solo evento se incluían en varios eventos.

## Versión 2.4.0: marzo de 2021

* El SDK ahora puede [instalarse como un paquete npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=es).
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

## Versión 2.3.0: noviembre de 2020

* Se ha agregado compatibilidad nonce para permitir políticas de seguridad de contenido más estrictas.
* Se ha agregado compatibilidad con la personalización para aplicaciones de una sola página.
* Se ha mejorado la compatibilidad con otros códigos JavaScript en la página que pueden estar sobrescribiendo las API `window.console`.
* Corrección de errores: `sendBeacon` no se estaba usando cuando `documentUnloading` estaba establecido en `true` o cuando se rastreaban automáticamente los clics en vínculos.
* Corrección de errores: Un vínculo no se seguiría automáticamente si el elemento de anclaje contuviera contenido HTML.
* Corrección de errores: Algunos errores del explorador que contenían una propiedad `message` de solo lectura no se gestionaban correctamente, lo que provocaba que se mostrara un error diferente al cliente.
* Corrección de errores: Si se ejecuta el SDK dentro de un iframe, se producirá un error si la página HTML del iframe procede de un subdominio diferente al de la página HTML de la ventana principal.

## Versión 2.2.0: octubre de 2020

* Corrección de errores: El objeto Opt-in impedía que Alloy realizara llamadas cuando `idMigrationEnabled` es `true`.
* Corrección de errores: Haga que Alloy tenga en cuenta las solicitudes que deben devolver ofertas de personalización para evitar un problema que parpadee.

## Versión 2.1.0: agosto de 2020

* Elimine el comando `syncIdentity` y permita que se pasen esos ID en el comando `sendEvent`.
* Compatibilidad con el estándar de consentimiento IAB 2.0.
* Compatibilidad para pasar ID adicionales en el comando `setConsent`.
* Compatibilidad con la anulación de `datasetId` en el comando `sendEvent`.
* Monitores de alertas de soporte ([Más información](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pase `environment: browser` en los datos de contexto de los detalles de implementación.
