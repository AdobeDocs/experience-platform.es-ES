---
title: Tipo de datos de información de detalles de error
description: Obtenga información sobre el tipo de datos de Información de detalles de error del Modelo de datos de experiencia (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 5%

---

# [!UICONTROL Información de detalles del error] tipo de datos

[!UICONTROL Información de detalles del error] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles del error. Utilice el [!UICONTROL Información de detalles del error] tipo de datos para capturar detalles de la fuente de error y la identificación. El ID de error identifica el error y el origen del error especifica si se origina desde el reproductor o desde un origen externo.

![Diagrama del tipo de datos Información de detalles del error.](../images/data-types/error-details-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL ID de error] | `name` | string | ID de error. |
| [!UICONTROL Origen de error] | `source` | string | Origen del error. Enumerado: &quot;reproductor&quot;, &quot;externo&quot; con los significados respectivos. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
