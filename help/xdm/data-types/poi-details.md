---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;esquemas;poi;detalles de poi;punto de interés;detalles de punto de interés;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de detalles del punto de interés
description: Obtenga información sobre el tipo de datos XDM de detalles del punto de interés.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 15%

---

# [!UICONTROL Detalles del punto de interés] tipo de datos

[!UICONTROL Detalles del punto de interés] es un tipo de datos XDM estándar que describe los datos geográficos donde se observó un evento.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Señalización]](./beacon.md) | Describe los detalles de la señalización activos para la interacción del PDI. |
| `geoInteractionDetails` | [[!UICONTROL Detalles de interacción geográfica]](./geo-interaction-details.md) | Describe los detalles geográficos activos para la interacción del PDI. |
| `category` | Cadena | Categoría general asignada para organizar puntos de interés por el administrador de definiciones de puntos de interés. |
| `distanceToPOICenter` | Duplicada | La distancia estimada desde el centro del PDI en metros. |
| `locatingType` | Cadena | Mecanismo utilizado para determinar la ubicación. Los valores aceptados incluyen: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Cadena | Un nombre dado al PDI. |
| `poiID` | Cadena | Un identificador único del PDI. |
| `type` | Cadena | El tipo general de PDI que usa un esquema de escritura seleccionado por el administrador de las definiciones de PDI. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
