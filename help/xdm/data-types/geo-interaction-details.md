---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;señalización;detalles de interacción;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles de interacción geográfica
topic-legacy: overview
description: Este documento proporciona una descripción general del tipo de datos XDM Detalles de interacción geográfica .
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 4%

---

# [!UICONTROL Tipo de datos de ] detalles de interacción geográfica

[!UICONTROL Los ] detalles de interacción geográfica son un tipo de datos XDM estándar que describe el estado actual de inclusión en un área definida geográficamente.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Describe la forma geográfica del área con la que se interactúa. Este campo puede describir un cuadro, un círculo o un polígono. |
| `deviceGeoAccuracy` | Duplicada | Precisión del dispositivo o mecanismo de medición geográfica, medida en metros. |
| `distanceToCenter` | Duplicada | Distancia al centro de la geografía en el caso de un círculo geográfico, medida en metros. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
