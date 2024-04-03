---
title: Tipo de datos de colección de detalles de error
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de recopilación de detalles del error.
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Detalles del error] Tipo de datos de colección

[!UICONTROL Detalles del error] La recopilación es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles del error. Utilice el [!UICONTROL Detalles del error] Tipo de datos de recopilación para capturar los detalles del origen y la identificación del error. El ID de error identifica el error y el origen del error especifica si se origina desde el reproductor o desde un origen externo.

![Diagrama del tipo de datos Información de detalles del error.](../images/data-types/error-details-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL ID de error] | `name` | string | No | ID de error. |
| [!UICONTROL Origen de error] | `source` | string | No | Origen del error. Enumerado: &quot;reproductor&quot;, &quot;externo&quot; con los significados respectivos. |

{style="table-layout:auto"}
