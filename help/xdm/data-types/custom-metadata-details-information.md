---
title: Tipo de datos de información de detalles de metadatos personalizados
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de información de detalles de metadatos personalizados.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# [!UICONTROL Información de detalles de metadatos personalizados] tipo de datos

[!UICONTROL Información de detalles de metadatos personalizados] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que define una estructura para almacenar metadatos personalizados. Utilice el [!UICONTROL Información de detalles de metadatos personalizados] tipo de datos para capturar detalles como el nombre y el valor de los metadatos personalizados asociados al contenido o a las interacciones.

![Diagrama del tipo de datos Información de detalles de metadatos personalizados.](../images/data-types/custom-metadata-details-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nombre del campo de metadatos personalizado] | `name` | string | Nombre del campo personalizado. |
| [!UICONTROL Valor del campo de metadatos personalizado] | `value` | string | El valor del campo personalizado. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
