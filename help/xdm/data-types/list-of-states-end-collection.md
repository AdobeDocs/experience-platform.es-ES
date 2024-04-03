---
title: Tipo de datos de la colección final de lista de estados
description: Obtenga información acerca del tipo de datos Lista de estados de recopilación final Modelo de datos de experiencia (XDM).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL Fin de lista de estados] tipo de datos

El tipo de datos Lista de estados de recopilación final es un tipo de datos del Modelo de datos de experiencia (XDM) diseñado para representar información relacionada con el estado final de varios atributos de reproductor. Incluye el [!UICONTROL Nombre del estado del reproductor] propiedades que indican el estado de atributo específico (por ejemplo, &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;). Este tipo de datos se utiliza para capturar y describir las condiciones iniciales de diferentes estados del reproductor.

![Un diagrama del tipo de datos Lista de estados de recopilación final.](../images/data-types/list-of-states-end-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nombre del estado del reproductor] | `name` | string | No | Nombre del estado del reproductor. Enumerado: &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con los significados respectivos. |

{style="table-layout:auto"}
