---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;geografía;forma geográfica;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de forma geográfica
description: Obtenga información sobre el tipo de datos XDM de forma geográfica.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# Tipo de datos [!UICONTROL Forma geográfica]

[!UICONTROL Forma geográfica] es un tipo de datos XDM estándar que describe la forma de un área geográfica. Este tipo de datos se basa en la especificación pública documentada en [schema.org](https://schema.org/GeoShape).

![](../images/data-types/geo-shape.png){width=500}

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.box` | Matriz de [[!UICONTROL coordenadas geográficas]](./geo-coordinates.md) | Describe un área geográfica delimitada por un rectángulo formado por dos coordenadas. La primera coordenada es la esquina inferior del rectángulo y la segunda coordenada es la esquina superior. |
| `_schema.circle` | Matriz de [[!UICONTROL coordenadas geográficas]](./geo-coordinates.md) | Describe una región circular con un radio específico centrado en una coordenada geográfica. |
| `_schema.polygon` | [[!UICONTROL Círculo geográfico]](./geo-circle.md) | Una serie de cuatro o más coordenadas donde la primera y la última coordenada son idénticas. |
| `_schema.description` | Cadena | Una descripción de lo que está definiendo la forma. |
| `_schema.elevation` | Duplicada | La elevación específica o mínima de la forma. Este valor se ajusta a los datos [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. En combinación con `ceiling`, esta propiedad se puede utilizar para expresar un cuadro delimitador tridimensional para una ubicación. |
| `_id` | Cadena | Un identificador único generado por el sistema para la forma. |
| `ceiling` | Duplicada | La elevación máxima de la forma. Esta propiedad sólo es válida cuando se utiliza en combinación con `elevation`. El valor se ajusta a los datos [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. En combinación con `elevation`, esta propiedad se puede utilizar para expresar un cuadro delimitador tridimensional para una ubicación. |
