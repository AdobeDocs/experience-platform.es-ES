---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;API;api;
title: Guía de API del servicio de segmentación
topic: guide
description: La API de servicio de segmentación permite a los desarrolladores administrar mediante programación las operaciones de segmentación en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave mediante la API.
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Guía de la API del servicio de segmentación

[!DNL Adobe Experience Platform Segmentation Service] le permite crear segmentos y generar audiencias a partir  [!DNL Adobe Experience Platform] de  [!DNL Real-time Customer Profile] los datos.

La API [!DNL Segmentation Service] proporciona varios extremos que le permiten administrar mediante programación las operaciones de segmentación en [!DNL Experience Platform]. Este documento de información general proporciona introducciones de alto nivel a cada uno de estos extremos y vínculos a sus guías de punto final asociadas para obtener más información. Antes de leer las guías de punto final individuales, consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados requeridos, leer las llamadas de API de muestra y mucho más.

Para vista de todos los extremos disponibles y las operaciones de CRUD, consulte la [referencia de la API de servicio de segmentación](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Trabajos de exportación

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener a los miembros del segmento de audiencia en conjuntos de datos. Puede utilizar el extremo `/export/jobs` para recuperar todos los trabajos de exportación, crear un nuevo trabajo de exportación, recuperar detalles de un trabajo de exportación específico o cancelar un trabajo de exportación específico.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de trabajos de exportación](./export-jobs.md).

## Previsualizaciones y estimaciones

Las previsualizaciones proporcionan una lista paginada de perfiles de cualificación para una definición de segmento, lo que le permite comparar los resultados con lo que espera. Puede utilizar el extremo `/preview` para crear un nuevo trabajo de previsualización o buscar resultados de un trabajo de previsualización específico.

Las estimaciones proporcionan información estadística para definiciones de segmentos, como tamaño de audiencia proyectado, intervalo de confianza y desviación estándar de errores. Puede utilizar el extremo `/estimate` para vista una estimación de una definición de segmento.

Para obtener más información sobre el uso de estos extremos, lea la [guía de puntos finales de previsualizaciones y estimaciones](./previews-and-estimates.md).

## Programaciones

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día. Puede utilizar el extremo `/config/schedules` para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

Para obtener más información sobre el uso de este extremo, lea la guía del extremo [programa](./schedules.md).

## Definiciones de segmentos

Las definiciones de segmentos definen qué perfiles formarán parte de cada segmento de audiencia. Puede utilizar el extremo `/segment/definitions` para administrar las definiciones de segmentos.

Para obtener más información sobre el uso de este extremo, lea la guía de extremo de definiciones de segmento [](./segment-definitions.md).

## Trabajos de segmentos

Los trabajos de segmentos procesan definiciones de segmentos previamente establecidas para generar un segmento de audiencia. Puede utilizar el extremo `/segment/jobs` para administrar los trabajos de segmentos.

Para obtener más información sobre el uso de este extremo, lea la guía de extremo de trabajos de segmento [](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar los campos contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Para comenzar a trabajar con la búsqueda de segmentos, consulte la [guía de extremo de búsqueda](segment-search.md)

## Pasos siguientes

Para comenzar con la API [!DNL Segmentation Service], revise las distintas guías de punto final para ver los pasos detallados sobre cómo realizar llamadas a los distintos extremos del servicio. Para obtener más información sobre cómo trabajar con segmentos mediante la [!DNL Platform] interfaz de usuario, consulte la [Guía del usuario de segmentación](../ui/overview.md).