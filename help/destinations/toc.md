---
audience: user
user-guide-title: Guía de destinos
user-guide-description: Active los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
description: Este documento enumera la tabla de contenido de los destinos de Adobe Experience Platform
feature: Destinations
source-git-commit: a8faa3a146669e206b9aa129f5541a7511c1854a
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 7%

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
      * [(Beta) Exportar archivos bajo demanda a destinos por lotes utilizando la interfaz de usuario del Experience Platform](./ui/export-file-now.md)
   * [Ver detalles de destino](./ui/destination-details-page.md)
   * [Actualizar cuentas de destino](./ui/update-accounts.md)
   * [Eliminar cuentas de destino](./ui/delete-destination-account.md)
   * [Editar flujos de datos de activación](./ui/edit-activation.md)
   * [Eliminar destinos](./ui/delete-destinations.md)
   * [Monitorizar flujos de datos](./ui/monitor-dataflows.md)
   * [Suscripción a alertas de destino en contexto](ui/alerts.md)
* Catálogo de destinos {#catalog}
   * [Descripción general del catálogo de destinos](./catalog/overview.md)
   * Destinos de Adobe{#adobe}
      * [Información general sobre los destinos de Adobe](./catalog/adobe/overview.md)
      * [conexión del Marketo Engage](./catalog/adobe/marketo-engage.md)
      * [uso compartido de segmentos del Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Destinos publicitarios{#advertising}
      * [Información general sobre los destinos publicitarios](./catalog/advertising/overview.md)
      * [Conexión Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Extensión de Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Extensión de la etiqueta de conversión del anunciante de Awin](./catalog/advertising/awin-conversiontag.md)
      * [Extensión Awin Advertiser Mastertag](./catalog/advertising/awin-mastertag.md)
      * [Extensión de seguimiento de eventos universales (UET) de Bing Ads](./catalog/advertising/bing-ads.md)
      * [Extensión de rama](./catalog/advertising/branch.md)
      * [(Beta) Conexión con Criteo](./catalog/advertising/criteo.md)
      * [Extensión DoubleClick Floodlight (Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Extensión de facebook Pixel](./catalog/advertising/facebook-pixel.md)
      * [Extensión Flashtalk OneTag](./catalog/advertising/flashtalking.md)
      * [Conexión de Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Extensión de Google Ads](./catalog/advertising/google-ads-extension.md)
      * [Conexión de Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [(Beta) Conexión con Google Ad Manager 360](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Conexión Google Customer Match](./catalog/advertising/google-customer-match.md)
      * [Conexión de pantalla y vídeo de Google 360](./catalog/advertising/google-dv360.md)
      * [Extensión de etiqueta de Google](./catalog/advertising/gtag-advertising.md)
      * [Extensión de la etiqueta linkedIn Insight](./catalog/advertising/linkedin.md)
      * [Conexión de Microsoft Bing](./catalog/advertising/bing.md)
      * [Extensión de seguimiento de conversión de pinterest](./catalog/advertising/pinterest-extension.md)
      * [Conexión de lista de clientes de pinterest](./catalog/advertising/pinterest.md)
      * [(Beta) Conexión de Snapchat Ads](./catalog/advertising/snap-inc.md)
      * [La conexión con el mostrador de comercio](./catalog/advertising/tradedesk.md)
      * [La conexión con el servicio de asistencia al cliente](./catalog/advertising/tradedesk-emails.md)
      * [Extensión de la etiqueta del sitio web universal de twitter](./catalog/advertising/twitter-uwt.md)
      * [Conexión de Yahoo/Verizon DataX](./catalog/advertising/datax.md)
   * Destinos de Analytics {#analytics}
      * [Información general sobre los destinos de Analytics](./catalog/analytics/overview.md)
      * [Extensión de seguimiento de sitios web de Adobe](./catalog/analytics/adform.md)
      * [Extensión de Adobe Analytics](./catalog/analytics/adobe-analytics.md)
      * [Extensión de Adobe Media Analytics for Audio and Video](./catalog/analytics/adobe-video-analytics.md)
      * [Extensión de la tabla de clics](./catalog/analytics/clicktale.md)
      * [Extensión Contentsquare](./catalog/analytics/contentsquare.md)
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
   * Destinos de almacenamiento en la nube {#cloud-storage}
      * [Resumen de destinos de Cloud Storage](./catalog/cloud-storage/overview.md)
      * [Conexión de Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Conexión Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Conexión de Azure Blob](./catalog/cloud-storage/azure-blob.md)
      * [Conexión de los centros de eventos de Azure](./catalog/cloud-storage/azure-event-hubs.md)
      * [Conexión SFTP](./catalog/cloud-storage/sftp.md)
      * [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](./catalog/cloud-storage/ip-address-allow-list.md)
   * Destinos de administración de la relación con los clientes (CRM) {#crm-destinations}
      * [Conexión de Salesforce CRM](./catalog/crm/salesforce.md)
   * Destinos de la plataforma de gestión de datos {#data-management}
      * [Información general sobre los destinos de la plataforma de gestión de datos (DMP)](./catalog/data-management/overview.md)
      * [extensión del DIL del Audience Manager](./catalog/data-management/aam-dil-extension.md)
   * Destinos de correo electrónico {#email}
      * [Extensión Bizible](./catalog/email/bizible.md)
      * [Extensión de Marketo](./catalog/email/marketo.md)
      * [Extensión de Marketo Munchkin](./catalog/email/marketo-munchkin.md)
      * [Extensión PebblePost](./catalog/email/pebblepost.md)
   * Destinos de marketing por correo electrónico {#email-marketing}
      * [Información general sobre los destinos de marketing por correo electrónico](./catalog/email-marketing/overview.md)
      * [Conexión Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [Conexión oracle Eloqua](./catalog/email-marketing/oracle-eloqua.md)
      * [Conexión de Responsys de oracle](./catalog/email-marketing/oracle-responsys.md)
      * [(API) Conexión de Marketing Cloud de Salesforce](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [(Archivos) Conexión de Marketing Cloud de Salesforce](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [Conexión SendGrid](./catalog/email-marketing/sendgrid.md)
   * Extensiones de etiquetas {#launch-extensions}
      * [Información general de la extensión de etiquetas](./catalog/launch-extensions/overview.md)
   * Destinos de participación móvil {#mobile-engagement}
      * [Información general sobre los destinos de participación del dispositivo móvil](./catalog/mobile-engagement/overview.md)
      * [Conexión de atributos de aeronave](./catalog/mobile-engagement/airship-attributes.md)
      * [Conexión de etiquetas de la aeronave](./catalog/mobile-engagement/airship-tags.md)
      * [Conexión con el Brazo](./catalog/mobile-engagement/braze.md)
   * Destinos personalizados {#personalization}
      * [Información general sobre los destinos de personalización](./catalog/personalization/overview.md)
      * [Conexión Adobe Target](./catalog/personalization/adobe-target-connection.md)
      * [Extensión de Adobe Target](./catalog/personalization/adobe-target.md)
      * [Extensión de Adobe Target 2.0](./catalog/personalization/adobe-target-v2.md)
      * [Extensión de Beemray](./catalog/personalization/beemray.md)
      * [Conexión personalizada personalizada](./catalog/personalization/custom-personalization.md)
      * [Extensión de D&amp;B Visitor Intelligence](./catalog/personalization/dnb.md)
      * [Extensión de Experience Cloud ID Service](./catalog/personalization/adobe-ecid.md)
      * [Extensión de Gainsight](./catalog/personalization/gainsight.md)
      * [Extensión KickFire](./catalog/personalization/kickfire.md)
      * [Extensión de personalización web de Marketo](./catalog/personalization/marketo-web-personalization.md)
      * [Conexión de centro de decisión de clientes pega](./catalog/personalization/pega.md)
   * Destinos sociales{#social}
      * [Información general sobre destinos sociales](./catalog/social/overview.md)
      * [Extensión de Adobe Livefyre](./catalog/social/adobe-livefyre.md)
      * [Conexión facebook](./catalog/social/facebook.md)
      * [Conexión de Audiencias coincidentes de linkedIn](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] connection](./catalog/social/twitter.md)
   * Destinos de transmisión {#streaming}
      * [Conexión de API HTTP](./catalog/streaming/http-destination.md)
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
      * [Conexión con Medallia](./catalog/voice/medallia-connector.md)
      * [Extensión de Medallia](./catalog/voice/medallia.md)
      * [Extensión de la bandeja de entrada de URL de Talk](./catalog/voice/talkurl.md)
* SDK de destino {#destination-sdk}
   * [Información general](./destination-sdk/overview.md)
   * [Requisitos previos de integración](./destination-sdk/integration-prerequisites.md)
   * [Primeros pasos](./destination-sdk/getting-started.md)
   * funcionalidad de Destination SDK {#functionality}
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
      * Herramientas para desarrolladores {#developer-tools}
         * [Creación y prueba de una plantilla de transformación de mensaje](./destination-sdk/create-template.md)
         * [Probar la configuración de destino](./destination-sdk/test-destination.md)
   * Operaciones de API {#api}
      * [Referencia de la API del Destination SDK (creación de destino)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [Operaciones de API de extremo de destinos](./destination-sdk/destination-configuration-api.md)
      * [Operaciones de API de extremo del servidor de destino](./destination-sdk/destination-server-api.md)
      * [Operaciones de API de extremo de metadatos de audiencia](./destination-sdk/audience-metadata-api.md)
      * [Operaciones de API de extremo de credenciales](./destination-sdk/credentials-configuration-api.md)
      * [Publicar operaciones de API de extremo](./destination-sdk/destination-publish-api.md)
      * Referencia de herramientas para desarrolladores {#developer-tools-reference}
         * API de prueba de destino de transmisión {#streaming-destination-testing-api}
            * [Obtener operaciones de API de plantilla de ejemplo](./destination-sdk/sample-template-api.md)
            * [Operaciones de API de plantilla de procesamiento](./destination-sdk/render-template-api.md)
            * [Operaciones de API de prueba de destino](./destination-sdk/destination-testing-api.md)
            * [Ejemplos de operaciones de API de generación de perfiles](./destination-sdk/sample-profile-generation-api.md)
         * API de prueba de destino basada en archivos {#file-based-destination-testing-api}
            * [Resumen de la API de prueba de destino basada en archivos](./destination-sdk/file-based-destination-testing-overview.md)
            * [Generación de perfiles de muestra basados en un esquema de origen](./destination-sdk/file-based-sample-profile-generation-api.md)
            * [Pruebe el destino basado en archivos con perfiles de ejemplo](./destination-sdk/file-based-destination-testing-api.md)
            * [Ver resultados de activación detallados](./destination-sdk/file-based-destination-results-api.md)
            * [Validación de campos de cliente con plantilla](./destination-sdk/file-based-render-template-api.md)
   * Guías {#guides}
      * [Usar Destination SDK para configurar un destino de flujo continuo](./destination-sdk/configure-destination-instructions.md)
      * [(Beta) Usar el Destination SDK para configurar un destino basado en archivos](./destination-sdk/configure-file-based-destination-instructions.md)
      * [Enviar para revisión un destino creado en Destination SDK](./destination-sdk/submit-destination.md)
   * Referencia {#reference}
      * [Política de limitación de velocidad y reintentos para destinos de flujo continuo](./destination-sdk/rate-limiting-retry-policy.md)
      * [Funciones de transformación admitidas](./destination-sdk/supported-functions.md)
   * Documentar el destino {#document-destination}
      * [Documentar el destino en Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Utilice la interfaz web de GitHub para crear una página de documentación de destino](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Utilice un editor de texto en el entorno local para crear una página de documentación de destino](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Plantilla de autoservicio de documentación](./destination-sdk/docs-framework/self-service-template.md)
      * [Prácticas recomendadas sobre la creación](./destination-sdk/docs-framework/authoring-best-practices.md)
* [Preguntas frecuentes](./destinations-faq.md)
* [Notas de la versión de Platform](https://www.adobe.com/go/platform-release-notes-en)
