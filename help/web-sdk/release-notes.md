---
title: Notas de la versión del SDK web de Adobe Experience Platform
description: Últimas notas de la versión del SDK web de Adobe Experience Platform.
keywords: SDK web de Adobe Experience Platform;SDK web de Platform;SDK web;notas de la versión;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: c1fb9fe7d4863e316b824d6c8dd2ff0d3405d7ea
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 2%

---


# Notas de la versión

Este documento describe las notas de la versión del SDK web de Adobe Experience Platform.
Para obtener las últimas notas de la versión de la extensión de etiquetas SDK web, consulte las [notas de la versión de la extensión de etiquetas SDK web](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Versión 2.23.0: 19 de septiembre de 2024

**Nuevas funciones**

- Se ha agregado compatibilidad para solicitar la [ID principal](identity/overview.md#tracking-coreid-web-sdk) en el comando [getIdentity](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library).

**Correcciones y mejoras**

- Se ha corregido un problema por el cual las cookies no se escribían correctamente al ejecutar el SDK web localmente.

## Versión 2.22.0: 22 de agosto de 2024

**Nuevas funciones**

- Se ha añadido compatibilidad con los enlaces de monitorización de personalización.

**Correcciones y mejoras**

- Se ha eliminado la compatibilidad con Internet Explorer, lo que reduce el tamaño del gzip de la biblioteca en un 9 %.
- Se ha corregido un problema por el cual los detalles del vínculo de Activity Map no se inicializaban cuando se llamó al vínculo de monitor `onInstanceConfigured`.
- Se ha corregido un problema en el cual los destinos de las cookies no se establecían en la ruta correcta.
- Se ha corregido un problema del cliente con la llamada a.
- Se ha corregido un problema por el cual una codificación de URL no válida en el parámetro `adobe_mc` provocaba que las llamadas a [sendEvent](commands/sendevent/overview.md) fallaran.

## Versión 2.21.1: 18 de julio de 2024

**Correcciones y mejoras**

- Se corrigió un error de compilación al utilizar la biblioteca NPM.

## Versión 2.21.0: 16 de julio de 2024

**Nuevas funciones**

- Se ha agregado compatibilidad con el seguimiento automático de interacción de propuestas.
- Se ha añadido un script de compilación personalizada que proporciona un archivo alloy.js.
- Se ha mejorado la recopilación de clics con Activity Map y la compatibilidad con la agrupación de eventos.

## Versión 2.20.0: 21 de mayo de 2024

**Nuevas funciones**

- Se agregó compatibilidad con [Streaming Media Collection](../web-sdk/commands/configure/streamingmedia.md).

**Correcciones y mejoras**

- Se ha corregido un error que hacía que el fragmento de preocultación ocultara el contenido predeterminado cuando se optaba por el consentimiento.

## Versión 2.19.2: 10 de enero de 2024

**Correcciones y mejoras**

- Se ha corregido un problema por el cual los errores de identidad enmascaraban otros errores y cambiaban los errores de identidad a advertencias.
- Se corrigió un problema en el cual las llamadas de final de página nunca se enviaban cuando había una llamada superior de página con `renderDecisions` establecido en `false`.
- Se corrigió un problema en el cual el SDK web no podía leer identidades entre dominios cuando había varios `adobe_mc` parámetros de cadena de consulta.

## Versión 2.19.1: 10 de noviembre de 2023

**Correcciones y mejoras**

- Se corrigió un problema en el cual la matriz de propuestas devuelta desde `sendEvent` llamadas siempre estaba vacía.

## Versión 2.19.0: 1 de noviembre de 2023

**Nuevas funciones**

- Se ha agregado compatibilidad para procesar mensajes en la aplicación desde Adobe Journey Optimizer.
- Se agregó compatibilidad con [eventos de parte superior e inferior de la página](use-cases/top-bottom-page-events.md).
- Se ha agregado la opción [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) al comando `sendEvent` para controlar la solicitud del ámbito de toda la página y la superficie predeterminada.

**Correcciones y mejoras**

- La personalización combinada muestra eventos juntos al procesar varios tipos de personalización.
- Se corrigió un problema en el cual los nombres de vistas de aplicaciones de una sola página distinguían entre mayúsculas y minúsculas.
- Se ha corregido un problema con los selectores de oferta personalizados DOM de sombra.

## Versión 2.18.0: 31 de julio de 2023

**Nuevas funciones**

- Se agregó compatibilidad con [anulaciones por comando del ID de secuencia de datos](../datastreams/overrides.md).

**Correcciones y mejoras**

- Se ha corregido un problema por el cual los vínculos de salida no se clasificaban debido a que el dominio formaba parte de la consulta.
- `edgeConfigId` está en desuso a favor de `datastreamId` en la configuración del SDK web.

## Versión 2.17.0: 17 de mayo de 2023

**Correcciones y mejoras**

- El SDK web ahora codifica los valores de destino de las cookies del Audience Manager, de forma similar a la [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=es).

## Versión 2.16.0: 25 de abril de 2023

**Nuevas funciones**

- Se agregó compatibilidad con [anulaciones de configuración de secuencia de datos](../datastreams/overrides.md).

## Versión 2.15.0: 30 de marzo de 2023

**Nuevas funciones**

- Se agregó compatibilidad con la llamada de retorno de clic en vínculo [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).
- Se ha agregado compatibilidad con el rastreo de clics de Adobe Journey Optimizer.

**Correcciones y mejoras**

- La colección de vínculos ahora incluye el nombre del vínculo y la región del visitante.
- Se ha eliminado el error de consola para destinos URL fallidos.

## Versión 2.14.0: 25 de enero de 2023

- (Beta) Se ha añadido compatibilidad con superficies y propuestas de Adobe Journey Optimizer.

**Correcciones y mejoras**

- Se ha corregido un problema con las acciones de código personalizado del VEC de Adobe Target en el cual el código se insertaba en una ubicación alternativa a [!DNL at.js].
- Se ha corregido un problema en el cual en algunos casos extremos el encabezado &quot;referente&quot; no se establecía correctamente en las solicitudes al Edge Network.
- Se corrigió un problema en el cual las propiedades de [user agent client hint](/help/web-sdk/use-cases/client-hints.md) se podían establecer en un tipo incorrecto.
- Se corrigió un problema en el cual `placeContext.localTime` no coincidía con el esquema.

## Versión 2.13.1: 13 de octubre de 2022

- Se ha corregido un problema en el cual la migración de visitantes no funcionaba si window.Visitor se definía después de configurar. Esto es especialmente un problema cuando se ejecuta con etiquetas de Adobe.
- Se corrigió un problema en el cual `device.screenWidth` y `device.screenHeight` se rellenaban como cadenas en algunos entornos.

## Versión 2.13.0: 28 de septiembre de 2022

**Nuevas funciones**

- Se agregó compatibilidad con [Página por migración completa de página](home.md#migrating-to-web-sdk). El perfil de Adobe Target ahora se conservará a medida que un visitante se desplace entre las páginas de at.js y del SDK web.
- Se agregó compatibilidad configurable para [sugerencias de cliente de agente de usuario de alta entropía](/help/web-sdk/use-cases/client-hints.md).
- Se agregó compatibilidad con el comando [`applyResponse`](/help/web-sdk/commands/applyresponse.md). Esto habilita la personalización híbrida mediante la [API de Edge Network Server](../server-api/overview.md).
- Los vínculos del modo de control de calidad ahora funcionan en varias páginas.

**Correcciones y mejoras**

- Se ha corregido un problema en el cual las métricas de rastreo de clics de personalización no se actualizaban cuando el seguimiento de vínculos estaba deshabilitado.
- Se han actualizado los comandos para generar un error de validación cuando se especifican opciones desconocidas.
- La propiedad `_experience.decisioning.propositionEventType` ahora se rellena al enviar automáticamente eventos de personalización de visualización e interacción.
- Se agregó la validación del área de nombres duplicada para el comando `getIdentity`.
- Se agregó la validación duplicada del ámbito de decisión para el comando `sendEvent`.

## Versión 2.12.0: 29 de junio de 2022

- Cambie las solicitudes al Edge Network para que use la sugerencia de ubicación de la cookie `cluster` como parte de la dirección URL. Esto garantiza que los usuarios que cambian de ubicación (por ejemplo, a través de una VPN o conduciendo con dispositivos móviles, etc.) a mitad de la sesión tengan el mismo perfil personalizado.
- Consolide las funciones configuradas en la respuesta del comando getLibraryInfo.

## Versión 2.11.0: 13 de junio de 2022

**Nuevas funciones**

- Ahora puede ofrecer experiencias personalizadas con mayor precisión si comparte los ID de visitante entre aplicaciones móviles y contenido de la web móvil, así como entre dominios. Consulte la [documentación dedicada](identity/id-sharing.md) para obtener más información.
- Ahora puede procesar o ejecutar una matriz de propuestas de [!DNL Adobe Target] en aplicaciones de una sola página, sin incrementar las métricas de Analytics. Esto reduce los errores de creación de informes y aumenta la precisión del análisis. Consulte la [documentación dedicada](personalization/rendering-personalization-content.md#applypropositions) para obtener más información.
- Se ha agregado información adicional al comando `getLibraryInfo`, incluidos los comandos disponibles y la configuración final de la instancia.

**Correcciones y mejoras**

- Se ha actualizado la configuración de cookies para utilizar las marcas `sameSite="none"` y `secure` en las páginas [!DNL HTTPS].
- Se corrigió un problema en el cual el contenido personalizado no se aplicaba correctamente al usar el pseudoselector `eq`.
- Se corrigió un problema en el cual `localTimezoneOffset` podría fallar en la validación del Experience Platform.

## Versión 2.10.1: 3 de mayo de 2022

- Se ha corregido un problema en el cual se creaban varios iframes persistentes para sincronizaciones de ID y destinos de segmento.

## Versión 2.10.0: 22 de abril de 2022

- Utilice un iframe persistente para todas las sincronizaciones de ID y destinos de segmento.
- Se corrigió un problema en el cual las propuestas de métricas combinadas se duplicaban en el resultado `sendEvent`.

## Versión 2.9.0: 10 de marzo de 2022

- Se agregó compatibilidad con el seguimiento de [!DNL control (default)] experiencias de Adobe Target.
- Se han optimizado los eventos de cambio de vista para aplicaciones de una sola página. La notificación de visualización ahora se incluye con el evento de cambio de vista cuando se representan experiencias personalizadas.
- Se eliminó la advertencia de la consola cuando no había `eventType` presente.
- Se ha corregido un problema en el cual la propiedad `propositions` solo se devolvía desde un comando `sendEvent` cuando se solicitaban o recuperaban experiencias de la caché. La propiedad `propositions` ahora siempre se definirá como una matriz.
- Se ha corregido un problema en el cual los contenedores ocultos no se mostraban cuando el Edge Network devolvía un error.
- Se ha corregido un problema en el cual los eventos de interacción no se contaban en Adobe Target. Esto se solucionó añadiendo el nombre de la vista al XDM en web.webPageDetails.viewName.
- Corrección de vínculos de documentación dañados en los mensajes de la consola.

## Versión 2.8.0: 19 de enero de 2022

- Compatibilidad con selectores DOM en la sombra para la personalización.
- Se ha cambiado el nombre de tipos de eventos de personalización. (`display` y `click` se convierten en `decisioning.propositionDisplay` y `decisioning.propositionInteract`)
- Se ha corregido un problema por el cual las ofertas de HTML con etiquetas de scripts en línea añadían las etiquetas de scripts dos veces a la página aunque el script solo se ejecutara una vez.

## Versión 2.7.0: 26 de octubre de 2021

- Exponer información adicional del Edge Network en el valor devuelto de `sendEvent`, incluidos `inferences` y `destinations`. El formato de estas propiedades puede cambiar a medida que estas funciones se implementan como parte de una Beta.

## Versión 2.6.4: 7 de septiembre de 2021

- Se corrigió un problema en el cual las acciones de set HTML Adobe Target aplicadas al elemento `head` reemplazaban todo el contenido de `head`. Ahora, las acciones del HTML set aplicadas al elemento `head` se cambian a anexar HTML.

## Versión 2.6.3: 16 de agosto de 2021

- Se corrigió un problema en el cual los objetos no destinados al uso público se exponían a través de la promesa resuelta del comando `configure`.

## Versión 2.6.2: 4 de agosto de 2021

- Se ha corregido un problema en el cual una advertencia sobre la obsolescencia de `result.decisions` (proporcionada por el comando `sendEvent`) se registraba en la consola incluso cuando no se tenía acceso a la propiedad `result.decisions`. No se registrará ninguna advertencia al acceder a la propiedad `result.decisions`, pero la propiedad sigue en desuso.

## Versión 2.6.1: 29 de julio de 2021

- Se ha corregido un problema en el cual al procesar la personalización para una vista de aplicación de una sola página sin contenido de personalización, se producía un error y se rechazaba la promesa devuelta por el comando `sendEvent`.

## Versión 2.6.0: 27 de julio de 2021

- Proporciona más contenido de personalización en la promesa resuelta de `sendEvent`, incluidos tokens de respuesta de Adobe Target. Cuando se ejecuta el comando `sendEvent`, se devuelve una promesa, que finalmente se resuelve con un objeto `result` que contiene información recibida del servidor. Anteriormente, este objeto de resultado incluía una propiedad denominada `decisions`. Esta propiedad de `decisions` se ha dejado de utilizar. Se ha agregado una nueva propiedad, `propositions`. Esta nueva propiedad brinda a los clientes acceso a más contenido de personalización, entre ellos [tokens de respuesta](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Versión 2.5.0: junio de 2021

- Se ha agregado compatibilidad con ofertas de personalización de redireccionamiento.
- Las anchuras y alturas de ventanilla recopiladas automáticamente que sean valores negativos ya no se enviarán al servidor.
- Cuando se cancela un evento devolviendo `false` desde una llamada de retorno `onBeforeEventSend`, ahora se registra un mensaje.
- Se ha corregido un problema en el cual se incluían fragmentos específicos de datos XDM destinados a un solo evento en varios eventos.

## Versión 2.4.0: marzo de 2021

- Ahora, el SDK se puede instalar como [paquete NPM](/help/web-sdk/install/npm.md).
- Se agregó compatibilidad con la opción `out` al [configurar el consentimiento predeterminado](/help/web-sdk/commands/configure/defaultconsent.md), que anula todos los eventos hasta que se reciba el consentimiento (la opción `pending` existente pone en cola los eventos y los envía una vez que se recibe el consentimiento).
- Ahora se puede usar la llamada de retorno [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) para evitar que se envíe un evento.
- Ahora utiliza un grupo de campos de esquema XDM en lugar de `meta.personalization` al enviar eventos sobre el contenido personalizado que se procesa o en el que se hace clic.
- El comando [`getIdentity`](/help/web-sdk/commands/getidentity.md) ahora devuelve el ID de región perimetral junto con la identidad.
- Las advertencias y los errores recibidos del servidor se han mejorado y se gestionan de forma más adecuada.
- Se agregó compatibilidad con el estándar Consentimiento de Adobe 2.0 para el comando [`setConsent`](/help/web-sdk/commands/setconsent.md).
- Cuando se reciben, las preferencias de consentimiento tienen un cifrado hash y se almacenan en el almacenamiento local para una integración optimizada entre CMP, el SDK web de Platform y el Edge Network de Platform. Si está recopilando las preferencias de consentimiento, le recomendamos que llame a `setConsent` en cada carga de página.
- Se han agregado dos [vínculos de supervisión](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` y `onCommandRejected`.
- Corrección de errores: Los eventos de notificación de interacción de Personalization contendrían información duplicada sobre la misma actividad cuando un usuario navegaba a una nueva vista de aplicación de una sola página, volvía a la vista original y hacía clic en un elemento que cumplía los requisitos para la conversión.
- Corrección de errores: Si el primer evento enviado por el SDK tenía `documentUnloading` establecido en `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) se usaría para enviar el evento, lo que da como resultado un error con respecto a una identidad que no se está estableciendo.

## Versión 2.3.0: noviembre de 2020

- Se ha agregado compatibilidad con nonce para permitir políticas de seguridad de contenido más estrictas.
- Se ha agregado compatibilidad con la personalización para aplicaciones de una sola página.
- Se ha mejorado la compatibilidad con otro código de JavaScript en la página que podría estar sobrescribiendo las API `window.console`.
- Corrección de errores: `sendBeacon` no se estaba usando cuando `documentUnloading` se estableció en `true` o cuando se realizaba un seguimiento automático de los clics en los vínculos.
- Corrección de errores: No se rastrearía automáticamente un vínculo si el elemento de anclaje contuviera contenido de HTML.
- Corrección de errores: Algunos errores del explorador que contienen una propiedad de solo lectura `message` no se gestionaron correctamente, lo que dio como resultado que se expusiera un error diferente al cliente.
- Corrección de errores: La ejecución del SDK dentro de un iframe produciría un error si la página del HTML del iframe era de un subdominio diferente a la página del HTML de la ventana principal.

## Versión 2.2.0: octubre de 2020

- Corrección de errores: El objeto Opt-in bloqueaba el SDK web para que no realizara llamadas cuando `idMigrationEnabled` es `true`.
- Corrección de errores: Haga que el SDK web tenga en cuenta las solicitudes que deberían devolver ofertas de personalización para evitar un problema de parpadeo.

## Versión 2.1.0: agosto de 2020

- Quite el comando `syncIdentity` y permita pasar esos identificadores en el comando `sendEvent`.
- Compatibilidad con el estándar de consentimiento IAB 2.0.
- Compatibilidad para pasar ID adicionales en el comando `setConsent`.
- Compatibilidad para anular `datasetId` en el comando `sendEvent`.
- Admitir vínculos de supervisión ([Más información](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- Pase `environment: browser` en los datos de contexto de detalles de implementación.
