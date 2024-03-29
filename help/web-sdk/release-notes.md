---
title: Notas de la versión del SDK web de Adobe Experience Platform
description: Últimas notas de la versión del SDK web de Adobe Experience Platform.
keywords: SDK web de Adobe Experience Platform;SDK web de Platform;SDK web;notas de la versión;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 1%

---


# Notas de la versión

Este documento describe las notas de la versión del SDK web de Adobe Experience Platform.
Para obtener las últimas notas de la versión de la extensión de etiquetas del SDK web, consulte la [Notas de la versión de la extensión de etiquetas SDK web](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

>[!IMPORTANT]
>
>Google [ha anunciado](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) planea interrumpir la compatibilidad de Chrome con cookies de terceros en el segundo semestre de 2024. Por lo tanto, las cookies de terceros ya no serán compatibles con ninguno de los exploradores principales.
>
>Cuando se implemente este cambio, el Adobe dejará de admitir el `demdex` que se admite actualmente en el SDK web.

## Versión 2.19.2: 10 de enero de 2024

**Correcciones y mejoras**

* Se ha corregido un problema por el cual los errores de identidad enmascaraban otros errores y cambiaban los errores de identidad a advertencias.
* Se ha corregido un problema en el cual la parte inferior de las llamadas de página nunca se enviaban cuando había una parte superior de la llamada de página con `renderDecisions` establezca en `false`.
* Se ha corregido un problema en el cual el SDK web no podía leer identidades de dominios cruzados cuando había varios `adobe_mc` parámetros de cadena de consulta.

## Versión 2.19.1: 10 de noviembre de 2023

**Correcciones y mejoras**

* Se ha corregido un problema por el cual la matriz de propuestas devolvía de `sendEvent` llamadas siempre estaba vacío.

## Versión 2.19.0: 1 de noviembre de 2023

**Nuevas funciones**

* Se ha agregado compatibilidad para procesar mensajes en la aplicación desde Adobe Journey Optimizer.
* Se ha añadido la compatibilidad con [principio e final de los eventos de página](use-cases/top-bottom-page-events.md).
* Añadido [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) a la opción `sendEvent` para controlar la solicitud del ámbito de toda la página y la superficie predeterminada.

**Correcciones y mejoras**

* La personalización combinada muestra eventos juntos al procesar varios tipos de personalización.
* Se corrigió un problema en el cual los nombres de vistas de aplicaciones de una sola página distinguían entre mayúsculas y minúsculas.
* Se ha corregido un problema con los selectores de oferta personalizados DOM de sombra.

## Versión 2.18.0: 31 de julio de 2023

**Nuevas funciones**

* Se ha añadido la compatibilidad con [Anulaciones por comando del ID de la secuencia de datos](../datastreams/overrides.md).

**Correcciones y mejoras**

* Se ha corregido un problema por el cual los vínculos de salida no se clasificaban debido a que el dominio formaba parte de la consulta.
* Obsoleto `edgeConfigId` a favor de `datastreamId` en la configuración del SDK web.

## Versión 2.17.0: 17 de mayo de 2023

**Correcciones y mejoras**

* El SDK web ahora codifica los valores de destino de las cookies del Audience Manager, de forma similar a la [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=es).

## Versión 2.16.0: 25 de abril de 2023

**Nuevas funciones**

* Se ha añadido la compatibilidad con [anulaciones de configuración de secuencia de datos](../datastreams/overrides.md).

## Versión 2.15.0: 30 de marzo de 2023

**Nuevas funciones**

* Se ha añadido la compatibilidad con [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) clic en vínculo devolución de llamada.
* Se ha agregado compatibilidad con el rastreo de clics de Adobe Journey Optimizer.

**Correcciones y mejoras**

* La colección de vínculos ahora incluye el nombre del vínculo y la región del visitante.
* Se ha eliminado el error de consola para destinos URL fallidos.

## Versión 2.14.0: 25 de enero de 2023

* (Beta) Se ha agregado compatibilidad con superficies y propuestas de Adobe Journey Optimizer.

**Correcciones y mejoras**

* Se ha corregido un problema con las acciones de código personalizado del VEC de Adobe Target en el cual el código se insertaba en una ubicación alternativa que con [!DNL at.js].
* Se ha corregido un problema en el cual en algunos casos extremos el encabezado &quot;referente&quot; no se establecía correctamente en las solicitudes a la red perimetral.
* Se ha corregido un problema en el que [sugerencia de cliente del agente de usuario](/help/web-sdk/use-cases/client-hints.md) las propiedades se pueden establecer en un tipo incorrecto.
* Se ha corregido un problema en el que `placeContext.localTime` no coincide con el esquema.

## Versión 2.13.1: 13 de octubre de 2022

* Se ha corregido un problema en el cual la migración de visitantes no funcionaba si window.Visitor se definía después de configurar. Esto es especialmente un problema cuando se ejecuta con etiquetas de Adobe.
* Se ha corregido un problema en el que `device.screenWidth` y `device.screenHeight` se rellenaron como cadenas en algunos entornos.

## Versión 2.13.0: 28 de septiembre de 2022

**Nuevas funciones**

* Se ha añadido la compatibilidad con [Migración completa de página por página](home.md#migrating-to-web-sdk). El perfil de Adobe Target ahora se conservará a medida que un visitante se desplace entre las páginas de at.js y del SDK web.
* Se ha añadido compatibilidad configurable para [User-Agent Client Hints de alta entropía](/help/web-sdk/use-cases/client-hints.md).
* Se ha agregado compatibilidad con [`applyResponse`](/help/web-sdk/commands/applyresponse.md) comando. Esto permite la personalización híbrida a través de [API del servidor de red perimetral](../server-api/overview.md).
* Los vínculos del modo de control de calidad ahora funcionan en varias páginas.

**Correcciones y mejoras**

* Se ha corregido un problema en el cual las métricas de rastreo de clics de personalización no se actualizaban cuando el seguimiento de vínculos estaba deshabilitado.
* Se han actualizado los comandos para generar un error de validación cuando se especifican opciones desconocidas.
* El `_experience.decisioning.propositionEventType` ahora se rellena al enviar automáticamente eventos de personalización de visualización e interacción.
* Se ha añadido la validación del área de nombres duplicada para `getIdentity` comando.
* Se agregó la validación duplicada del ámbito de decisión para `sendEvent` comando.

## Versión 2.12.0: 29 de junio de 2022

* Cambiar las solicitudes a la red perimetral para utilizar `cluster` sugerencia de ubicación de cookies como parte de la dirección URL. Esto garantiza que los usuarios que cambian de ubicación (por ejemplo, a través de una VPN o conduciendo con dispositivos móviles, etc.) a mitad de la sesión tengan el mismo perfil personalizado.
* Consolide las funciones configuradas en la respuesta del comando getLibraryInfo.

## Versión 2.11.0: 13 de junio de 2022

**Nuevas funciones**

* Ahora puede ofrecer experiencias personalizadas con mayor precisión si comparte los ID de visitante entre aplicaciones móviles y contenido de la web móvil, así como entre dominios. Consulte la [documentación dedicada](identity/id-sharing.md) para obtener más información.
* Ahora puede procesar o ejecutar una matriz de propuestas desde [!DNL Adobe Target] en aplicaciones de una sola página, sin incrementar las métricas de analytics. Esto reduce los errores de creación de informes y aumenta la precisión del análisis. Consulte la [documentación dedicada](personalization/rendering-personalization-content.md#applypropositions) para obtener más información.
* Se ha añadido información adicional a `getLibraryInfo` incluido los comandos disponibles y la configuración final de la instancia.

**Correcciones y mejoras**

* Configuración de cookies actualizada para utilizar `sameSite="none"` y `secure` marcar en [!DNL HTTPS] páginas.
* Se ha corregido un problema en el cual el contenido personalizado no se aplicaba correctamente al usar el `eq` pseudoselector.
* Se ha corregido un problema en el que `localTimezoneOffset` podría fallar la validación del Experience Platform.

## Versión 2.10.1: 3 de mayo de 2022

* Se ha corregido un problema en el cual se creaban varios iframes persistentes para sincronizaciones de ID y destinos de segmento.

## Versión 2.10.0: 22 de abril de 2022

* Utilice un iframe persistente para todas las sincronizaciones de ID y destinos de segmento.
* Se ha corregido un problema por el cual las propuestas de métricas combinadas se duplicaban en la variable `sendEvent` resultado.

## Versión 2.9.0: 10 de marzo de 2022

* Se ha agregado compatibilidad con el seguimiento [!DNL control (default)] Experiencias de Adobe Target.
* Se han optimizado los eventos de cambio de vista para aplicaciones de una sola página. La notificación de visualización ahora se incluye con el evento de cambio de vista cuando se representan experiencias personalizadas.
* Advertencia de consola eliminada cuando no `eventType` está presente.
* Se ha corregido un problema por el que `propositions` La propiedad solo se ha devuelto desde un `sendEvent` cuando se solicitaron o recuperaron experiencias de la caché. El `propositions` ahora, la propiedad siempre se definirá como una matriz.
* Se ha corregido un problema en el cual los contenedores ocultos no se mostraban cuando se devolvía un error desde la red de Edge.
* Se ha corregido un problema en el cual los eventos de interacción no se contaban en Adobe Target. Esto se solucionó añadiendo el nombre de la vista al XDM en web.webPageDetails.viewName.
* Corrección de vínculos de documentación dañados en los mensajes de la consola.

## Versión 2.8.0: 19 de enero de 2022

* Compatibilidad con selectores DOM en la sombra para la personalización.
* Se ha cambiado el nombre de tipos de eventos de personalización. (`display` y `click` llegar a `decisioning.propositionDisplay` y `decisioning.propositionInteract`)
* Se ha corregido un problema por el cual las ofertas de HTML con etiquetas de scripts en línea añadían las etiquetas de scripts dos veces a la página aunque el script solo se ejecutara una vez.

## Versión 2.7.0: 26 de octubre de 2021

* Exponer información adicional de la red perimetral en el valor devuelto desde `sendEvent`, incluido `inferences` y `destinations`. El formato de estas propiedades puede cambiar a medida que estas funciones se implementan como parte de una versión beta.

## Versión 2.6.4: 7 de septiembre de 2021

* Se ha corregido un problema por el cual se aplicaban acciones de Adobe Target del HTML de conjunto a `head` estaban reemplazando todo el `head` contenido. Ahora, las acciones del HTML se aplican al `head` Los elementos de se cambian a HTML de datos anexados.

## Versión 2.6.3: 16 de agosto de 2021

* Se ha corregido un problema en el cual los objetos no destinados al uso público se exponían a través de la promesa resuelta del `configure` comando.

## Versión 2.6.2: 4 de agosto de 2021

* Se ha corregido un problema por el que una advertencia sobre la obsolescencia de `result.decisions` (proporcionado por el `sendEvent` ) se registraría en la consola incluso cuando el `result.decisions` no se estaba accediendo a la propiedad. No se registrará ninguna advertencia al acceder a `result.decisions` , pero la propiedad sigue en desuso.

## Versión 2.6.1: 29 de julio de 2021

* Se ha corregido un problema en el cual al procesar la personalización para una vista de aplicación de una sola página sin contenido de personalización, se producía un error y se devolvía la promesa del `sendEvent` comando que se va a rechazar.

## Versión 2.6.0: 27 de julio de 2021

* Proporciona más contenido de personalización en la `sendEvent` promesa resuelta, incluidos los tokens de respuesta de Adobe Target. Si la variable `sendEvent` se ejecuta, se devuelve una promesa, que finalmente se resuelve con una `result` objeto que contiene información recibida del servidor. Anteriormente, este objeto de resultado incluía una propiedad denominada `decisions`. Esta `decisions` La propiedad se ha desaprobado. Una nueva propiedad, `propositions`, se ha añadido. Esta nueva propiedad proporciona a los clientes acceso a más contenido de personalización, como [tokens de respuesta](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Versión 2.5.0: junio de 2021

* Se ha agregado compatibilidad con ofertas de personalización de redireccionamiento.
* Las anchuras y alturas de ventanilla recopiladas automáticamente que sean valores negativos ya no se enviarán al servidor.
* Cuando se cancela un evento devolviendo `false` de un `onBeforeEventSend` callback, ahora se registra un mensaje.
* Se ha corregido un problema en el cual se incluían fragmentos específicos de datos XDM destinados a un solo evento en varios eventos.

## Versión 2.4.0: marzo de 2021

* Ahora, el SDK se puede instalar como [Paquete NPM](/help/web-sdk/install/npm.md).
* Se ha añadido la compatibilidad con `out` opción cuando [configuración del consentimiento predeterminado](/help/web-sdk/commands/configure/defaultconsent.md), que descarta todos los eventos hasta que se recibe el consentimiento (el existente `pending` la opción pone en cola eventos y los envía una vez recibido el consentimiento).
* El [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) ahora, la devolución de llamada se puede utilizar para evitar que se envíe un evento.
* Ahora se utiliza un grupo de campos de esquema XDM en lugar de `meta.personalization` al enviar eventos sobre contenido personalizado que se procesa o se hace clic en él.
* El [`getIdentity`](/help/web-sdk/commands/getidentity.md) ahora, el comando devuelve el ID de región perimetral junto con la identidad.
* Las advertencias y los errores recibidos del servidor se han mejorado y se gestionan de forma más adecuada.
* Se ha agregado compatibilidad con el estándar de Consentimiento de Adobe 2.0 para [`setConsent`](/help/web-sdk/commands/setconsent.md) comando.
* Cuando se reciben, las preferencias de consentimiento tienen un cifrado hash y se almacenan en el almacenamiento local para una integración optimizada entre CMP, el SDK web de Platform y la red perimetral de Platform. Si está recopilando las preferencias de consentimiento, ahora le recomendamos que llame a `setConsent` en cada carga de página.
* Dos [ganchos de monitorización](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` y `onCommandRejected`, se han añadido.
* Corrección de errores: Los eventos de notificación de interacción de personalización contenían información duplicada sobre la misma actividad cuando un usuario navegaba a una nueva vista de aplicación de una sola página, volvía a la vista original y hacía clic en un elemento que cumplía los requisitos para la conversión.
* Corrección de errores: Si el primer evento enviado por el SDK hubiera tenido `documentUnloading` establezca en `true`, [`sendBeacon`](https://developer.mozilla.org/es-ES/docs/Web/API/Navigator/sendBeacon) se utilizaría para enviar el evento, lo que da como resultado un error con respecto a una identidad que no se está estableciendo.

## Versión 2.3.0: noviembre de 2020

* Se ha agregado compatibilidad con nonce para permitir políticas de seguridad de contenido más estrictas.
* Se ha agregado compatibilidad con la personalización para aplicaciones de una sola página.
* Se ha mejorado la compatibilidad con otro código JavaScript en la página que podría sobrescribirse `window.console` API.
* Corrección de errores: `sendBeacon` no se estaba utilizando cuando `documentUnloading` se estableció en `true` o cuando se realizaba un seguimiento automático de los clics en vínculos.
* Corrección de errores: No se rastrearía automáticamente un vínculo si el elemento de anclaje contuviera contenido de HTML.
* Corrección de errores: Algunos errores del explorador que contienen un de solo lectura `message` Las propiedades de no se gestionaban correctamente, lo que provocaba que se mostrara un error diferente al cliente.
* Corrección de errores: La ejecución del SDK dentro de un iframe produciría un error si la página del HTML del iframe era de un subdominio diferente a la página del HTML de la ventana principal.

## Versión 2.2.0: octubre de 2020

* Corrección de errores: El objeto Opt-in impedía que el SDK web realizara llamadas al `idMigrationEnabled` es `true`.
* Corrección de errores: Haga que el SDK web tenga en cuenta las solicitudes que deberían devolver ofertas de personalización para evitar un problema de parpadeo.

## Versión 2.1.0: agosto de 2020

* Retire el `syncIdentity` y admitir el paso de esos ID en el `sendEvent` comando.
* Compatibilidad con el estándar de consentimiento IAB 2.0.
* Compatibilidad para pasar ID adicionales en `setConsent` comando.
* Compatibilidad con la anulación de `datasetId` en el `sendEvent` comando.
* Enlaces de supervisión de soporte ([Más información](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Aprobado `environment: browser` en la implementación detalla los datos de contexto.
