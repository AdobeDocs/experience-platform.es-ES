---
solution: Data Collection
audience: user
user-guide-title: Ayuda del SDK web de Adobe Experience Platform
breadcrumb-title: Guía del SDK web
user-guide-description: Interactúe con los servicios de Experience Cloud a través de la red perimetral.
feature: Web SDK
source-git-commit: 5a64beb2f5826bda585111e9ce7f760b939bf9b9
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 33%

---


# SDK web de Adobe Experience Platform {#edge}

* [Información general de Platform Web SDK](home.md)
* Aspectos básicos {#fundamentals}
   * [Casos de uso admitidos](fundamentals/supported-use-cases.md)
   * [Requisitos previos](fundamentals/prerequisite.md)
   * [Instalación del SDK](fundamentals/installing-the-sdk.md)
   * [Configuración del SDK](fundamentals/configuring-the-sdk.md)
   * [Ejecutar comandos](fundamentals/executing-commands.md)
   * [Seguimiento de eventos](fundamentals/tracking-events.md)
   * [Depuración](fundamentals/debugging.md)
   * [Configuración de un CSP](fundamentals/configuring-a-csp.md)
   * [Interactuar con varias propiedades](fundamentals/interacting-with-multiple-properties.md)
   * [User-Agent Client Hints](fundamentals/user-agent-client-hints.md)
* Corrientes de datos {#datastreams}
   * [Información general](./datastreams/overview.md)
   * [Configurar una secuencia de datos](./datastreams/configure.md)
   * [Configurar anulaciones de secuencia de datos](./datastreams/overrides.md)
   * [Preparación de datos para la recopilación de datos](./datastreams/data-prep.md)
   * Enriquecimiento de datos {#data-enrichment}
      * [Datos meteorológicos por el canal del tiempo](./datastreams/data-enrichment/weather.md)
      * [Asignaciones de campos de datos meteorológicos](./datastreams/data-enrichment/weather-reference.md)
* Identidad {#identity}
   * [Información general](identity/overview.md)
   * [ID de dispositivos de origen](identity/first-party-device-ids.md)
   * [Uso compartido de ID de móviles a web y entre dominios](identity/id-sharing.md)
* Recopilación de datos {#data-collection}
   * [Información recopilada automáticamente](data-collection/automatic-information.md)
   * [Seguimiento de vínculos](data-collection/track-links.md)
   * [Recopilación de datos de comercio y productos](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Uso de Adobe Analytics con el SDK web de Platform](data-collection/adobe-analytics/analytics-overview.md)
      * [Asignación de variables de Analytics](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [Variables asignadas automáticamente](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [Envío de datos a Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* Personalización {#personalization}
   * [Procesar contenido personalizado](personalization/rendering-personalization-content.md)
   * [Personalización mediante implementación híbrida](personalization/hybrid-personalization.md)
   * [Administrar parpadeo](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Información general](personalization/adobe-target/target-overview.md)
      * [Implementación de aplicación de una sola página](personalization/adobe-target/spa-implementation.md)
      * [Acceso a tokens de respuesta](personalization/adobe-target/accessing-response-tokens.md)
      * [Uso del ID de terceros de mbox](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Comparación de la biblioteca at.js con el SDK web](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Registro de Analytics for Target (A4T) {#a4t}
         * [Información general ](personalization/adobe-target/analytics-logging/overview.md)
         * [Lado del cliente registro](personalization/adobe-target/analytics-logging/client-side.md)
         * [Registro en el lado del servidor](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Información general](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Información general](personalization/ajo/overview.md)
* Consentimiento {#consent}
   * [Consentimiento de apoyo](consent/supporting-consent.md)
   * Marco de transparencia y consentimiento IAB 2.0 {#iab-tcf}
      * [Información general](consent/iab-tcf/overview.md)
      * [Integración con etiquetas](consent/iab-tcf/with-launch.md)
      * [Integración sin etiquetas](consent/iab-tcf/without-launch.md)
* Extensión de etiqueta de SDK web {#extension}
   * [Extensión del SDK web](extension/web-sdk-extension-configuration.md)
   * [Tipos de eventos](extension/event-types.md)
   * [Tipos de acción](extension/action-types.md)
   * [Tipos de elementos de datos](extension/data-element-types.md)
   * [Acceso al ECID](extension/accessing-the-ecid.md)
   * [Notas de la versión de la extensión Web SDK](extension/web-sdk-ext-release-notes.md)
* [Notas de la versión](release-notes.md)
* [Preguntas frecuentes](web-sdk-faq.md)
* [Recursos](resources.md)
