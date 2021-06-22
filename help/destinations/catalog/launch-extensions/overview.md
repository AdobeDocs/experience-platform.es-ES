---
keywords: extensiones de launch;extensión de launch;destinos de launch; extensiones de platform launch;extensión de platform launch;destinos de platform launch
title: Extensión de Adobe Experience Platform Launch
description: Adobe Experience Platform Launch es la próxima generación de funcionalidades de administración de etiquetas de Adobe. Platform Launch ofrece una alternativa sencilla para implementar y gestionar todas las integraciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 20a9103dd96116f3099bccc9eeb678be5ac2bb79
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 14%

---

# Extensiones de Adobe Experience Platform Launch

Adobe Experience Platform Launch es la función de administración de etiquetas de próxima generación de Adobe. Platform Launch ofrece una alternativa sencilla para implementar y gestionar todas las integraciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes. El platform launch se ofrece a los clientes de Adobe Experience Cloud como una función incluida que añade valor.

Para obtener una introducción a las funciones de Experience Platform Launch, consulte los recursos a continuación:

- Documentación [de Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=es)
- Adobe Experience Platform Launch [vídeos de inicio rápido](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). Comience con [Introducción a Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) y [Información general del proceso de publicación](https://helpx.adobe.com/es/analytics/how-to/adobe-launch-publishing-process.html), a continuación, pase a los conceptos siguientes.

## Cómo encontrar las extensiones de Platform launch en la interfaz de Platform {#how-to-find-extensions-in-interface}

Para buscar las extensiones de Platform launch en la interfaz de Platform, vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** y seleccione **[!UICONTROL Extensions]** en el filtro **[!UICONTROL Types]**.

![Filtro Extensiones en la interfaz](../../assets/catalog/launch-extensions/filter.png)

## Funcionamiento de las extensiones de Platform launch {#how-extensions-work}

Las extensiones de platform launch reenvían datos de eventos sin procesar a varios tipos de destinos. Considere las extensiones como un tipo de destino **Event Forwarding**. Se trata de un tipo más sencillo de integración con las plataformas de destino, que solo reenvía datos de eventos sin procesar. Algunos ejemplos son la [Gainsight personalization extension](../personalization/gainsight.md) o la [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Los destinos de** exportación de perfil/segmento en Adobe Experience Platform capturan datos de evento, los combinan con otras fuentes de datos, aplican segmentación y exportan segmentos y perfiles cualificados a los destinos. Algunos ejemplos son el [destino de almacenamiento en la nube de Amazon S3](../cloud-storage/amazon-s3.md) o el [destino publicitario de Google Display &amp; Video 360](../advertising/google-dv360.md).

![Extensiones de Experience Platform Launch en comparación con otros destinos](../../assets/common/launch-and-other-destinations.png)

## Ventajas del uso de extensiones de Platform launch {#extensions-benefits}

Adobe Experience Platform Launch es gratuito para los clientes Experience Cloud existentes. platform launch simplifica la implementación de etiquetas en su sitio web a través de extensiones fáciles de usar que puede instalar, configurar, actualizar y eliminar. platform launch tiene una huella pequeña en su sitio web y le permite mantener las páginas cargándose rápidamente.

>[!IMPORTANT]
>
>Aunque no puede activar segmentos en extensiones de Platform launch, puede configurar reglas para que solo reenvíen datos de evento en determinadas situaciones. Más información abajo.

Puede crear *reglas* que determinen cuándo reenviar los datos de evento a las extensiones. Esta potente funcionalidad permite reenviar datos de evento solo en determinadas situaciones, en lugar de enviar datos de evento en cada interacción. Para obtener más información, lea sobre las reglas en la [documentación de Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Casos de uso de ejemplo para extensiones de Platform launch {#extensions-use-cases}

Las extensiones de platform launch permiten satisfacer varios casos de uso de clientes. Algunos ejemplos de casos de uso de extensiones de Platform launch son:

- Puede enviar datos de sitios web o aplicaciones nativas a Facebook a través de la extensión de píxeles de Facebook. Facebook Pixel indica a qué partes del sitio o de la aplicación navegó un visitante, envía esa información a Facebook y puede redirigirse al visitante a través de Facebook.
- Puede reenviar datos de eventos de sus sitios web y aplicaciones a Google Analytics para que analicen y tomen decisiones basadas en esos datos.
- Puede activar una aplicación de chat del lado del cliente en el momento adecuado en función de cómo interactúan los usuarios con sus páginas, según las reglas que haya configurado en el Platform launch.

## Categorías de extensión {#extension-categories}

Las extensiones de platform launch pueden incluirse en las siguientes categorías de Platform:

- [Publicidad](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plataforma de gestión de datos](../data-management/overview.md)
- [Destinos de marketing por correo electrónico](../email-marketing/overview.md)
- [Personalización](../personalization/overview.md)
- [Encuestas](../survey/overview.md)
- [Voz del cliente](../voice/overview.md)
