---
title: Tipo de datos de colección de detalles de error
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de recopilación de detalles del error.
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL Detalles del error] Tipo de datos de colección

[!UICONTROL Detalles del error] La colección es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles del error. Utilice el tipo de datos de colección [!UICONTROL Detalles del error] para capturar los detalles del origen y la identificación del error. El ID de error identifica el error y el origen del error especifica si se origina desde el reproductor o desde un origen externo.

![Un diagrama del tipo de datos Información de detalles del error.](../images/data-types/error-details-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL ID de error] | `name` | cadena | No | ID de error. |
| [!UICONTROL Error de Source] | `source` | cadena | No | Origen del error. Enumerado: &quot;reproductor&quot;, &quot;externo&quot; con los significados respectivos. |

{style="table-layout:auto"}
