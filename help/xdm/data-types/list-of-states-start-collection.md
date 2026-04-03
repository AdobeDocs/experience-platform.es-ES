---
title: Lista de estados Iniciar tipo de datos de colección
description: Obtenga información sobre el tipo de datos de la lista de estados Inicio Modelo de datos de experiencia (XDM).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 8%

---

# [!UICONTROL List of States Start] tipo de datos

El tipo de datos [!UICONTROL List of States Start] es un tipo de datos del Modelo de datos de experiencia (XDM) diseñado para representar información relacionada con el estado de inicio de varios atributos de reproductor. Incluye las propiedades [!UICONTROL Player State Name] que indican el estado de atributo específico (por ejemplo, &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;). Este tipo de datos se utiliza para capturar y describir las condiciones iniciales de diferentes estados del reproductor.

![Un diagrama de [!UICONTROL List of States Start] tipo de datos.](../images/data-types/list-of-states-start-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | cadena | No | Nombre del estado del reproductor. Enumerado: &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con los significados respectivos. |

{style="table-layout:auto"}
