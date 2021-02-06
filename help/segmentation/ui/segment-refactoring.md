---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Generador de segmentos;Generador de segmentos
solution: Experience Platform
title: Guía de la interfaz de usuario de restricciones de tiempo de segmentación refactorizada
topic: ui guide
description: 'El Generador de segmentos proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de datos de Perfil. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar propiedades de datos. '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Refactorización de las limitaciones de tiempo

La versión de octubre de 2020 para Adobe Experience Platform ha introducido cambios de rendimiento en el servicio de segmentación de Adobe Experience Platform que agregan nuevas restricciones al uso de los operadores lógicos O y AND. Estos cambios afectarán a los segmentos recién creados o editados realizados mediante la interfaz de usuario del Generador de segmentos. Esta guía explica cómo mitigar estos cambios.

Antes de la versión de octubre de 2020, todas las restricciones de tiempo a nivel de regla, de grupo y de evento hacían referencia de forma redundante a la misma marca de tiempo. Para aclarar el uso de restricciones de tiempo, se han eliminado las restricciones de tiempo a nivel de regla y de grupo. Para adaptarse a este cambio, todas las restricciones de tiempo deben reescribirse como restricciones de tiempo de nivel de evento.

Anteriormente, un evento individual podía tener varias reglas de restricción de tiempo adjuntas.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Como puede ver, este segmento tiene dos restricciones en el nivel de regla: Uno para &quot;[!UICONTROL Hoy]&quot; y el otro para &quot;[!UICONTROL Ayer]&quot;.

El segmento anterior es equivalente al siguiente — ambas restricciones de tiempo de nivel de evento se han conectado mediante un operador Y. La primera restricción de tiempo de nivel de evento hace referencia a un evento de clics cuyo nombre es igual a &quot;Formación&quot; y se está produciendo hoy, mientras que la segunda restricción de tiempo de nivel de evento hace referencia a un evento de clics cuyo nombre es igual a &quot;Mascotas&quot; y se produjo ayer.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Esta refactorización de las restricciones de tiempo también afecta a las restricciones de tiempo que están conectadas mediante un operador O.