---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;API;api;
title: Guía de API del servicio de segmentación
topic-legacy: guide
description: La API del servicio de segmentación permite a los desarrolladores administrar mediante programación las operaciones de segmentación en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Guía de API del servicio de segmentación

[!DNL Adobe Experience Platform Segmentation Service] le permite crear segmentos y generar audiencias a partir  [!DNL Adobe Experience Platform] de sus  [!DNL Real-time Customer Profile] datos.

La API [!DNL Segmentation Service] proporciona varios extremos que le permiten administrar mediante programación sus operaciones de segmentación en [!DNL Experience Platform]. Este documento de información general proporciona introducciones de alto nivel a cada uno de estos puntos finales y vínculos a sus guías de puntos finales asociadas para obtener más información. Antes de leer las guías de puntos finales individuales, consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y las operaciones de CRUD, consulte la [referencia de la API del servicio de segmentación](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exportar trabajos

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener a los miembros del segmento de audiencia en conjuntos de datos. Puede utilizar el extremo `/export/jobs` para recuperar todos los trabajos de exportación, crear un nuevo trabajo de exportación, recuperar detalles de un trabajo de exportación específico o cancelar un trabajo de exportación específico.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de trabajos de exportación](./export-jobs.md).

## Previsión y estimaciones

Las vistas previas proporcionan una lista paginada de perfiles cualificados para una definición de segmento, lo que le permite comparar los resultados con lo que espera. Puede utilizar el extremo `/preview` para crear un nuevo trabajo de vista previa o buscar los resultados de un trabajo de vista previa específico.

Las estimaciones proporcionan información estadística para definiciones de segmentos, como tamaño de audiencia proyectado, intervalo de confianza y desviación estándar de errores. Puede utilizar el extremo `/estimate` para ver una estimación de una definición de segmento.

Para obtener más información sobre el uso de estos extremos, lea la [guía de vistas previas y estimaciones de puntos finales](./previews-and-estimates.md).

## Programaciones

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día. Puede utilizar el extremo `/config/schedules` para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

Para obtener más información sobre el uso de este punto final, lea la [guía de extremo de programación](./schedules.md).

## Definiciones de segmentos

Las definiciones de segmentos definen qué perfiles formarán parte de cada segmento de audiencia. Puede utilizar el extremo `/segment/definitions` para administrar las definiciones de segmentos.

Para obtener más información sobre el uso de este punto final, lea la [guía de extremo de definiciones de segmento](./segment-definitions.md).

## Trabajos de segmentos

Los trabajos de segmentos procesan definiciones de segmentos establecidas anteriormente para generar un segmento de audiencia. Puede utilizar el extremo `/segment/jobs` para administrar los trabajos de segmentos.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de trabajos de segmento](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar campos contenidos en varias fuentes de datos y devolverlos casi en tiempo real. Para empezar a trabajar con la búsqueda de segmentos, consulte la [guía de extremo de búsqueda](segment-search.md)

## Pasos siguientes

Para comenzar con la API [!DNL Segmentation Service], revise las distintas guías de puntos finales para ver los pasos detallados sobre cómo realizar llamadas a los distintos puntos finales del servicio. Para obtener más información sobre el trabajo con segmentos mediante la interfaz de usuario [!DNL Platform], consulte la [Guía del usuario de segmentación](../ui/overview.md).
