---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de círculo geográfico
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de círculo geográfico.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 4%

---


# [!UICONTROL Tipo de datos de círculo] geográfico

[!UICONTROL Geo Circle] es un tipo de datos XDM estándar que describe la región geográfica circular, dado un radio particular centrado en un conjunto específico de coordenadas. Este tipo de datos se basa en la especificación pública documentada en [esquema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Describe las coordenadas geográficas del centro del círculo. |
| `_schema.description` | Cadena | Descripción de lo que contiene el círculo. |
| `_schema.radius` | Duplicada | Longitud del radio del círculo. Este valor se ajusta a la referencia [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_id` | Cadena | ID única generada por el sistema para el círculo. |
