---
keywords: extensiones de etiqueta;extensión de etiqueta;destinos de inicio; extensiones de etiquetas de plataforma;extensión de etiquetas de plataforma;destinos de platform launch
title: Extensiones de etiquetas en Adobe Experience Platform
description: Adobe Experience Platform proporciona la siguiente generación de funcionalidades de administración de etiquetas de Adobe. Platform le ofrece una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 010e05968f1d7ad5675b0f0af43d9cfcc1f3a2ff
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 1%

---

# Etiquetar extensiones en Adobe Experience Platform

Adobe Experience Platform proporciona la siguiente generación de funcionalidades de administración de etiquetas de Adobe. Platform le ofrece una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes. Las etiquetas se ofrecen a los clientes de Adobe Experience Cloud como una función incluida que añade valor.

Para obtener una introducción a las etiquetas, consulte los recursos a continuación:

- [Información general sobre etiquetas](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=es)
- [Guía de inicio rápido](../../../tags/quick-start/quick-start.md)

## Búsqueda de extensiones de etiquetas en la interfaz de Platform {#how-to-find-extensions-in-interface}

Para buscar las extensiones en la interfaz de Platform, vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** y seleccione **[!UICONTROL Extensions]** en el filtro **[!UICONTROL Types]**.

![Filtro Extensiones en la interfaz](../../assets/catalog/launch-extensions/filter.png)

## Funcionamiento de las extensiones de etiquetas {#how-extensions-work}

Las extensiones reenvían datos de eventos sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino **Event Forwarding**. Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de eventos sin procesar. Algunos ejemplos son la [Gainsight personalization extension](../personalization/gainsight.md) o la [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Los destinos de** exportación de perfil/segmento en Adobe Experience Platform capturan datos de evento, los combinan con otras fuentes de datos, aplican segmentación y exportan segmentos y perfiles cualificados a los destinos. Algunos ejemplos son el [destino de almacenamiento en la nube de Amazon S3](../cloud-storage/amazon-s3.md) o el [destino publicitario de Google Display &amp; Video 360](../advertising/google-dv360.md).

![Etiquetar extensiones en comparación con otros destinos](../../assets/common/launch-and-other-destinations.png)

## Ventajas del uso de extensiones de etiquetas {#extensions-benefits}

Las funcionalidades de etiquetas de Platform son gratuitas para los clientes Experience Cloud existentes. El sistema simplifica la implementación de etiquetas en el sitio web a través de extensiones fáciles de usar que puede instalar, configurar, actualizar y eliminar. Las etiquetas dejan una huella pequeña en el sitio web y le permiten mantener las páginas cargándose rápidamente.

Aunque no puede activar segmentos para etiquetar extensiones, puede configurar reglas para que solo reenvíen datos de evento en determinadas situaciones. Esta potente funcionalidad permite reenviar datos de evento solo en determinadas situaciones, en lugar de enviar datos de evento en cada interacción. Para obtener más información, lea sobre las reglas en la [documentación de etiquetas](../../../tags/ui/managing-resources/rules.md).

## Ejemplos de casos de uso de extensiones {#extensions-use-cases}

Las extensiones permiten satisfacer varios casos de uso de clientes. Algunos ejemplos de casos de uso de extensiones son:

- Puede enviar datos de sitios web o aplicaciones nativas a Facebook a través de la extensión de píxeles de Facebook. Facebook Pixel indica a qué partes del sitio o de la aplicación navegó un visitante, envía esa información a Facebook y puede redirigirse al visitante a través de Facebook.
- Puede reenviar datos de eventos de sus sitios web y aplicaciones a Google Analytics para que analicen y tomen decisiones basadas en esos datos.
- Puede activar una aplicación de chat del lado del cliente en el momento adecuado en función de cómo interactúan los usuarios con sus páginas, según las reglas que haya configurado.

## Categorías de extensión {#extension-categories}

Las extensiones pueden incluirse en las siguientes categorías de Platform:

- [Publicidad](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gestión de datos](../data-management/overview.md)
- [Destinos de marketing por correo electrónico](../email-marketing/overview.md)
- [Personalización](../personalization/overview.md)
- [Encuestas](../survey/overview.md)
- [Voz del cliente](../voice/overview.md)
