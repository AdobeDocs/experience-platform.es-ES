---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;poi;detalles del poi;punto de interés;detalles del punto de interés;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles del punto de interés
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de Detalles del punto de interés.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---


# [!UICONTROL Tipo de datos de ] detalles del punto de interés

[!UICONTROL Los ] detalles del punto de interés son un tipo de datos XDM estándar que describe los datos geográficos en los que se observó un evento.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Señalización]](./beacon.md) | Describe los detalles de señalización activos para la interacción de puntos de interés. |
| `geoInteractionDetails` | [[!UICONTROL Detalles de interacción geográfica]](./geo-interaction-details.md) | Describe los detalles geográficos activos para la interacción de puntos de interés. |
| `category` | Cadena | Categoría general asignada para organizar los puntos de interés por el administrador de definiciones de puntos de interés. |
| `distanceToPOICenter` | Duplicada | La distancia estimada desde el centro del punto de interés en metros. |
| `locatingType` | Cadena | Mecanismo utilizado para determinar la ubicación. Los valores aceptados incluyen: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Cadena | Un nombre dado al POI. |
| `poiID` | Cadena | Identificador único del punto de interés. |
| `type` | Cadena | Tipo general del punto de interés mediante un esquema de escritura seleccionado por el administrador de las definiciones de puntos de interés. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)