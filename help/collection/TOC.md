---
audience: user
solution: Data Collection
user-guide-title: Recopilación de datos
breadcrumb-title: Recopilación de datos
user-guide-description: Obtenga información sobre cómo enviar datos a Adobe Experience Platform.
feature: Data Collection
role: Developer
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 30%

---


# Recopilación de datos {#collection}

+ [Información general](home.md)
+ [Permisos](permissions.md)
+ BrightScript {#brightscript}
   + [Información general de BrightScript](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [Información general sobre Web SDK JavaScript](js/js-overview.md)
   + [Notas de la versión](js/release-notes.md)
   + Instalación {#install}
      + [Resumen de instalación](js/install/overview.md)
      + [Biblioteca](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [Compilación personalizada](js/install/create-custom-build.md)
   + Comandos {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + configurar {#configure}
         + [Información general](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [contexto](js/commands/configure/context.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [prehiddenStyle](js/commands/configure/prehidingstyle.md)
         + [pushNotifications](js/commands/configure/pushnotifications.md)
         + [streamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [Información general](js/commands/sendevent/overview.md)
         + [datos](js/commands/sendevent/data.md)
         + [documentUnloading](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [personalización](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [Respuestas de comando](js/commands/command-responses.md)
   + [Enlaces de monitorización](js/monitoring-hooks.md)
   + [Preguntas frecuentes](js/faq.md)
+ Etiquetas de JavaScript del lado del cliente {#tags}
   + [Información general](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [compañía](tags/company.md)
   + [_container](tags/container.md)
   + [cookie](tags/cookie.md)
   + [entorno](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [_monitores](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [track](tags/track.md)
+ Casos de uso {#use-cases}
   + [Información general](use-cases/overview.md)
   + [Client hints](use-cases/client-hints.md)
   + [Estado del cliente](use-cases/client-state.md)
   + [Recopilación de datos de comercio](use-cases/collect-commerce-data.md)
   + [Configuración de un CSP](use-cases/configuring-a-csp.md)
   + [Depuración](use-cases/debugging.md)
   + [Deduplicación de eventos](use-cases/event-duplication.md)
   + Identidad {#identity}
      + [Información general](use-cases/identity/id-overview.md)
      + [ID de dispositivos propios](use-cases/identity/first-party-device-ids.md)
      + [Uso compartido de ID](use-cases/identity/id-sharing.md)
   + [Varias instancias de SDK](use-cases/multiple-instances.md)
   + Personalización {#personalization}
      + [Información general](use-cases/personalization/pers-overview.md)
      + [Mostrar eventos](use-cases/personalization/display-events.md)
      + [Administrar parpadeo](use-cases/personalization/manage-flicker.md)
      + [Representación de contenido personalizado](use-cases/personalization/rendering-personalization-content.md)
      + [Eventos de página superior e inferior](use-cases/personalization/top-bottom-page-events.md)
