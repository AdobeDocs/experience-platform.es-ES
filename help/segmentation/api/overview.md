---
title: Guía de API del servicio de segmentación
description: La API del servicio de segmentación permite a los desarrolladores administrar mediante programación las operaciones de segmentación en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 3%

---

# Guía de API del servicio de segmentación

Adobe Experience Platform [!DNL Segmentation Service] le permite crear audiencias a través de definiciones de segmentos u otras fuentes en Adobe Experience Platform a partir de sus datos de [!DNL Real-Time Customer Profile].

La API [!DNL Segmentation Service] proporciona varios extremos que le permiten administrar mediante programación las operaciones de segmentación en [!DNL Experience Platform]. Este documento de información general proporciona introducciones de alto nivel a cada uno de estos extremos y vínculos a sus guías de extremos asociadas para obtener más detalles. Antes de leer las guías de extremos individuales, consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados obligatorios, la lectura de llamadas de API de ejemplo y mucho más.

Para ver todos los extremos disponibles y las operaciones de CRUD, consulte la [referencia de la API del servicio de segmentación](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Públicos

Las audiencias son una colección de personas que comparten comportamientos o características similares. Se pueden generar mediante Platform o desde fuentes externas. Puede usar el extremo `/audiences` para recuperar todas las audiencias, crear una audiencia nueva, recuperar detalles de una audiencia específica, actualizar una audiencia específica o eliminar una audiencia específica.

Para obtener más información sobre cómo usar este extremo, lea la [guía de extremo de audiencias](./audiences.md).

## Exportar trabajos

Los trabajos de exportación son procesos asincrónicos que se utilizan para mantener los miembros de segmentos de audiencia en conjuntos de datos. Puede utilizar el extremo `/export/jobs` para recuperar todos los trabajos de exportación, crear un nuevo trabajo de exportación, recuperar detalles de un trabajo de exportación específico o cancelar un trabajo de exportación específico.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de trabajos de exportación](./export-jobs.md).

## Previsualizaciones y estimaciones

Las vistas previas proporcionan una lista paginada de perfiles aptos para una definición de segmento, lo que le permite comparar los resultados con lo que espera. Puede utilizar el extremo `/preview` para crear un nuevo trabajo de vista previa o buscar los resultados de un trabajo de vista previa específico.

Las estimaciones proporcionan información estadística para las definiciones de segmentos, como el tamaño de audiencia proyectado, el intervalo de confianza y la desviación estándar de error. Puede usar el extremo `/estimate` para ver una estimación de una definición de segmento.

Para obtener más información sobre el uso de estos extremos, lea la [guía de extremos de estimaciones y vistas previas](./previews-and-estimates.md).

## Programaciones

Los programas son una herramienta que se puede utilizar para ejecutar automáticamente trabajos de segmentación por lotes una vez al día. Puede usar el extremo `/config/schedules` para recuperar una lista de programaciones, crear una nueva programación, recuperar detalles de una programación específica, actualizar una programación específica o eliminar una programación específica.

Para obtener más información sobre cómo usar este extremo, lea la [guía de extremo de programaciones](./schedules.md).

## Definiciones de segmentos

Las definiciones de segmentos definen qué perfiles formarán parte de qué audiencia. Puede usar el extremo `/segment/definitions` para administrar definiciones de segmento.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de definiciones de segmento](./segment-definitions.md).

## Trabajos de segmento

Los trabajos de segmentos procesan las definiciones de segmentos establecidas anteriormente para generar una audiencia. Puede usar el extremo `/segment/jobs` para administrar trabajos de segmentos.

Para obtener más información sobre el uso de este extremo, lea la [guía de extremo de trabajos de segmentación](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar campos contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Para comenzar a trabajar con la búsqueda de segmentos, consulte la [guía de extremo de búsqueda](segment-search.md)

## Pasos siguientes

Para empezar a usar la API [!DNL Segmentation Service], revise las distintas guías de extremos para ver los pasos detallados sobre cómo realizar llamadas a los distintos extremos del servicio. Para obtener más información sobre cómo trabajar con segmentos mediante la interfaz de usuario de [!DNL Platform], consulte la [Guía del usuario de segmentación](../ui/overview.md).
