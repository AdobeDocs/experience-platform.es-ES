---
audience: user
user-guide-title: Guía de destinos
user-guide-description: Active los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
description: Este documento enumera la tabla de contenido de los destinos de Adobe Experience Platform
feature: Destinations
source-git-commit: 09bae0d24eead5f0b6533ba5b89e1fc87c8c71b5
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 11%

---


# Destinos {#destinations}

* [Destinos sobre validación](./home.md)
* [Tipos y categorías de destino](./destination-types.md)
* Tutoriales de API {#api}
   * [Conectarse a destinos de flujo continuo y activar datos mediante la API de servicio de flujo](./api/streaming-destinations.md)
   * [Conectarse a destinos de marketing por correo electrónico y activar datos mediante la API de servicio de flujo](./api/email-marketing.md)
* Guías de la interfaz de usuario {#ui}
   * [Espacio de trabajo de destinos](./ui/destinations-workspace.md)
   * [Crear una nueva conexión de destino](./ui/connect-destination.md)
   * Activar datos de audiencia en destinos{#activate}
      * [Información general de Activation](./ui/activation-overview.md)
      * [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](./ui/activate-segment-streaming-destinations.md)
      * [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](./ui/activate-streaming-profile-destinations.md)
      * [Activar datos de audiencia en destinos de exportación de perfiles en lote](./ui/activate-batch-profile-destinations.md)
   * [Ver detalles de destino](./ui/destination-details-page.md)
   * [Actualizar cuentas de destino](./ui/update-accounts.md)
   * [Editar flujos de activación](./ui/edit-activation.md)
   * [Eliminar destinos](./ui/delete-destinations.md)
   * [Monitorizar flujos de datos](./ui/monitor-dataflows.md)
* Catálogo de destinos {#catalog}
   * [Descripción general del catálogo de destinos](./catalog/overview.md)
   * [ Conexión HTTP (Alpha)](./catalog/http-destination.md)
   * Destinos de Adobe{#adobe}
      * [Información general sobre los destinos de Adobe](./catalog/adobe/overview.md)
      * [Conexión del Marketo Engage (Beta)](./catalog/adobe/marketo-engage.md)
      * [uso compartido de segmentos del Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Destinos publicitarios{#advertising}
      * [Información general sobre los destinos publicitarios](./catalog/advertising/overview.md)
      * [Extensión de Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Extensión de la etiqueta de conversión del anunciante de Awin](./catalog/advertising/awin-conversiontag.md)
      * [Extensión Awin Advertiser Mastertag](./catalog/advertising/awin-mastertag.md)
      * [Extensión de seguimiento de eventos universales (UET) de Bing Ads](./catalog/advertising/bing-ads.md)
      * [Extensión de rama](./catalog/advertising/branch.md)
      * [Extensión DoubleClick Floodlight (Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Extensión de facebook Pixel](./catalog/advertising/facebook-pixel.md)
      * [Extensión Flashtalk OneTag](./catalog/advertising/flashtalking.md)
      * [Conexión de Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Extensión de Google Ads](./catalog/advertising/google-ads-extension.md)
      * [Conexión de Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [Conexión de Google Customer Match](./catalog/advertising/google-customer-match.md)
      * [Conexión de Google Display y Video 360](./catalog/advertising/google-dv360.md)
      * [Extensión de Google Gtag](./catalog/advertising/gtag-advertising.md)
      * [Extensión de la etiqueta linkedIn Insight](./catalog/advertising/linkedin.md)
      * [Conexión de Microsoft Bing](./catalog/advertising/bing.md)
      * [Extensión de seguimiento de conversión de pinterest](./catalog/advertising/pinterest-extension.md)
      * [La conexión con el mostrador de comercio](./catalog/advertising/tradedesk.md)
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
      * [(Beta) Conexión de Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Conexión Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Conexión de Azure Blob](./catalog/cloud-storage/azure-blob.md)
      * [(Beta) Conexión de los centros de eventos de Azure](./catalog/cloud-storage/azure-event-hubs.md)
      * [Conexión SFTP](./catalog/cloud-storage/sftp.md)
      * [LISTA DE PERMITIDOS de direcciones IP](./catalog/cloud-storage/ip-address-allow-list.md)
   * Destinos {#data-management} de la plataforma de gestión de datos
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
      * [Conexión de Marketing Cloud de Salesforce](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * Extensiones de etiquetas {#launch-extensions}
      * [Información general de la extensión de etiquetas](./catalog/launch-extensions/overview.md)
   * Destinos de participación móvil {#mobile-engagement}
      * [Información general sobre los destinos de participación del dispositivo móvil](./catalog/mobile-engagement/overview.md)
      * [(Beta) Conexión de Atributos de Aeronaves](./catalog/mobile-engagement/airship-attributes.md)
      * [(Beta) Conexión de las etiquetas de los buques aéreos](./catalog/mobile-engagement/airship-tags.md)
      * [(Beta) Conexión en formato Braze](./catalog/mobile-engagement/braze.md)
   * Destinos personalizados {#personalization}
      * [Información general sobre los destinos de personalización](./catalog/personalization/overview.md)
      * [Extensión de Adobe Target](./catalog/personalization/adobe-target.md)
      * [Extensión de Adobe Target 2.0](./catalog/personalization/adobe-target-v2.md)
      * [Extensión de Beemray](./catalog/personalization/beemray.md)
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
   * Destinos de Survey {#survey}
      * [Información general sobre los destinos de encuesta](./catalog/survey/overview.md)
      * [Destino de la extensión forestal](./catalog/survey/foresee.md)
      * [Extensión InMoment](./catalog/survey/inmoment.md)
      * [Extensión de comentarios del sitio web de Qualtrics](./catalog/survey/qualtrics.md)
      * [Extensión de los estudios de interceptación de QuestionPro](./catalog/survey/web-intercept-surveys.md)
   * Voz de los destinos de cliente {#voice}
      * [Descripción general de los destinos de la voz del cliente](./catalog/voice/overview.md)
      * [Confirmar extensión de comentarios digitales](./catalog/voice/confirmit-digital-feedback.md)
      * [Extensión de etiquetas de Invoca](./catalog/voice/invoca.md)
      * [Extensión de Medallia](./catalog/voice/medallia.md)
      * [Extensión de la bandeja de entrada de URL de Talk](./catalog/voice/talkurl.md)
* [Preguntas frecuentes](./destinations-faq.md)
* [Notas de la versión de Platform](https://www.adobe.com/go/platform-release-notes-en)
