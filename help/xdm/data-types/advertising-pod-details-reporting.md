---
title: Tipo de datos del informe Detalles de Advertising Pod
description: Obtenga información sobre el tipo de datos del modelo de datos de experiencia (XDM) de creación de informes de detalles de secuencia de Advertising.
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# [!UICONTROL Informes de detalles de Advertising Pod] tipo de datos

[!UICONTROL Informes de detalles de Advertising Pod] es un tipo de datos estándar del Modelo de datos de experiencia (XDM). Define una secuencia o grupo de anuncios que normalmente se reproducen sucesivamente durante los saltos de contenido. Use el tipo de datos [!UICONTROL Informes de detalles de Advertising Pod] para capturar detalles como el ID de la pausa publicitaria, un nombre descriptivo para la pausa publicitaria, el índice de anuncios dentro de la pausa publicitaria y el desplazamiento de la pausa publicitaria dentro de la cronología del contenido en segundos.

![Un diagrama del tipo de datos de informes de detalles de Advertising Pod.](../images/data-types/advertising-pod-details-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID de desglose de anuncios] | `ID` | cadena | El ID de la pausa publicitaria. |
| [!UICONTROL Nombre descriptivo de la secuencia] | `friendlyName` | cadena | El nombre fácilmente comprensible de la pausa publicitaria. |
| [!UICONTROL Posición del anuncio en la secuencia] | `index` | entero | Índice de la publicidad dentro del inicio de pausa publicitaria principal. |
| [!UICONTROL Desplazamiento de secuencia] | `offset` | entero | **Obligatorio** El desplazamiento del desglose de anuncios dentro del contenido, en segundos. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
