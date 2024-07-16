---
title: Tipo de datos de recopilación de detalles de Advertising Pod
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de recopilación de detalles de Advertising Pod.
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Detalles de Advertising Pod] Tipo de datos de colección

La colección [!UICONTROL Advertising Pod Details] es un tipo de datos estándar del Modelo de datos de experiencia (XDM). Define una secuencia o grupo de anuncios que normalmente se reproducen sucesivamente durante los saltos de contenido. Utilice la colección [!UICONTROL Advertising Pod Details] para capturar detalles como el ID de la pausa publicitaria, un nombre descriptivo para la pausa publicitaria, el índice de anuncios dentro de la pausa publicitaria y el desplazamiento de la pausa publicitaria dentro de la cronología del contenido en segundos.

![Un diagrama del tipo de datos de recopilación de información de detalles de Advertising Pod.](../images/data-types/advertising-pod-details-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Posición del anuncio en la secuencia] | `index` | entero | Sí | Índice de la publicidad dentro del inicio de pausa publicitaria principal. |
| [!UICONTROL Nombre descriptivo de la secuencia] | `friendlyName` | cadena | No | El nombre fácilmente comprensible de la pausa publicitaria. |
| [!UICONTROL Desplazamiento de secuencia] | `offset` | entero | Sí | El desplazamiento del desglose de anuncios dentro del contenido, en segundos. |
