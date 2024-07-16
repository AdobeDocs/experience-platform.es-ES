---
title: Lista de estados Iniciar tipo de datos de colección
description: Obtenga información sobre el tipo de datos de la lista de estados Inicio Modelo de datos de experiencia (XDM).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL Tipo de datos de inicio de lista de estados]

El tipo de datos [!UICONTROL Inicio de lista de estados] es un tipo de datos del Modelo de datos de experiencia (XDM) diseñado para representar información relacionada con el estado inicial de varios atributos del reproductor. Incluye las propiedades [!UICONTROL Player State Name] que indican el estado de atributo específico (por ejemplo, &quot;pantalla completa&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Este tipo de datos se utiliza para capturar y describir las condiciones iniciales de diferentes estados del reproductor.

![Un diagrama de [!UICONTROL lista de estados de inicio] tipo de datos.](../images/data-types/list-of-states-start-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nombre de estado del reproductor] | `name` | cadena | No | Nombre del estado del reproductor. Enumerado: &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con los significados respectivos. |

{style="table-layout:auto"}
