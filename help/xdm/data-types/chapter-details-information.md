---
title: Detalles del capítulo Información Tipo de datos
description: Obtenga información sobre los detalles del capítulo del tipo de datos del Modelo de datos de experiencia (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 6%

---

# [!UICONTROL Información de detalles del capítulo] tipo de datos

[!UICONTROL Información de detalles del capítulo] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe varios atributos relacionados con capítulos o segmentos dentro del contenido de medios. Utilice el [!UICONTROL Información de detalles del capítulo] tipo de datos para capturar detalles como el nombre del capítulo, la duración, la posición, el ID, el estado de reproducción (iniciada/completada) y el tiempo empleado en cada capítulo.

![Diagrama del tipo de datos Información de detalles del capítulo.](../images/data-types/chapter-details-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL Nombre del capítulo] | `friendlyName` | string | El nombre del capítulo y/o segmento. |
| [!UICONTROL Duración O Longitud Del Capítulo] | `length` | entero | **Requerido** La duración del capítulo en segundos. |
| [!UICONTROL Desplazamiento de capítulo] | `offset` | entero | **Requerido** El desplazamiento del capítulo dentro del contenido (en segundos) desde el inicio. |
| [!UICONTROL Posición del capítulo] | `index` | entero | **Requerido** La posición (índice, entero) del capítulo dentro del contenido. |
| [!UICONTROL ID de capítulo] | `ID` | string | El ID del capítulo generado automáticamente. |
| [!UICONTROL Capítulo iniciado] | `isStarted` | Booleano | Si el capítulo ha comenzado. |
| [!UICONTROL Capítulo completado] | `isCompleted` | Booleano | Si el capítulo se ha completado. |
| [!UICONTROL Tiempo de reproducción del capítulo] | `timePlayed` | entero | El tiempo empleado en el capítulo, en segundos. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)
