---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;API;api;
title: Guía de API del servicio de segmentación
description: La API del servicio de segmentación permite a los desarrolladores administrar mediante programación las operaciones de segmentación en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# Guía de API del servicio de segmentación

[!DNL Adobe Experience Platform Segmentation Service] le permite crear segmentos y generar audiencias en [!DNL Adobe Experience Platform] de su [!DNL Real-Time Customer Profile] datos.

La variable [!DNL Segmentation Service] La API proporciona varios puntos de conexión que le permiten administrar mediante programación sus operaciones de segmentación en [!DNL Experience Platform]. Este documento de información general proporciona introducciones de alto nivel a cada uno de estos puntos finales y vínculos a sus guías de puntos finales asociadas para obtener más información. Antes de leer las guías de puntos finales individuales, consulte la sección [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y las operaciones de CRUD, consulte la [Referencia de la API del servicio de segmentación](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## Exportar trabajos

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener a los miembros del segmento de audiencia en conjuntos de datos. Puede usar la variable `/export/jobs` para recuperar todos los trabajos de exportación, crear un nuevo trabajo de exportación, recuperar detalles de un trabajo de exportación específico o cancelar un trabajo de exportación específico.

Para obtener más información sobre el uso de este punto final, lea la [exportar guía de extremo de trabajos](./export-jobs.md).

## Previsión y estimaciones

Las vistas previas proporcionan una lista paginada de perfiles cualificados para una definición de segmento, lo que le permite comparar los resultados con lo que espera. Puede usar la variable `/preview` para crear un nuevo trabajo de vista previa o buscar resultados de un trabajo de vista previa específico.

Las estimaciones proporcionan información estadística para definiciones de segmentos, como tamaño de audiencia proyectado, intervalo de confianza y desviación estándar de errores. Puede usar la variable `/estimate` para ver una estimación de una definición de segmento.

Para obtener más información sobre el uso de estos extremos, lea la [guía de extremos de vista previa y estimación](./previews-and-estimates.md).

## Programaciones

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente los trabajos de segmentación por lotes una vez al día. Puede usar la variable `/config/schedules` para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

Para obtener más información sobre el uso de este punto final, lea la [guía de extremo sobre programaciones](./schedules.md).

## Definiciones de segmentos

Las definiciones de segmentos definen qué perfiles formarán parte de cada segmento de audiencia. Puede usar la variable `/segment/definitions` para administrar definiciones de segmentos.

Para obtener más información sobre el uso de este punto final, lea la [guía de extremo de definiciones de segmentos](./segment-definitions.md).

## Trabajos de segmentos

Los trabajos de segmentos procesan definiciones de segmentos establecidas anteriormente para generar un segmento de audiencia. Puede usar la variable `/segment/jobs` para administrar los trabajos de segmentos.

Para obtener más información sobre el uso de este punto final, lea la [guía de extremo de trabajos de segmentos](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar campos contenidos en varias fuentes de datos y devolverlos casi en tiempo real. Para empezar a trabajar con la búsqueda de segmentos, consulte la [guía de extremo de búsqueda](segment-search.md)

## Pasos siguientes

Para empezar con el [!DNL Segmentation Service] , revise las distintas guías de puntos finales para ver los pasos detallados sobre cómo realizar llamadas a los distintos puntos finales del servicio. Para obtener más información sobre cómo trabajar con segmentos, use la variable [!DNL Platform] La interfaz de usuario de puede consultar la [Guía del usuario de segmentación](../ui/overview.md).
