---
title: Tipo de datos de la colección final de lista de estados
description: Obtenga información acerca del tipo de datos Lista de estados de recopilación final Modelo de datos de experiencia (XDM).
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 7%

---

# [!UICONTROL List of States End] tipo de datos

El tipo de datos Lista de estados de recopilación final es un tipo de datos del Modelo de datos de experiencia (XDM) diseñado para representar información relacionada con el estado final de varios atributos de reproductor. Incluye las propiedades [!UICONTROL Player State Name] que indican el estado de atributo específico (por ejemplo, &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;). Este tipo de datos se utiliza para capturar y describir las condiciones iniciales de diferentes estados del reproductor.

![Un diagrama del tipo de datos Lista de estados de fin de colección.](../images/data-types/list-of-states-end-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | cadena | No | Nombre del estado del reproductor. Enumerado: &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con los significados respectivos. |

{style="table-layout:auto"}
