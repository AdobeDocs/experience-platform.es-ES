---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;API;api;
title: Guía de API del servicio de segmentación
description: La API del servicio de segmentación permite a los desarrolladores administrar mediante programación las operaciones de segmentación en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# Guía de API del servicio de segmentación

[!DNL Adobe Experience Platform Segmentation Service] le permite generar segmentos y audiencias en [!DNL Adobe Experience Platform] de su [!DNL Real-Time Customer Profile] datos.

El [!DNL Segmentation Service] La API de proporciona varios extremos que le permiten administrar mediante programación las operaciones de segmentación en [!DNL Experience Platform]. Este documento de información general proporciona introducciones de alto nivel a cada uno de estos extremos y vínculos a sus guías de extremos asociadas para obtener más detalles. Antes de leer las guías de extremos individuales, consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

Para ver todos los extremos disponibles y las operaciones de CRUD, consulte la [Referencia de API del servicio de segmentación](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## Exportar trabajos

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener los miembros de segmentos de audiencia en conjuntos de datos. Puede usar el complemento `/export/jobs` extremo para recuperar todos los trabajos de exportación, crear un nuevo trabajo de exportación, recuperar detalles de un trabajo de exportación específico o cancelar un trabajo de exportación específico.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de trabajos de exportación](./export-jobs.md).

## Previsualizaciones y estimaciones

Las vistas previas proporcionan una lista paginada de perfiles aptos para una definición de segmento, lo que le permite comparar los resultados con lo que espera. Puede usar el complemento `/preview` extremo para crear un nuevo trabajo de vista previa o buscar resultados de un trabajo de vista previa específico.

Las estimaciones proporcionan información estadística para las definiciones de segmentos, como el tamaño de audiencia proyectado, el intervalo de confianza y la desviación estándar de error. Puede usar el complemento `/estimate` extremo para ver una estimación de una definición de segmento.

Para obtener más información sobre el uso de estos extremos, lea la [guía de extremos de previsualizaciones y estimaciones](./previews-and-estimates.md).

## Horarios

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente trabajos de segmentación por lotes una vez al día. Puede usar el complemento `/config/schedules` punto final para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de programaciones](./schedules.md).

## Definiciones de segmentos

Las definiciones de segmentos definen qué perfiles formarán parte de qué segmentos de audiencia. Puede usar el complemento `/segment/definitions` extremo para administrar definiciones de segmentos.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de definiciones de segmento](./segment-definitions.md).

## Trabajos de segmento

Los trabajos de segmentos procesan las definiciones de segmentos establecidas anteriormente para generar un segmento de audiencia. Puede usar el complemento `/segment/jobs` extremo para administrar trabajos de segmentos.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de trabajos de segmento](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar campos contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Para empezar a trabajar con la búsqueda de segmentos, consulte las [guía de extremo de búsqueda](segment-search.md)

## Pasos siguientes

Para empezar a usar la [!DNL Segmentation Service] API, revise las diferentes guías de extremos para ver los pasos detallados sobre cómo realizar llamadas a los distintos extremos del servicio. Para obtener más información sobre cómo trabajar con segmentos mediante [!DNL Platform] IU, consulte la [Guía del usuario de segmentación](../ui/overview.md).
