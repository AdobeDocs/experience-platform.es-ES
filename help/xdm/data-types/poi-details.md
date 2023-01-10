---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;poi;detalles de puntos de interés;detalles de puntos de interés;tipo de datos;tipo de datos;tipo de datos; tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles del punto de interés
description: Este documento proporciona información general sobre el tipo de datos XDM de Detalles del punto de interés.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 5%

---

# [!UICONTROL Detalles del punto de interés] tipo de datos

[!UICONTROL Detalles del punto de interés] es un tipo de datos XDM estándar que describe los datos geográficos donde se observó un evento.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Señalización]](./beacon.md) | Describe los detalles de señalización activos para la interacción de puntos de interés. |
| `geoInteractionDetails` | [[!UICONTROL Detalles de interacción geográfica]](./geo-interaction-details.md) | Describe los detalles geográficos activos para la interacción de puntos de interés. |
| `category` | Cadena | Una categoría general asignada para organizar los puntos de interés por el administrador de definiciones de puntos de interés. |
| `distanceToPOICenter` | Doble | La distancia estimada del centro de puntos de interés en metros. |
| `locatingType` | Cadena | Mecanismo utilizado para determinar la ubicación. Los valores aceptados incluyen: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Cadena | Nombre dado al punto de interés. |
| `poiID` | Cadena | Identificador único del punto de interés. |
| `type` | Cadena | Tipo general del punto de interés utilizando un esquema de escritura seleccionado por el administrador de las definiciones de punto de interés. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
