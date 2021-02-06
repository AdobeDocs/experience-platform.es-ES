---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;señalización;detalles de interacción;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles de interacción geográfica
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Detalles de interacción geográfica.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---


# [!UICONTROL Tipo de datos de ] detalles de interacción geográfica

[!UICONTROL Los ] detalles de interacción geográfica son un tipo de datos XDM estándar que describe el estado actual de inclusión en un área definida geográficamente.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Describe la forma geográfica del área con la que se interactúa. Este campo puede describir un cuadro, un círculo o un polígono. |
| `deviceGeoAccuracy` | Duplicada | Precisión del dispositivo o mecanismo de medición geográfica, medida en metros. |
| `distanceToCenter` | Duplicada | Distancia al centro de la geografía en el caso de un círculo geográfico, medida en metros. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
