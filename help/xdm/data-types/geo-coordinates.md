---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos Coordenadas geográficas
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Coordenadas geográficas.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---


# [!UICONTROL Tipo de datos Coordenadas] geográficas

[!UICONTROL Coordenadas] geográficas es un tipo de datos XDM estándar que describe las coordenadas geográficas de un lugar. Este tipo de datos se basa en la especificación pública documentada en [esquema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.description` | Cadena | Descripción de lo que identifican las coordenadas. |
| `_schema.elevation` | Duplicada | Elevación específica de la coordenada definida. El valor debe ajustarse a la referencia [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_schema.latitude` | Duplicada | Coordenada vertical firmada del punto geográfico. |
| `_schema.longitude` | Duplicada | Coordenada horizontal firmada del punto geográfico. |
| `_id` | Cadena | ID única generada por el sistema para las coordenadas. |
