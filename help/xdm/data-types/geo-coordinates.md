---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;geo;coordenadas;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de coordenadas geográficas
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Coordenadas geográficas.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---


# [!UICONTROL Tipo ] de datos de coordenadas geográficas

[!UICONTROL Geo ] Coordinatesis es un tipo de datos XDM estándar que describe las coordenadas geográficas de un lugar. Este tipo de datos se basa en la especificación pública documentada en [esquema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.description` | Cadena | Descripción de lo que identifican las coordenadas. |
| `_schema.elevation` | Duplicada | Elevación específica de la coordenada definida. El valor debe cumplir la referencia [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_schema.latitude` | Duplicada | Coordenada vertical firmada del punto geográfico. |
| `_schema.longitude` | Duplicada | Coordenada horizontal firmada del punto geográfico. |
| `_id` | Cadena | ID única generada por el sistema para las coordenadas. |
