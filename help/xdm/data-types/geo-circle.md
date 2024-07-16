---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;geografía;círculo;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos del círculo geográfico
description: Obtenga información sobre el tipo de datos XDM de círculo geográfico.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 11%

---

# [!UICONTROL Círculo geográfico] tipo de datos

[!UICONTROL Círculo geográfico] es un tipo de datos XDM estándar que describe una región geográfica circular, dado un radio particular centrado en un conjunto específico de coordenadas. Este tipo de datos se basa en la especificación pública documentada en [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Describe las coordenadas geográficas del centro del círculo. |
| `_schema.description` | Cadena | Una descripción de lo que contiene el círculo. |
| `_schema.radius` | Duplicada | La longitud del radio del círculo. Este valor se ajusta a los datos [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_id` | Cadena | Un ID único generado por el sistema para el círculo. |
