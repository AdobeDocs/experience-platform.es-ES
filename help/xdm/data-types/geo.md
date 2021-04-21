---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;geo;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos geográficos
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

---

# [!UICONTROL Geo] tipo de datos

[!UICONTROL Geo] es un tipo de datos XDM estándar que describe el área geográfica donde se observó un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Describe las coordenadas geográficas de un lugar. |
| `_id` | Cadena | ID único generado por el sistema para las coordenadas. |
| `city` | Cadena | El nombre de la ciudad. |
| `countryCode` | Cadena | Código <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> de dos caracteres para el país. |
| `dmaID` | Número entero | La investigación de medios de comunicación de Nielsen designó zona de mercado. |
| `msaID` | Número entero | El área estadística metropolitana en los Estados Unidos donde se produjo la observación. |
| `postalCode` | Cadena | El código postal de la ubicación. Los códigos postales no están disponibles para todos los países. En algunos países, esto solo contiene parte del código postal. |
| `stateProvince` | Cadena | Estado o provincia de la observación. El formato sigue el estándar [ISO 3166-2 (país y subdivisión)](http://www.unece.org/cefact/locode/subdivisions.html). |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)
