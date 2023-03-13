---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;generador de segmentos;Generador de segmentos
solution: Experience Platform
title: Guía de IU de restricciones de tiempo de segmentación refactorizada
description: El Generador de segmentos proporciona un espacio de trabajo enriquecido que le permite interactuar con los elementos de datos de perfil. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Refactorización con restricciones temporales

La versión de octubre de 2020 para Adobe Experience Platform ha introducido cambios de rendimiento en el servicio de segmentación de Adobe Experience Platform que añaden nuevas restricciones al uso de los operadores lógicos OR y AND. Estos cambios afectarán a los segmentos recién creados o editados realizados con la interfaz de usuario del Generador de segmentos. Esta guía explica cómo mitigar estos cambios.

Antes de la versión de octubre de 2020, todas las restricciones horarias de nivel de regla, nivel de grupo y nivel de evento hacían referencia de forma redundante a la misma marca de tiempo. Para aclarar el uso de la restricción temporal, se han eliminado las restricciones temporales a nivel de regla y de grupo. Para dar cabida a este cambio, todas las restricciones de tiempo deben reescribirse como restricciones de tiempo de nivel de evento.

Anteriormente, un evento individual podía tener varias reglas de restricción de tiempo adjuntas.

![El estilo anterior de las restricciones de tiempo se resalta en el Generador de segmentos.](../images/ui/segment-refactoring/former-time-constraint.png)

Como puede ver, este segmento tiene dos restricciones en el nivel de regla: Una para &quot;[!UICONTROL Hoy]&quot; y el otro para &quot;[!UICONTROL Ayer]&quot;.

El segmento anterior equivale al siguiente: ambas restricciones temporales de nivel de evento se han conectado mediante un operador AND. La primera restricción de tiempo de nivel de evento hace referencia a un evento de clic cuyo nombre es igual a &quot;Aprendizaje&quot; y que se produce hoy, mientras que la segunda restricción de tiempo de nivel de evento hace referencia a un evento de clic cuyo nombre es igual a &quot;Mascotas&quot; y que se produjo ayer.

![El nuevo estilo de restricciones de tiempo se resalta en el Generador de segmentos.](../images/ui/segment-refactoring/time-constraint-1.png) ![El nuevo estilo de restricciones de tiempo se resalta en el Generador de segmentos.](../images/ui/segment-refactoring/time-constraint-2.png)

Esta refactorización de las restricciones de tiempo también afecta a las restricciones de tiempo que están conectadas mediante un operador OR.
