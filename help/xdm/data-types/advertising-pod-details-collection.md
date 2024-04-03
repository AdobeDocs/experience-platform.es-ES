---
title: Tipo de datos de colección de detalles de Advertising Pod
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de recopilación de detalles del Advertising Pod.
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---

# [!UICONTROL Detalles de Advertising Pod] Tipo de datos de colección

[!UICONTROL Detalles de Advertising Pod] La recopilación es un tipo de datos estándar del Modelo de datos de experiencia (XDM). Define una secuencia o grupo de anuncios que normalmente se reproducen sucesivamente durante los saltos de contenido. Utilice el [!UICONTROL Detalles de Advertising Pod] Tipo de datos de recopilación para capturar detalles como el ID de pausa publicitaria, un nombre descriptivo para la pausa publicitaria, el índice de anuncios dentro de la pausa publicitaria y el desplazamiento de la pausa publicitaria dentro de la cronología del contenido en segundos.

![Diagrama del tipo de datos de recopilación de información de detalles de Advertising Pod.](../images/data-types/advertising-pod-details-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Posición del anuncio en la secuencia] | `index` | entero | Sí | Índice de la publicidad dentro del inicio de pausa publicitaria principal. |
| [!UICONTROL Nombre descriptivo del pod] | `friendlyName` | string | No | El nombre fácilmente comprensible de la pausa publicitaria. |
| [!UICONTROL Desplazamiento de pod] | `offset` | entero | Sí | El desplazamiento del desglose de anuncios dentro del contenido, en segundos. |
