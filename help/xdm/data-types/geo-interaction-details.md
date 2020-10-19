---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de detalles de interacción geográfica
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Detalles de interacción geográfica.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# [!UICONTROL Tipo de datos de detalles] de interacción geográfica

[!UICONTROL Detalles] de interacción geográfica es un tipo de datos XDM estándar que describe el estado actual de inclusión en un área definida geográficamente.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Describe la forma geográfica del área con la que se interactúa. Este campo puede describir un cuadro, un círculo o un polígono. |
| `deviceGeoAccuracy` | Duplicada | Precisión del dispositivo o mecanismo de medición geográfica, medida en metros. |
| `distanceToCenter` | Duplicada | Distancia al centro de la geografía en el caso de un círculo geográfico, medida en metros. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
