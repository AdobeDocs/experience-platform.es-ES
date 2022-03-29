---
audience: user
user-guide-title: Guía de destinos
user-guide-description: Active los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
description: Este documento enumera la tabla de contenido de los destinos de Adobe Experience Platform
feature: Destinations
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 9%

---


# Destinos {#destinations}

* [Destinos sobre validación](./home.md)
* [Tipos y categorías de destino](./destination-types.md)
* Tutoriales de API {#api}
   * [Conectarse a destinos de flujo continuo y activar datos mediante la API de servicio de flujo](./api/streaming-destinations.md)
   * [Conéctese a destinos de almacenamiento en la nube por lotes y marketing por correo electrónico y active los datos mediante la API de servicio de flujo](./api/connect-activate-batch-destinations.md)
   * [(Beta) Activar segmentos de audiencia en destinos por lotes mediante la API de activación ad hoc](./api/ad-hoc-activation-api.md)
   * [Actualizar flujos de datos de destino](./api/update-destination-dataflows.md)
   * [Eliminar cuentas de destino](./api/delete-destination-account.md)
   * [Eliminar flujos de datos de destino](./api/delete-destination-dataflow.md)
* Guías de la interfaz de usuario {#ui}
   * [Espacio de trabajo de destinos](./ui/destinations-workspace.md)
   * [Crear una nueva conexión de destino](./ui/connect-destination.md)
   * Activar datos de audiencia en destinos{#activate}
      * [Información general de Activation](./ui/activation-overview.md)
      * [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](./ui/activate-segment-streaming-destinations.md)
      * [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](./ui/activate-streaming-profile-destinations.md)
      * [Activar datos de audiencia en destinos de exportación de perfiles en lote](./ui/activate-batch-profile-destinations.md)
      * [Activar datos de audiencia en destinos de solicitud de perfil](./ui/activate-profile-request-destinations.md)
      * [Configurar destinos de personalización para la personalización de la misma página y de la página siguiente](./ui/configure-personalization-destinations.md)
   * [Ver detalles de destino](./ui/destination-details-page.md)
   * [Update destination accounts](./ui/update-accounts.md)
   * [Eliminar cuentas de destino](./ui/delete-destination-account.md)
   * [Editar flujos de datos de activación](./ui/edit-activation.md)
   * [Eliminar destinos](./ui/delete-destinations.md)
   * [Monitorizar flujos de datos](./ui/monitor-dataflows.md)
* Catálogo de destinos {#catalog}
   * [Descripción general del catálogo de destinos](./catalog/overview.md)
   * Adobe destinations{#adobe}
      * [Adobe destinations overview](./catalog/adobe/overview.md)
      * [conexión del Marketo Engage](./catalog/adobe/marketo-engage.md)
      * [uso compartido de segmentos del Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Destinos publicitarios{#advertising}
      * [Información general sobre los destinos publicitarios](./catalog/advertising/overview.md)
      * [Extensión de Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Extensión de la etiqueta de conversión del anunciante de Awin](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag extension](./catalog/advertising/awin-mastertag.md)
      * [Extensión de seguimiento de eventos universales (UET) de Bing Ads](./catalog/advertising/bing-ads.md)
      * [Extensión de rama](./catalog/advertising/branch.md)
      * [Extensión DoubleClick Floodlight (Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Extensión de facebook Pixel](./catalog/advertising/facebook-pixel.md)
      * [Extensión Flashtalk OneTag](./catalog/advertising/flashtalking.md)
      * [Conexión de Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Google Ads extension](./catalog/advertising/google-ads-extension.md)
      * [Conexión de Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [Conexión Google Customer Match](./catalog/advertising/google-customer-match.md)
      * [Google Display &amp; Video 360 connection](./catalog/advertising/google-dv360.md)
      * [Extensión de etiqueta de Google](./catalog/advertising/gtag-advertising.md)
      * [Extensión de la etiqueta linkedIn Insight](./catalog/advertising/linkedin.md)
      * [Conexión de Microsoft Bing](./catalog/advertising/bing.md)
      * [Extensión de seguimiento de conversión de pinterest](./catalog/advertising/pinterest-extension.md)
      * [Pinterest Customer List connection](./catalog/advertising/pinterest.md)
      * [La conexión con el mostrador de comercio](./catalog/advertising/tradedesk.md)
      * [Extensión de la etiqueta del sitio web universal de twitter](./catalog/advertising/twitter-uwt.md)
      * [Conexión de Yahoo/Verizon DataX](./catalog/advertising/datax.md)
   * Destinos de Analytics {#analytics}
      * [Información general sobre los destinos de Analytics](./catalog/analytics/overview.md)
      * [Extensión de seguimiento de sitios web de Adobe](./catalog/analytics/adform.md)
      * [Extensión de Adobe Analytics](./catalog/analytics/adobe-analytics.md)
      * [Extensión de Adobe Media Analytics for Audio and Video](./catalog/analytics/adobe-video-analytics.md)
      * [Extensión de la tabla de clics](./catalog/analytics/clicktale.md)
      * [Contentsquare extension](./catalog/analytics/contentsquare.md)
      * [Extensión Decibel](./catalog/analytics/decibel.md)
      * [Extensión de Demandbase](./catalog/analytics/demandbase.md)
      * [Extensión DialogTech](./catalog/analytics/dialogtech.md)
      * [Extensión de Google Global Site Tag](./catalog/analytics/gtag-analytics.md)
      * [Extensión de Google Universal Analytics](./catalog/analytics/google-universal-analytics.md)
      * [Extensión de JW Player Analytics (Beta)](./catalog/analytics/jw-player-analytics.md)
      * [Extensión de Nielsen BSDK](./catalog/analytics/nielsen-bsdk.md)
      * [Extensión del controlador IMA de Nielsen](./catalog/analytics/nielsen-ima.md)
      * [Extensión del controlador de reproductor de VideoJS de Nielsen](./catalog/analytics/nielsen-videojs.md)
      * [Extensión de Analytics de Parse.ly](./catalog/analytics/parsely.md)
      * [Extensión de métrica cuántica](./catalog/analytics/quantum-metric.md)
      * [Extensión SessionCam](./catalog/analytics/sessioncam.md)
      * [Extensión TMMData](./catalog/analytics/tmmdata.md)
      * [Extensión de seguimiento de conversión de contexto](./catalog/analytics/yext.md)
   * Cloud storage destinations {#cloud-storage}
      * [Cloud Storage destinations overview](./catalog/cloud-storage/overview.md)
      * [(Beta) Conexión de Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Conexión Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Conexión de Azure Blob](./catalog/cloud-storage/azure-blob.md)
      * [(Beta) Azure Event Hubs connection](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP connection](./catalog/cloud-storage/sftp.md)
      * [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](./catalog/cloud-storage/ip-address-allow-list.md)
   * Data Management Platform destinations {#data-management}
      * [Información general sobre los destinos de la plataforma de gestión de datos (DMP)](./catalog/data-management/overview.md)
      * [Audience Manager DIL extension](./catalog/data-management/aam-dil-extension.md)
   * Destinos de correo electrónico {#email}
      * [Extensión Bizible](./catalog/email/bizible.md)
      * [Marketo extension](./catalog/email/marketo.md)
      * [Extensión de Marketo Munchkin](./catalog/email/marketo-munchkin.md)
      * [PebblePost extension](./catalog/email/pebblepost.md)
   * Email marketing destinations {#email-marketing}
      * [Información general sobre los destinos de marketing por correo electrónico](./catalog/email-marketing/overview.md)
      * [Conexión Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [Conexión oracle Eloqua](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle Responsys connection](./catalog/email-marketing/oracle-responsys.md)
      * [Salesforce Marketing Cloud connection](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * Extensiones de etiquetas {#launch-extensions}
      * [Tag extension overview](./catalog/launch-extensions/overview.md)
   * Destinos de participación de Mobile {#mobile-engagement}
      * [Información general sobre los destinos de participación del dispositivo móvil](./catalog/mobile-engagement/overview.md)
      * [Conexión de atributos de aeronave](./catalog/mobile-engagement/airship-attributes.md)
      * [Airship Tags connection](./catalog/mobile-engagement/airship-tags.md)
      * [Conexión con el Brazo](./catalog/mobile-engagement/braze.md)
   * Destinos personalizados {#personalization}
      * [Información general sobre los destinos de personalización](./catalog/personalization/overview.md)
      * [Adobe Target connection](./catalog/personalization/adobe-target-connection.md)
      * [Extensión de Adobe Target](./catalog/personalization/adobe-target.md)
      * [Extensión de Adobe Target 2.0](./catalog/personalization/adobe-target-v2.md)
      * [Beemray extension](./catalog/personalization/beemray.md)
      * [Conexión personalizada personalizada](./catalog/personalization/custom-personalization.md)
      * [Extensión de D&amp;B Visitor Intelligence](./catalog/personalization/dnb.md)
      * [Extensión de Experience Cloud ID Service](./catalog/personalization/adobe-ecid.md)
      * [Extensión de Gainsight](./catalog/personalization/gainsight.md)
      * [Extensión KickFire](./catalog/personalization/kickfire.md)
      * [Extensión de personalización web de Marketo](./catalog/personalization/marketo-web-personalization.md)
   * Destinos sociales{#social}
      * [Información general sobre destinos sociales](./catalog/social/overview.md)
      * [Extensión de Adobe Livefyre](./catalog/social/adobe-livefyre.md)
      * [Conexión facebook](./catalog/social/facebook.md)
      * [Conexión de Audiencias coincidentes de linkedIn](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] connection](./catalog/social/twitter.md)
   * Destinos de transmisión {#streaming}
      * [ Conexión de API HTTP (Beta)](./catalog/streaming/http-destination.md)
      * [LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo](./catalog/streaming/ip-address-allow-list.md)
   * Destinos de Survey {#survey}
      * [Información general sobre los destinos de encuesta](./catalog/survey/overview.md)
      * [Destino de la extensión forestal](./catalog/survey/foresee.md)
      * [Extensión InMoment](./catalog/survey/inmoment.md)
      * [Extensión de comentarios del sitio web de Qualtrics](./catalog/survey/qualtrics.md)
      * [Extensión de los estudios de interceptación de QuestionPro](./catalog/survey/web-intercept-surveys.md)
   * Voz de los destinos del cliente {#voice}
      * [Descripción general de los destinos de la voz del cliente](./catalog/voice/overview.md)
      * [Confirmar extensión de comentarios digitales](./catalog/voice/confirmit-digital-feedback.md)
      * [Extensión de etiquetas de Invoca](./catalog/voice/invoca.md)
      * [Medallia extension](./catalog/voice/medallia.md)
      * [Talk URL Inbox extension](./catalog/voice/talkurl.md)
* SDK de destino {#destination-sdk}
   * [Información general](./destination-sdk/overview.md)
   * [Integration prerequisites](./destination-sdk/integration-prerequisites.md)
   * [Primeros pasos](./destination-sdk/getting-started.md)
   * Destination SDK functionality {#functionality}
      * [Opciones de Configuration](./destination-sdk/configuration-options.md)
      * [Configuración de destino de transmisión](./destination-sdk/destination-configuration.md)
      * [(Beta) Configuración de destino basada en archivos](./destination-sdk/file-based-destination-configuration.md)
      * [Especificaciones del servidor y la plantilla de los destinos de transmisión](./destination-sdk/server-and-template-configuration.md)
      * [(Beta) Especificaciones del servidor y los archivos de destinos basados en archivos](./destination-sdk/server-and-file-configuration.md)
      * [Formato del mensaje](./destination-sdk/message-format.md)
      * [Gestión de metadatos de audiencia](./destination-sdk/audience-metadata-management.md)
      * Autenticación {#authentication}
         * [Configuración de autenticación](./destination-sdk/authentication-configuration.md)
         * [Autenticación OAuth 2](./destination-sdk/oauth2-authentication.md)
      * Developer tools {#developer-tools}
         * [Creación y prueba de una plantilla de transformación de mensaje](./destination-sdk/create-template.md)
         * [Probar la configuración de destino](./destination-sdk/test-destination.md)
   * Operaciones de API {#api}
      * [Referencia de la API del Destination SDK (creación de destino)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [Destinations endpoint API operations](./destination-sdk/destination-configuration-api.md)
      * [Operaciones de API de extremo del servidor de destino](./destination-sdk/destination-server-api.md)
      * [Operaciones de API de extremo de metadatos de audiencia](./destination-sdk/audience-metadata-api.md)
      * [Operaciones de API de extremo de credenciales](./destination-sdk/credentials-configuration-api.md)
      * [Publicar operaciones de API de extremo](./destination-sdk/destination-publish-api.md)
      * Referencia de herramientas para desarrolladores {#developer-tools-reference}
         * [Get sample template API operations](./destination-sdk/sample-template-api.md)
         * [Render template API operations](./destination-sdk/render-template-api.md)
         * [Destination testing API operations](./destination-sdk/destination-testing-api.md)
         * [Ejemplos de operaciones de API de generación de perfiles](./destination-sdk/sample-profile-generation-api.md)
   * Guías {#guides}
      * [Usar Destination SDK para configurar un destino de flujo continuo](./destination-sdk/configure-destination-instructions.md)
      * [(Beta) Use Destination SDK to configure a file-based destination](./destination-sdk/configure-file-based-destination-instructions.md)
      * [Enviar para revisión un destino creado en Destination SDK](./destination-sdk/submit-destination.md)
   * Document your destination {#document-destination}
      * [Documentar el destino en Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Use the GitHub web interface to create a destination documentation page](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Utilice un editor de texto en el entorno local para crear una página de documentación de destino](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Plantilla de autoservicio de documentación](./destination-sdk/docs-framework/self-service-template.md)
* [Preguntas frecuentes](./destinations-faq.md)
* [Notas de la versión de Platform](https://www.adobe.com/go/platform-release-notes-en)
