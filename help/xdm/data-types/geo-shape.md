---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de forma geográfica
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de forma geográfica.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---


# [!UICONTROL Tipo de datos de forma] geográfica

[!UICONTROL La forma] geográfica es un tipo de datos XDM estándar que describe la forma de un área geográfica. Este tipo de datos se basa en la especificación pública documentada en [esquema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.box` | Matriz de coordenadas [[!UICONTROL geográficas]](./geo-coordinates.md) | Describe un área geográfica delimitada por un rectángulo formado por dos coordenadas. La primera coordenada es la esquina inferior del rectángulo y la segunda es la esquina superior. |
| `_schema.circle` | Matriz de coordenadas [[!UICONTROL geográficas]](./geo-coordinates.md) | Describe una región circular con un radio específico centrado en una coordenada geográfica. |
| `_schema.polygon` | [[!UICONTROL Círculo geográfico]](./geo-circle.md) | Una serie de cuatro o más coordenadas en las que las coordenadas primera y final son idénticas. |
| `_schema.description` | Cadena | Descripción de lo que define la forma. |
| `_schema.elevation` | Duplicada | La elevación específica o mínima de la forma. Este valor se ajusta a la referencia [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. En combinación con `ceiling`, esta propiedad se puede utilizar para expresar un cuadro delimitador tridimensional para una ubicación. |
| `_id` | Cadena | Identificador único generado por el sistema para la forma. |
| `ceiling` | Duplicada | La elevación máxima de la forma. Esta propiedad solo es válida cuando se utiliza en combinación con `elevation`. El valor se ajusta a la referencia [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. En combinación con `elevation`, esta propiedad se puede utilizar para expresar un cuadro delimitador tridimensional para una ubicación. |
