---
title: Tipo de datos de colección de detalles de error
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de recopilación de detalles del error.
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 10%

---

# [!UICONTROL Error Details] tipo de datos de colección

La colección [!UICONTROL Error Details] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles del error. Utilice el tipo de datos de colección [!UICONTROL Error Details] para capturar los detalles del origen y la identificación del error. El ID de error identifica el error y el origen del error especifica si se origina desde el reproductor o desde un origen externo.

![Un diagrama del tipo de datos Información de detalles del error.](../images/data-types/error-details-collection.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | cadena | No | ID de error. |
| [!UICONTROL Error Source] | `source` | cadena | No | Origen del error. Enumerado: &quot;reproductor&quot;, &quot;externo&quot; con los significados respectivos. |

{style="table-layout:auto"}
