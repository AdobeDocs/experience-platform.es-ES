---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;geo;círculo;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de círculo geográfico
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de Círculo geográfico.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# [!UICONTROL Geo Circle] tipo de datos

[!UICONTROL Geo Circle] es un tipo de datos XDM estándar que describe una región geográfica circular, dado un radio en particular centrado en un conjunto específico de coordenadas. Este tipo de datos se basa en la especificación pública documentada en [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Describe las coordenadas geográficas del centro del círculo. |
| `_schema.description` | Cadena | Descripción del contenido del círculo. |
| `_schema.radius` | Duplicada | Longitud del radio del círculo. Este valor se ajusta a la referencia [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_id` | Cadena | Un ID único generado por el sistema para el círculo. |
