---
solution: Data Collection
audience: user
user-guide-title: Ayuda del SDK web de Adobe Experience Platform
breadcrumb-title: Guía del SDK web
user-guide-description: Interactúe con los servicios de Experience Cloud a través de la red perimetral.
feature: Web SDK
role: Developer
source-git-commit: bed63cb9be1ffe39a538d1c3f8be9065ffb2ca28
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 23%

---


# SDK web de Adobe Experience Platform {#web-sdk}

* [Información general del SDK web](home.md)
* [Notas de la versión](release-notes.md)
* Instalación de Web SDK {#install}
   * [Información general](install/overview.md)
   * [Instalación de Web SDK mediante la extensión de etiquetas](install/extension.md)
   * [Instalar Web SDK mediante la biblioteca de JavaScript](install/library.md)
   * [Instalación de Web SDK mediante el paquete NPM](install/npm.md)
   * [Cree una compilación personalizada de Web SDK con el paquete NPM](install/create-custom-build.md)
* Comandos {#commands}
   * configurar {#configure}
      * [Información general](commands/configure/overview.md)
      * [autoCollectPropositionInteractions](commands/configure/autocollectpropositioninteractions.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [contexto](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehiddenStyle](commands/configure/prehidingstyle.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [Información general](commands/sendevent/overview.md)
      * [datos](commands/sendevent/data.md)
      * [documentUnloading](commands/sendevent/documentunloading.md)
      * [personalización](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [tipo](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [Configurar anulaciones de secuencia de datos](commands/datastream-overrides.md)
   * [Respuestas de comando](commands/command-responses.md)

* Identidad {#identity}
   * [Información general](identity/overview.md)
   * [ID de dispositivos de origen](identity/first-party-device-ids.md)
   * [Uso compartido de ID de móviles a web y entre dominios](identity/id-sharing.md)

* Personalización {#personalization}
   * [Administrar eventos de visualización](personalization/display-events.md)
   * [Procesar contenido personalizado](personalization/rendering-personalization-content.md)
   * [Personalization mediante implementación híbrida](personalization/hybrid-personalization.md)
   * [Administrar parpadeo](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Información general](personalization/adobe-target/target-overview.md)
      * [Implementación de aplicación de una sola página](personalization/adobe-target/spa-implementation.md)
      * [Acceso a tokens de respuesta](personalization/adobe-target/accessing-response-tokens.md)
      * [Uso del ID de terceros de mbox](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Comparación de la biblioteca at.js con Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Registro {#a4t} de Analytics for Target (A4T)
         * [Información general](personalization/adobe-target/analytics-logging/overview.md)
         * [Registro en el lado del cliente](personalization/adobe-target/analytics-logging/client-side.md)
         * [Registro en el lado del servidor](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Información general](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Información general](personalization/ajo/overview.md)
      * [Implementación de aplicación de una sola página](personalization/ajo/web-spa-implementation.md)
      * [Configuración de la compatibilidad con la mensajería web en la aplicación en Web SDK](personalization/web-in-app-messaging.md)

* Consentimiento {#consent}
   * Marco de transparencia y consentimiento IAB 2.0 {#iab-tcf}
      * [Información general](consent/iab-tcf/overview.md)
      * [Integración con etiquetas](consent/iab-tcf/with-tags.md)
      * [Integración sin etiquetas](consent/iab-tcf/without-tags.md)

* Casos de uso {#use-cases}
   * [Información general](use-cases/overview.md)
   * [Envío de datos a Adobe Analytics mediante Web SDK](use-cases/adobe-analytics.md)
   * [User agent client hints](use-cases/client-hints.md)
   * [Recopilación de datos de comercio](use-cases/collect-commerce-data.md)
   * [Configuración de un CSP](use-cases/configuring-a-csp.md)
   * [Métodos de depuración](use-cases/debugging.md)
   * [Uso de varias instancias de Web SDK](use-cases/multiple-instances.md)
   * [Configuración de eventos de página superior e inferior](use-cases/top-bottom-page-events.md)
* [Enlaces de monitorización](monitoring-hooks.md)
* [Preguntas frecuentes](faq.md)
* [Recursos](resources.md)
