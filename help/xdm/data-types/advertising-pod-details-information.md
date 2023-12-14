---
title: Información de detalles de Advertising Pod Tipo de datos
description: Obtenga información sobre el tipo de datos del modelo de datos de experiencia (XDM) de detalles de Advertising Pod.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# [!UICONTROL Información de detalles de Advertising Pod] tipo de datos

[!UICONTROL Información de detalles de Advertising Pod] es un tipo de datos estándar del Modelo de datos de experiencia (XDM). Define una secuencia o grupo de anuncios que normalmente se reproducen sucesivamente durante los saltos de contenido. Utilice el [!UICONTROL Información de detalles de Advertising Pod] Tipo de datos para capturar detalles como el ID de pausa publicitaria, un nombre descriptivo para la pausa publicitaria, el índice de anuncios dentro de la pausa publicitaria y el desplazamiento de la pausa publicitaria dentro de la cronología del contenido en segundos.

![Diagrama del tipo de datos Información de detalles del Advertising Pod.](../images/data-types/advertising-pod-details-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID de desglose de anuncios] | `ID` | string | El ID de la pausa publicitaria. |
| [!UICONTROL Nombre descriptivo del pod] | `friendlyName` | string | El nombre fácilmente comprensible de la pausa publicitaria. |
| [!UICONTROL Posición del anuncio en la secuencia] | `index` | entero | Índice de la publicidad dentro del inicio de pausa publicitaria principal. |
| [!UICONTROL Desplazamiento de pod] | `offset` | entero | **Requerido** El desplazamiento del desglose de anuncios dentro del contenido, en segundos. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
