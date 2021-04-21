---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;geografía;coordenadas;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de coordenadas geográficas
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Coordenadas geográficamente.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

# [!UICONTROL Geo Coordinates] tipo de datos

[!UICONTROL Geo Coordinates] es un tipo de datos XDM estándar que describe las coordenadas geográficas de un lugar. Este tipo de datos se basa en la especificación pública documentada en [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.description` | Cadena | Descripción de lo que identifican las coordenadas. |
| `_schema.elevation` | Duplicada | Elevación específica de la coordenada definida. El valor debe ajustarse a la referencia [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_schema.latitude` | Duplicada | Coordenada vertical firmada del punto geográfico. |
| `_schema.longitude` | Duplicada | Coordenada horizontal firmada del punto geográfico. |
| `_id` | Cadena | ID único generado por el sistema para las coordenadas. |
