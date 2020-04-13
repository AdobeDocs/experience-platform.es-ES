---
title: Extensiones de Experience Platform Launch
seo-title: Extensiones de Experience Platform Launch
description: Launch es la función de administración de etiquetas de próxima generación de Adobe. Launch ofrece a los clientes una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente.
seo-description: Launch es la función de administración de etiquetas de próxima generación de Adobe. Launch ofrece a los clientes una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch es la función de administración de etiquetas de próxima generación de Adobe. Launch ofrece a los clientes una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Launch se ofrece a los clientes de Adobe Experience Cloud como una función de valor añadido incluida.

Para obtener una introducción a las funciones de Experience Platform Launch, consulte los recursos siguientes:
* [Documentación del Experience Platform Launch](https://docs.adobe.com/content/help/es-ES/launch/using/overview.html)
* Vídeos [de inicio](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html)rápido Experience Platform Launch. Inicio con [Introducción al proceso de Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) y [publicación](https://helpx.adobe.com/es/analytics/how-to/adobe-launch-publishing-process.html)y, a continuación, pase a los siguientes conceptos.

## Cómo funcionan las extensiones de lanzamiento

Las extensiones de inicio reenvían datos de evento sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino de reenvío de **Evento** . Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de evento sin procesar. Algunos ejemplos son la extensión [de personalización de](/help/rtcdp/destinations/gainsight-extension.md) Gainsight o [Confirmar voz de la extensión](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Cliente.

**Los destinos de exportación** de Perfiles y segmentos en la plataforma de datos del cliente de Adobe en tiempo real capturan datos de evento, los combinan con otras fuentes de datos, aplican segmentación y exportan segmentos y perfiles cualificados a los destinos. Algunos ejemplos son el destino [de almacenamiento en la nube](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 o el destino [publicitario de](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Extensiones de Experience Platform Launch en comparación con otros destinos](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Ventajas de utilizar extensiones de Launch

El Experience Platform Launch es gratuito para los clientes existentes de Experience Cloud. Launch simplifica la implementación de etiquetas en el sitio web mediante extensiones fáciles de usar que puede instalar, configurar, actualizar y eliminar. Launch tiene una pequeña huella en el sitio web y le permite mantener las páginas cargadas rápidamente.

>[!IMPORTANT]
>
>Aunque no puede activar segmentos en extensiones de Launch, puede configurar reglas para reenviar sólo datos de evento en determinadas situaciones. Lea más abajo.

Puede crear *reglas* que determinen cuándo reenviar datos de evento a extensiones. Esta potente funcionalidad le permite reenviar datos de evento solo en determinadas situaciones, en lugar de enviar datos de evento en cada interacción. Para obtener más información, consulte acerca de las reglas en la documentación [de](https://docs.adobe.com/help/es-ES/launch/using/reference/manage-resources/rules.html)lanzamiento.

## Ejemplos de casos de uso para extensiones de Launch

Las extensiones de inicio le permiten satisfacer diversos casos de uso de clientes. Algunos ejemplos de casos de uso para usar extensiones de Launch son:

* Puede enviar datos de sitios web o aplicaciones nativas a Facebook mediante la extensión de píxeles de Facebook. El píxel de Facebook indica a qué partes del sitio o de la aplicación navegó un visitante, reenvía esa información a Facebook y puede redirigir el visitante a través de Facebook.
* Puede reenviar datos de evento de sus sitios web y aplicaciones a Google Analytics para analizar y tomar decisiones en función de esos datos.
* Puede activar una aplicación de cuadro de chat del lado del cliente en el momento adecuado en función de cómo interactúen los usuarios con sus páginas, según las reglas que configure en Launch.


## categorías de extensión

Las extensiones de inicio pueden encontrarse bajo las siguientes categorías en Adobe Real-time CDP:

* [Publicidad](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Plataforma de Gestión de datos](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinos de mercadotecnia de correo electrónico](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalización](/help/rtcdp/destinations/personalization-destinations.md)
* [Encuestas](/help/rtcdp/destinations/survey-destinations.md)
* [Voz del cliente](/help/rtcdp/destinations/voice-of-customer-destinations.md)
