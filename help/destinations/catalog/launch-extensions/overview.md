---
keywords: extensiones de etiquetas;extensión de etiquetas;destinos de launch; extensiones de etiquetas de platform;extensión de etiquetas de platform;destinos de platform launch
title: Extensiones de etiquetas en Adobe Experience Platform
description: Adobe Experience Platform proporciona la siguiente generación de funcionalidades de administración de etiquetas desde el Adobe. Platform le ofrece una alternativa sencilla para implementar y gestionar todas las integraciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Extensiones de etiquetas en Adobe Experience Platform

Adobe Experience Platform proporciona la siguiente generación de funcionalidades de administración de etiquetas desde el Adobe. Platform le ofrece una alternativa sencilla para implementar y gestionar todas las integraciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor.

Para ver una introducción a las etiquetas, consulte los recursos siguientes:

- [Información general sobre etiquetas](../../../tags/home.md)
- [Guía de inicio rápido](../../../tags/quick-start/quick-start.md)

## Cómo encontrar extensiones de etiquetas en la interfaz de Platform {#how-to-find-extensions-in-interface}

Para buscar las extensiones en la interfaz de Platform, vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** y seleccione **[!UICONTROL Extensiones]** en el **[!UICONTROL Tipos]** filtro.

![Filtro Extensiones en la interfaz](../../assets/catalog/launch-extensions/filter.png)

## Funcionamiento de las extensiones de etiquetas {#how-extensions-work}

A [extensión de etiqueta](../../../tags/home.md#extensions) es un paquete de código que mejora la funcionalidad de un sitio web o una aplicación móvil. Esto puede incluir el envío de datos de evento sin procesar a un destino como [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) pero también pueden servir para otras funciones.

Es importante diferenciar entre extensiones de etiqueta y de reenvío de eventos. Las extensiones que aparecen en la interfaz de usuario de destinos de Platform son *extensiones de etiquetas*. Consulte la información general sobre el reenvío de eventos para obtener más información sobre [diferencias entre etiquetas y reenvío de eventos](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Ventajas de utilizar extensiones de etiquetas {#extensions-benefits}

Las funciones de etiquetas de Platform son gratuitas para los clientes Experience Cloud existentes. El sistema simplifica la implementación de etiquetas en el sitio web mediante extensiones fáciles de usar que se pueden instalar, configurar, actualizar y eliminar. Las etiquetas dejan un pequeño espacio en el sitio web y le permiten mantener las páginas cargadas rápidamente.

Aunque no puede activar segmentos para etiquetar extensiones, puede configurar reglas para reenviar solo datos de evento en determinadas situaciones. Esta potente funcionalidad le permite reenviar datos de evento solo en determinadas situaciones, en lugar de enviar datos de evento en cada interacción. Para obtener más información, lea acerca de las reglas en [documentación de etiquetas](../../../tags/ui/managing-resources/rules.md).

## Casos de uso de ejemplo para extensiones {#extensions-use-cases}

Las extensiones permiten satisfacer varios casos de uso de clientes. Algunos casos de uso de ejemplo para el uso de extensiones son:

- Puede enviar datos de sitios web o aplicaciones nativas a Facebook mediante la extensión de píxeles de Facebook. Píxel de facebook indica a qué partes del sitio o aplicación navegó un visitante, reenvía esa información a Facebook y puede redireccionar al visitante a través de Facebook.
- Puede reenviar datos de eventos de sus sitios web y aplicaciones a los Google Analytics para analizar y tomar decisiones basadas en esos datos.
- Puede activar una aplicación de chat del lado del cliente en el momento adecuado en función de cómo interactúen los usuarios con las páginas, según las reglas que configure.

## Categorías de extensión {#extension-categories}

Las extensiones pueden clasificarse en las siguientes categorías en Platform:

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de administración de datos](../data-management/overview.md)
- [Destinos de marketing por correo electrónico](../email-marketing/overview.md)
- [Personalización](../personalization/overview.md)
- [Encuestas](../survey/overview.md)
- [Voz del cliente](../voice/overview.md)
