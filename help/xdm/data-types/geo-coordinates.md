---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;geografía;coordenadas;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de coordenadas geográficas
description: Obtenga información sobre el tipo de datos XDM de coordenadas geográficas.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 7%

---

# [!UICONTROL Coordenadas geográficas] tipo de datos

[!UICONTROL Coordenadas geográficas] es un tipo de datos XDM estándar que describe las coordenadas geográficas de un lugar. Este tipo de datos se basa en la especificación pública documentada en [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema.description` | Cadena | Una descripción de lo que identifican las coordenadas. |
| `_schema.elevation` | Doble | La elevación específica de la coordenada definida. El valor debe ajustarse a [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) y se mide en metros. |
| `_schema.latitude` | Doble | La coordenada vertical firmada del punto geográfico. |
| `_schema.longitude` | Doble | La coordenada horizontal firmada del punto geográfico. |
| `_id` | Cadena | ID único generado por el sistema para las coordenadas. |
