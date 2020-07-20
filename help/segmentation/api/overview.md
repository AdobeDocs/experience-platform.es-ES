---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía para desarrolladores de Adobe Experience Platform Segmentation Service
topic: guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# Guía para desarrolladores de API de servicio de segmentación por Adobe Experience Platform

[!DNL Adobe Experience Platform Segmentation Service] le permite crear segmentos y generar audiencias a partir [!DNL Adobe Experience Platform] de sus [!DNL Real-time Customer Profile] datos.

La [!DNL Segmentation Service] API proporciona varios extremos que le permiten administrar mediante programación las operaciones de segmentación en [!DNL Experience Platform]. Este documento de información general proporciona introducciones de alto nivel a cada uno de estos extremos y vínculos a sus guías de punto final asociadas para obtener más información. Antes de leer las guías de punto final individuales, consulte la guía [de](./getting-started.md) introducción para obtener información importante sobre los encabezados requeridos, leer las llamadas de API de muestra y mucho más.

Para vista de todos los extremos disponibles y las operaciones de CRUD, consulte la referencia [de la API de servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentación.

## Trabajos de exportación

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener a los miembros del segmento de audiencia en conjuntos de datos. Puede utilizar el extremo para recuperar todos los trabajos de exportación, crear un nuevo trabajo de exportación, recuperar detalles de un trabajo de exportación específico o cancelar un trabajo de exportación específico. `/export/jobs`

Para obtener más información sobre el uso de este extremo, lea la guía de extremo de trabajos de [exportación](./export-jobs.md).

## Previsualizaciones y estimaciones

Las Previsualizaciones proporcionan una lista paginada de perfiles de cualificación para una definición de segmento, lo que le permite comparar los resultados con lo que espera. Puede usar el extremo para crear un nuevo trabajo de previsualización o buscar los resultados de un trabajo de previsualización específico. `/preview`

Las estimaciones proporcionan información estadística para definiciones de segmentos, como tamaño de audiencia proyectado, intervalo de confianza y desviación estándar de errores. Puede utilizar el punto final para realizar la vista de una estimación de una definición de segmento. `/estimate`

Para obtener más información sobre el uso de estos extremos, lea la guía [de puntos finales de](./previews-and-estimates.md)previsualizaciones y estimaciones.

## Programaciones

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día. Puede utilizar el extremo para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica. `/config/schedules`

Para obtener más información sobre el uso de este punto final, lea la guía del punto final de la [programación](./schedules.md).

## Definiciones de segmentos

Las definiciones de segmentos definen qué perfiles formarán parte de cada segmento de audiencia. Puede utilizar el extremo para administrar las definiciones de segmentos `/segment/definitions` .

Para obtener más información sobre el uso de este punto final, lea la guía del punto final de definiciones de [segmentos](./segment-definitions.md).

## Trabajos de segmentos

Los trabajos de segmentos procesan definiciones de segmentos previamente establecidas para generar un segmento de audiencia. Puede usar el extremo para administrar los trabajos de segmentos `/segment/jobs` .

Para obtener más información sobre el uso de este extremo, lea la guía de extremo de trabajos de [segmento](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar los campos contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Para comenzar a trabajar con la búsqueda de segmentos, consulte la guía de punto final de [búsqueda](segment-search.md)

## Pasos siguientes

Para comenzar con la [!DNL Segmentation Service] API, consulte las distintas guías de punto final para ver los pasos detallados sobre cómo realizar llamadas a los distintos puntos finales del servicio. Para obtener más información sobre cómo trabajar con segmentos mediante la [!DNL Platform] interfaz de usuario, consulte la guía [del usuario](../ui/overview.md)Segmentación.