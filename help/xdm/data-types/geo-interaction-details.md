---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;señalización;detalles de interacción;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles de interacción geográfica
topic-legacy: overview
description: Este documento proporciona una descripción general del tipo de datos XDM Detalles de interacción geográfica .
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 2%

---

# [!UICONTROL Geo interaction details] tipo de datos

[!UICONTROL Geo interaction details] es un tipo de datos XDM estándar que describe el estado actual de inclusión en un área definida geográficamente.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo Shape]](./geo-shape.md) | Describe la forma geográfica del área con la que se interactúa. Este campo puede describir un cuadro, un círculo o un polígono. |
| `deviceGeoAccuracy` | Duplicada | Precisión del dispositivo o mecanismo de medición geográfica, medida en metros. |
| `distanceToCenter` | Duplicada | Distancia al centro de la geografía en el caso de un círculo geográfico, medida en metros. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
