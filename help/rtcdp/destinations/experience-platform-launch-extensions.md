---
keywords: launch extensions;launch extension;launch destinations; platform launch extensions;platform launch extension;platform launch destinations
title: Extensiones de Experience Platform Launch
seo-title: Extensiones de Experience Platform Launch
description: Launch es la función de administración de etiquetas de próxima generación de Adobe. Launch ofrece una alternativa sencilla para implementar y gestionar todas las integraciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes.
seo-description: Launch es la función de administración de etiquetas de próxima generación de Adobe. Launch ofrece una alternativa sencilla para implementar y gestionar todas las integraciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 21%

---


# Extensiones de Adobe Experience Platform Launch {#experience-platform-launch-extensions}

Adobe Experience Platform Launch es la próxima generación de funciones de administración de etiquetas de Adobe. Platform Launch ofrece una alternativa sencilla para implementar y gestionar todas las integraciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes. Platform Launch se ofrece a los clientes de Adobe Experience Cloud como una función de valor añadido incluida.

Para obtener una introducción a las funciones de Experience Platform Launch, consulte los recursos siguientes:
* Adobe Experience Platform Launch [documentation](https://docs.adobe.com/content/help/es-ES/launch/using/overview.html)
* Adobe Experience Platform Launch [quick start videos](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html). Inicio con la [introducción a Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) y al proceso de [publicación](https://helpx.adobe.com/es/analytics/how-to/adobe-launch-publishing-process.html)y, a continuación, pase a los siguientes conceptos.

## Cómo encontrar las extensiones de Launch de plataforma en la interfaz CDP en tiempo real de Adobe {#how-to-find-extensions-in-interface}

Para encontrar las extensiones de Launch de plataforma en la interfaz CDP en tiempo real de Adobe, vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** y seleccione **[!UICONTROL Extensiones]** en el filtro **[!UICONTROL Tipos]** .

![Filtro Extensiones en la interfaz](/help/rtcdp/destinations/assets/extensions-filter.png)

## Cómo funcionan las extensiones de Launch de plataforma {#how-extensions-work}

Las extensiones de Launch de plataforma reenvían datos de evento sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino de reenvío de **Evento** . Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de evento sin procesar. Algunos ejemplos son la extensión [de personalización de](/help/rtcdp/destinations/gainsight-extension.md) Gainsight o [Confirmar voz de la extensión](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Cliente.

**Los destinos de exportación** de perfil/segmento en la plataforma de datos del cliente en tiempo real capturan datos de evento, los combinan con otras fuentes de datos, aplican segmentación y exportan segmentos y perfiles cualificados a los destinos. Algunos ejemplos son el destino [del almacenamiento en la nube](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 o el destino [publicitario de](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Extensiones de Experience Platform Launch en comparación con otros destinos](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Ventajas del uso de extensiones de Launch de plataforma {#extensions-benefits}

Adobe Experience Platform Launch es gratuito para los clientes Experience Cloud existentes. El lanzamiento de plataforma simplifica la implementación de etiquetas en el sitio web mediante extensiones fáciles de usar que puede instalar, configurar, actualizar y eliminar. Platform Launch tiene una pequeña huella en el sitio web y le permite mantener las páginas cargadas rápidamente.

>[!IMPORTANT]
>
>Aunque no puede activar segmentos en extensiones de Launch de plataforma, puede configurar reglas para reenviar sólo datos de evento en determinadas situaciones. Lea más abajo.

Puede crear *reglas* que determinen cuándo reenviar datos de evento a extensiones. Esta potente funcionalidad le permite reenviar datos de evento solo en determinadas situaciones, en lugar de enviar datos de evento en cada interacción. Para obtener más información, consulte las reglas en la documentación [de](https://docs.adobe.com/help/es-ES/launch/using/reference/manage-resources/rules.html)Adobe Experience Platform Launch.

## Ejemplos de casos de uso para extensiones de Launch de plataforma {#extensions-use-cases}

Las extensiones de Launch de plataforma le permiten satisfacer diversos casos de uso de clientes. Algunos ejemplos de casos de uso para usar extensiones de Launch de plataforma son:

* Puede enviar datos de sitios web o aplicaciones nativas a Facebook mediante la extensión de píxeles de Facebook. El píxel de Facebook indica a qué partes del sitio o de la aplicación navegó un visitante, reenvía esa información a Facebook y puede redirigir el visitante a través de Facebook.
* Puede reenviar datos de evento de sus sitios web y aplicaciones a Google Analytics para analizar y tomar decisiones en función de esos datos.
* Puede activar una aplicación de cuadro de chat del lado del cliente en el momento adecuado en función de cómo interactúen los usuarios con las páginas, según las reglas que configure en Inicio de plataforma.


## Categorías de extensión {#extension-categories}

Las extensiones de inicio de plataforma pueden encontrarse bajo las siguientes categorías en Adobe Real-time CDP:

* [Publicidad](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Plataforma de gestión de datos](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinos de mercadotecnia de correo electrónico](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalización](/help/rtcdp/destinations/personalization-destinations.md)
* [Encuestas](/help/rtcdp/destinations/survey-destinations.md)
* [Voz del cliente](/help/rtcdp/destinations/voice-of-customer-destinations.md)
