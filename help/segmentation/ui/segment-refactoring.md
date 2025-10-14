---
solution: Experience Platform
title: Guía de IU de restricciones de tiempo de segmentación refactorizada
description: El Generador de segmentos proporciona un espacio de trabajo enriquecido que le permite interactuar con los elementos de datos de perfil. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos.
hidefromtoc: true
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: c7d71113ddcef6aca8b2637814b46e589a6b7fdf
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 9%

---

# Refactorización de las restricciones temporales {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Refactorización de las restricciones temporales"
>abstract="Se han eliminado las restricciones temporales a nivel de regla y de grupo para aclarar el uso de restricciones temporales. Vuelva a escribir la restricción como una restricción temporal a nivel de lienzo o de tarjeta."

La versión de enero de 2024 para Adobe Experience Platform ha introducido cambios en el servicio de segmentación de Adobe Experience Platform que agregan nuevas restricciones en los casos en los que se pueden definir restricciones de tiempo. Estos cambios afectan a los segmentos recién creados o editados realizados con la IU del Generador de segmentos. Esta guía explica cómo mitigar estos cambios.

Antes de la versión de enero de 2024, todas las restricciones temporales de nivel de regla, nivel de grupo y nivel de lienzo hacían referencia de forma redundante a la misma marca de tiempo. Para aclarar el uso de la restricción temporal, se han eliminado las restricciones temporales a nivel de regla y de grupo. Para dar cabida a este cambio, todas las restricciones de tiempo **deben** reescribirse como **restricciones de tiempo de nivel de lienzo** o de nivel de tarjeta **5&rbrace;.**

Anteriormente, un evento individual podía tener varias reglas de restricción de tiempo adjuntas. Con esta actualización reciente, intentar agregar una restricción de tiempo a una regla dará como resultado **error**.

![Se resalta la restricción de tiempo a nivel de regla. También se resalta el error que se produce posteriormente. &#x200B;](../images/ui/segment-refactoring/rule-time-constraint.png)

Ahora, las restricciones de tiempo solo se pueden aplicar en el nivel de lienzo o de tarjeta.

Al aplicar una restricción de tiempo en el nivel de lienzo, aún puede seleccionar todas las restricciones de tiempo disponibles.

>[!NOTE]
>
>Si solo hay **una** tarjeta en el lienzo, aplicar la restricción de tiempo a la tarjeta es **equivalente** a aplicar la restricción de tiempo en el nivel de lienzo.
>
>Si hay **varias** tarjetas en el lienzo, al aplicar la restricción de tiempo al nivel de lienzo, se aplicará esa restricción de tiempo a **todas** las tarjetas en el lienzo.

![Se resalta la restricción de tiempo en el nivel de lienzo.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Para aplicar una restricción de tiempo en el nivel de tarjeta, seleccione la tarjeta específica a la que desee aplicar la restricción de tiempo. Aparece el contenedor **[!UICONTROL Reglas de evento]**. Ahora puede seleccionar la restricción de tiempo que desee aplicar a la tarjeta.

![Se ha resaltado la restricción de tiempo a nivel de tarjeta.](../images/ui/segment-refactoring/card-time-constraint.png)
