---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;geo;círculo;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de círculo geográfico
description: Este documento proporciona información general sobre el tipo de datos XDM de Círculo geográfico.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL Círculo geográfico] tipo de datos

[!UICONTROL Círculo geográfico] es un tipo de datos XDM estándar que describe una región geográfica circular, dado un radio en particular centrado en un conjunto específico de coordenadas. Este tipo de datos se basa en la especificación pública documentada en [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Describe las coordenadas geográficas del centro del círculo. |
| `_schema.description` | Cadena | Descripción del contenido del círculo. |
| `_schema.radius` | Doble | Longitud del radio del círculo. Este valor se ajusta a la variable [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_id` | Cadena | Un ID único generado por el sistema para el círculo. |
