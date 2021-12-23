---
keywords: extensiones de etiqueta;extensión de etiqueta;destinos de inicio; extensiones de etiquetas de plataforma;extensión de etiquetas de plataforma;destinos de platform launch
title: Extensiones de etiquetas en Adobe Experience Platform
description: Adobe Experience Platform proporciona la siguiente generación de funcionalidades de administración de etiquetas de Adobe. Platform le ofrece una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Etiquetar extensiones en Adobe Experience Platform

Adobe Experience Platform proporciona la siguiente generación de funcionalidades de administración de etiquetas de Adobe. Platform gives you a simple way to deploy and manage all of the analytics, marketing, and advertising tags necessary to power relevant customer experiences. Tags are offered to Adobe Experience Cloud customers as an included, value-add feature.

Para obtener una introducción a las etiquetas, consulte los recursos a continuación:

- [Información general sobre etiquetas](../../../tags/home.md)
- [Guía de inicio rápido](../../../tags/quick-start/quick-start.md)

## How to find tag extensions in the Platform interface {#how-to-find-extensions-in-interface}

Para buscar las extensiones en la interfaz de Platform, vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** y seleccione **[!UICONTROL Extensiones]** en el **[!UICONTROL Tipos]** filtro.

![Filtro Extensiones en la interfaz](../../assets/catalog/launch-extensions/filter.png)

## Funcionamiento de las extensiones de etiquetas {#how-extensions-work}

A [extensión de etiqueta](../../../tags/home.md#extensions) es un paquete de código que mejora la funcionalidad de un sitio web o una aplicación móvil. Esto podría incluir el envío de datos de eventos sin procesar a un destino como [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) pero también pueden servir otras funciones.

Es importante diferenciar entre las extensiones de reenvío de etiquetas y de eventos. Las extensiones que aparecen en la interfaz de usuario de destinos de Platform son *extensiones de etiqueta*. Consulte la descripción general sobre el reenvío de eventos para obtener más información sobre el [diferencias entre etiquetas y reenvío de eventos](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Ventajas del uso de extensiones de etiquetas {#extensions-benefits}

Platform&#39;s tag capabilities are free for existing Experience Cloud customers. The system simplifies tag deployment on your website via easy-to-use extensions that you can install, configure, update, and delete. Tags leave a small footprint on your website and allow you to keep your pages loading quickly.

Aunque no puede activar segmentos para etiquetar extensiones, puede configurar reglas para que solo reenvíen datos de evento en determinadas situaciones. This powerful functionality enables you to forward event data only in certain situations as opposed to sending event data on every interaction. For more information, read about rules in the [tags documentation](../../../tags/ui/managing-resources/rules.md).

## Example use cases for extensions {#extensions-use-cases}

Las extensiones permiten satisfacer varios casos de uso de clientes. Algunos ejemplos de casos de uso de extensiones son:

- Puede enviar datos de sitios web o aplicaciones nativas a Facebook a través de la extensión de píxeles de Facebook. Facebook Pixel indica a qué partes del sitio o de la aplicación navegó un visitante, envía esa información a Facebook y puede redirigirse al visitante a través de Facebook.
- Puede reenviar datos de eventos de sus sitios web y aplicaciones a Google Analytics para que analicen y tomen decisiones basadas en esos datos.
- Puede activar una aplicación de chat del lado del cliente en el momento adecuado en función de cómo interactúan los usuarios con sus páginas, según las reglas que haya configurado.

## Categorías de extensión {#extension-categories}

Las extensiones pueden incluirse en las siguientes categorías de Platform:

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gestión de datos](../data-management/overview.md)
- [Destinos de marketing por correo electrónico](../email-marketing/overview.md)
- [Personalización](../personalization/overview.md)
- [Encuestas](../survey/overview.md)
- [Voz del cliente](../voice/overview.md)
