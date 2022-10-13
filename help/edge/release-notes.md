---
title: Notas de la versión del SDK web de Adobe Experience Platform
description: Últimas notas de la versión del SDK web de Adobe Experience Platform.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;notas de la versión;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: f406ad74da00a7f4bf7ef1b52bee59cd91435d8f
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---


# Notas de la versión

Este documento cubre las notas de la versión del SDK web de Adobe Experience Platform.
Para ver las últimas notas de la versión de la extensión de etiqueta del SDK web, consulte la [Notas de la versión de la extensión de etiqueta del SDK web](extension/web-sdk-ext-release-notes.md).

## Versión 2.13.1: 13 de octubre de 2022

* Se ha corregido un problema en el cual la migración de visitantes no funcionaba si window.Visitor se definía después de la configuración. Este es un problema especial al ejecutar con etiquetas de Adobe.
* Se ha corregido un problema en el cual `device.screenWidth` y `device.screenHeight` se rellenaron como cadenas en algunos entornos.

## Versión 2.13.0: 28 de septiembre de 2022

**Nuevas funciones**

* Se ha agregado compatibilidad con [Migración de página por página completa](home.md#migrating-to-web-sdk). El perfil de Adobe Target ahora se conservará cuando un visitante se desplace entre at.js y las páginas del SDK web.
* Se ha agregado compatibilidad configurable para [sugerencias de cliente de agente de usuario de alta entropía](fundamentals/user-agent-client-hints.md#high-entropy).
* Se ha agregado compatibilidad con el nuevo `applyResponse` comando. Esto permite la personalización híbrida mediante la variable [API de servidor de red perimetral](../server-api/overview.md).
* Los vínculos de modo de control de calidad ahora funcionan en varias páginas.

**Correcciones y mejoras**

* Se ha corregido un problema por el cual las métricas de rastreo de clics de personalización no se actualizaban cuando el seguimiento de vínculos estaba desactivado.
* Se han actualizado los comandos para generar un error de validación cuando se especifican opciones desconocidas.
* La variable `_experience.decisioning.propositionEventType` ahora se rellena al enviar automáticamente eventos de personalización de visualización e interacción.
* Se ha agregado la validación de espacio de nombres duplicada para la variable `getIdentity` comando.
* Se ha agregado la validación duplicada del ámbito de decisión para la variable `sendEvent` comando.

## Versión 2.12.0: 29 de junio de 2022

* Cambie las solicitudes a la red perimetral para usar la variable `cluster` indicio de ubicación de la cookie como parte de la dirección URL. Esto garantiza que los usuarios que cambian de ubicación (por ejemplo, a través de una VPN o conduciendo con dispositivos móviles, etc.) durante la sesión tengan el mismo perfil de personalización y tengan el mismo perfil.
* Consolide las funciones configuradas en la respuesta del comando getLibraryInfo.

## Versión 2.11.0: 13 de junio de 2022

**Nuevas funciones**

* Ahora puede ofrecer experiencias personalizadas de forma más precisa, compartiendo los ID de visitante entre aplicaciones móviles y contenido web móvil, así como entre dominios. Consulte la [documentación dedicada](identity/id-sharing.md) para obtener más información.
* Ahora puede procesar o ejecutar una matriz de propuestas desde [!DNL Adobe Target] en aplicaciones de una sola página, sin incrementar las métricas de análisis. Esto reduce los errores en los informes y aumenta la precisión de los análisis. Consulte la [documentación dedicada](personalization/rendering-personalization-content.md#applypropositions) para obtener más información.
* Se ha añadido información adicional al `getLibraryInfo` incluido los comandos disponibles y la configuración final de la instancia.

**Correcciones y mejoras**

* Se ha actualizado la configuración de cookies para usar `sameSite="none"` y `secure` marcar en [!DNL HTTPS] páginas.
* Se ha corregido un problema por el cual el contenido personalizado no se aplicaba correctamente al usar la variable `eq` pseudo selector.
* Se ha corregido un problema en el cual `localTimezoneOffset` podría fallar la validación del Experience Platform.

## Versión 2.10.1: 3 de mayo de 2022

* Se ha corregido un problema por el cual se creaban varios iframes persistentes para sincronizar los ID y segmentar los destinos.

## Versión 2.10.0: 22 de abril de 2022

* Utilice un iframe persistente para todas las sincronizaciones de ID y los destinos de segmento.
* Se ha corregido un problema por el cual las propuestas de métricas combinadas se duplicaban en la variable `sendEvent` resultado.

## Versión 2.9.0: 10 de marzo de 2022

* Se ha agregado compatibilidad con el seguimiento [!DNL control (default)] Experiencias de Adobe Target.
* Se han optimizado los eventos view-change para aplicaciones de una sola página. La notificación de visualización ahora se incluye con el evento de cambio de vista cuando se procesan experiencias personalizadas.
* Se ha eliminado la advertencia de la consola cuando no `eventType` está presente.
* Se ha corregido un problema en el cual la variable `propositions` la propiedad solo se devolvió desde un `sendEvent` cuando se solicitaron o recuperaron experiencias de la caché. La variable `propositions` ahora siempre se definirá como una matriz.
* Se ha corregido un problema en el cual los contenedores ocultos no se mostraban cuando se devolvía un error desde Adobe Experience Edge.
* Se ha corregido un problema por el cual los eventos de interacción no se contaban en Adobe Target. Esto se corrigió agregando el nombre de vista al XDM en web.webPageDetails.viewName.
* Se han corregido los vínculos de documentación dañados en los mensajes de consola.

## Versión 2.8.0: 19 de enero de 2022

* Compatibilidad con selectores DOM de sombra para la personalización.
* Se ha cambiado el nombre de los tipos de eventos de personalización. (`display` y `click` se `decisioning.propositionDisplay` y `decisioning.propositionInteract`)
* Se ha corregido un problema en el cual las ofertas de HTML con etiquetas de script en línea agregaban dos veces las etiquetas de script a la página aunque el script solo se ejecutara una vez.

## Versión 2.7.0: 26 de octubre de 2021

* Exponer información adicional de Experience Edge en el valor devuelto de `sendEvent`, incluyendo `inferences` y `destinations`. El formato de estas propiedades puede cambiar, ya que estas funciones se están desplegando como parte de una versión beta. Para obtener más información, consulte [Seguimiento de eventos.](fundamentals/tracking-events.md)

## Versión 2.6.4: 7 de septiembre de 2021

* Se ha corregido un problema por el cual se establecían acciones de Adobe Target de HTML aplicadas al `head` reemplazaban a todo `head` contenido. Ahora se definen las acciones del HTML aplicadas al `head` se cambian a HTML de datos adjuntos.

## Versión 2.6.3: 16 de agosto de 2021

* Se ha corregido un problema que hacía que los objetos que no estaban pensados para uso público se mostraran mediante la promesa resuelta del `configure` comando.

## Versión 2.6.2: 4 de agosto de 2021

* Se ha corregido un problema por el cual se mostraba una advertencia sobre el desuso de `result.decisions` (proporcionado por el `sendEvent` ) se registraría en la consola incluso cuando `result.decisions` no se estaba accediendo a la propiedad. No se registrará ninguna advertencia al acceder a la variable `result.decisions` , pero la propiedad sigue en desuso.

## Versión 2.6.1: 29 de julio de 2021

* Se ha corregido un problema en el cual la personalización de renderización para una vista de aplicación de una sola página que no tiene contenido de personalización generaba un error y causaba la promesa devuelta por la variable `sendEvent` para rechazar.

## Versión 2.6.0: 27 de julio de 2021

* Proporciona más contenido personalizado en la variable `sendEvent` promesa resuelta, incluidos los tokens de respuesta de Adobe Target. Cuando la variable `sendEvent` se ejecuta, se devuelve una promesa que finalmente se resuelve con un `result` que contiene información recibida del servidor. Anteriormente, este objeto de resultado incluía una propiedad denominada `decisions`. Esta `decisions` se ha desaprobado. Una nueva propiedad, `propositions`, se ha añadido. Esta nueva propiedad proporciona a los clientes acceso a más contenido personalizado, incluyendo [tokens de respuesta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Versión 2.5.0: junio de 2021

* Se ha agregado compatibilidad con ofertas de personalización de redireccionamiento.
* Los anchos y las alturas de las ventanillas que se recopilan automáticamente y que son valores negativos ya no se enviarán al servidor.
* Cuando se cancela un evento al devolver `false` de un `onBeforeEventSend` llamada de retorno, ahora se registra un mensaje.
* Se ha corregido un problema por el cual partes específicas de datos XDM destinados a un solo evento se incluían en varios eventos.

## Versión 2.4.0: marzo de 2021

* Ahora el SDK puede ser [instalado como paquete npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=es).
* Se ha agregado compatibilidad con un `out` cuando [configuración del consentimiento predeterminado](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), que descarta todos los eventos hasta que se recibe el consentimiento (la variable `pending` pone en cola los eventos y los envía una vez recibido el consentimiento).
* La variable [Llamada de retorno onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) ahora se puede utilizar para evitar que se envíe un evento.
* Ahora utiliza un grupo de campos de esquema XDM en lugar de `meta.personalization` al enviar eventos sobre el contenido personalizado que se representa o en el que se hace clic.
* La variable [getIdentity, comando](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) ahora devuelve el ID de región perimetral junto con la identidad.
* Las advertencias y los errores recibidos del servidor se han mejorado y se gestionan de forma más adecuada.
* Se ha agregado compatibilidad con [Consentimiento de Adobe 2.0 estándar](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Las preferencias de consentimiento, cuando se reciben, se colocan en hash y se almacenan en el almacenamiento local para lograr una integración optimizada entre CMP, Platform Web SDK y Platform Edge Network. Si recopila preferencias de consentimiento, ahora le recomendamos que llame a `setConsent` en cada carga de página.
* Two [monitorización de enlaces](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` y `onCommandRejected`, se han añadido.
* Corrección de errores: Los eventos de notificación de interacción de personalización contendrían información duplicada sobre la misma actividad cuando un usuario navegaba a una nueva vista de aplicación de una sola página, regresaba a la vista original y hacía clic en un elemento que cumplía los requisitos para la conversión.
* Corrección de errores: Si el primer evento enviado por el SDK tenía `documentUnloading` configure como `true`, [`sendBeacon`](https://developer.mozilla.org/es-ES/docs/Web/API/Navigator/sendBeacon) se utilizará para enviar el evento, lo que resulta en un error con respecto a que no se establece una identidad.

## Versión 2.3.0: noviembre de 2020

* Se ha agregado compatibilidad nonce para permitir políticas de seguridad de contenido más estrictas.
* Se ha agregado compatibilidad con la personalización para aplicaciones de una sola página.
* Se ha mejorado la compatibilidad con otros códigos JavaScript en la página que pueden estar sobrescribiendo `window.console` API.
* Corrección de errores: `sendBeacon` no se estaba usando cuando `documentUnloading` se estableció en `true` o cuando se rastrearon automáticamente los clics en vínculos.
* Corrección de errores: Un vínculo no se seguiría automáticamente si el elemento de anclaje contuviera contenido de HTML.
* Corrección de errores: Ciertos errores del explorador que contienen solo lectura `message` no se gestionaban correctamente, lo que provocaba que se mostrara un error diferente al cliente.
* Corrección de errores: Si se ejecuta el SDK dentro de un iframe, se producirá un error si la página HTML del iframe procede de un subdominio diferente al de la página HTML de la ventana principal.

## Versión 2.2.0: octubre de 2020

* Corrección de errores: El objeto Opt-in bloqueaba a Alloy de realizar llamadas cuando `idMigrationEnabled` es `true`.
* Corrección de errores: Haga que Alloy tenga en cuenta las solicitudes que deben devolver ofertas de personalización para evitar un problema que parpadee.

## Versión 2.1.0: agosto de 2020

* Elimine el `syncIdentity` y admiten pasar esos ID en la variable `sendEvent` comando.
* Compatibilidad con el estándar de consentimiento IAB 2.0.
* Compatibilidad para pasar ID adicionales en `setConsent` comando.
* Compatibilidad con la anulación de la función `datasetId` en el `sendEvent` comando.
* Monitores de alertas de compatibilidad ([Más información](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pass `environment: browser` en los datos de contexto de los detalles de implementación.
