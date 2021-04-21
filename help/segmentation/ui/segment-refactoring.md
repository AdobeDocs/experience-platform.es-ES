---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Generador de segmentos;Generador de segmentos
solution: Experience Platform
title: Guía de la interfaz de usuario sobre restricciones de tiempo de segmentación refactorizada
topic-legacy: ui guide
description: El Generador de segmentos proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de datos de perfil. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Refactorización de restricciones de tiempo

La versión de octubre de 2020 para Adobe Experience Platform ha introducido cambios de rendimiento en el servicio de segmentación de Adobe Experience Platform que añaden nuevas restricciones al uso de los operadores lógicos OR y AND. Estos cambios afectarán a los segmentos recién creados o editados realizados mediante la interfaz de usuario del Generador de segmentos. Esta guía explica cómo mitigar estos cambios.

Antes de la versión de octubre de 2020, todas las restricciones de tiempo de nivel de regla, de grupo y de evento hacían referencia de forma redundante a la misma marca de tiempo. Para aclarar el uso de la restricción de tiempo, se han eliminado las restricciones de tiempo a nivel de regla y de grupo. Para dar cabida a este cambio, todas las restricciones de tiempo deben reescribirse como restricciones de tiempo de nivel de evento.

Anteriormente, un evento individual podía tener varias reglas de restricción de tiempo adjuntas.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Como puede ver, este segmento tiene dos restricciones en el nivel de regla: Uno para &quot;[!UICONTROL Today]&quot; y el otro para &quot;[!UICONTROL Yesterday]&quot;.

El segmento anterior es equivalente al siguiente segmento: ambas restricciones de tiempo de nivel de evento se han conectado mediante un operador AND. La primera restricción de tiempo a nivel de evento hace referencia a un evento de clic cuyo nombre es igual a &quot;Formación&quot; y está ocurriendo hoy, mientras que la segunda restricción de tiempo a nivel de evento hace referencia a un evento de clic cuyo nombre es igual a &quot;Mascotas&quot; y ocurrió ayer.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Esta refactorización de las restricciones de tiempo también afecta a las restricciones de tiempo que están conectadas mediante un operador OR.
