---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;campos;esquemas;esquemas;señalización;detalles de interacción;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles de interacción geográfica
description: Obtenga información sobre el tipo de datos XDM de detalles de interacción geográfica.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 13%

---

# [!UICONTROL Detalles de interacción geográfica] tipo de datos

[!UICONTROL Detalles de interacción geográfica] es un tipo de datos XDM estándar que describe el estado actual de inclusión en un área definida geográficamente.

![](../images/data-types/geo-interaction-details.png){width=400}

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Describe la forma geográfica del área con la que se está interactuando. Este campo puede describir un cuadro, un círculo o un polígono. |
| `deviceGeoAccuracy` | Duplicada | La precisión del dispositivo o mecanismo de medición geográfica, medida en metros. |
| `distanceToCenter` | Duplicada | La distancia al centro del geo en el caso de un círculo geográfico, medida en metros. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
