---
solution: Experience Platform
title: Ignorar actualización de restricción de tiempo de año
description: Obtenga información sobre cómo resolver un problema con la restricción de tiempo de ignorar año.
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: 006950092f69d378b064c795b117166343e5d8f2
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 8%

---

# Actualización de la restricción temporal de Ignorar año {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Actualización de Ignorar año"
>abstract="Se ha actualizado la restricción temporal de Ignorar año. Vuelva a guardar el público."

>[!IMPORTANT]
>
>Solo puede usar la restricción de tiempo &quot;ignorar año&quot; en una definición de segmento evaluada mediante **segmentación por lotes**. Si agrega la restricción de tiempo &quot;omitir año&quot; a la definición del segmento, la audiencia resultante **no será elegible** para la segmentación de Edge o streaming.

La versión de febrero de 2024 para Adobe Experience Platform ha introducido cambios en el servicio de segmentación de Adobe Experience Platform, que resuelve un problema con la opción &quot;ignorar año&quot; en la creación y evaluación de audiencias.

La opción &quot;ignorar año&quot; está diseñada para ignorar el componente año de una fecha cuando se realizan evaluaciones de audiencia. Puede utilizar esta opción en situaciones en las que la relación temporal entre diferentes eventos es importante, pero el año específico no lo es, como un campo de fecha de nacimiento.

Sin embargo, durante años bisiestos como 2024, el sistema subyacente no gestionó correctamente esta opción, lo que resultó en evaluaciones de audiencia inexactas. Como resultado, si &quot;ignorar año&quot; está habilitado en un año bisiesto, la evaluación de audiencia perdería un día.

Si ha creado una audiencia antes de que se publicara esta corrección, solo tiene que volver a guardar la audiencia en el Generador de segmentos para aplicar la corrección. Si no está seguro de si su audiencia se ve afectada por esta resolución, el Generador de segmentos le preguntará al usuario si la audiencia existente se ve afectada por este problema.
