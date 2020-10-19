---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos geográficos
topic: overview
description: Este documento proporciona información general sobre el tipo de datos Geo XDM.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---


# [!UICONTROL Tipo de datos geográficos]

[!UICONTROL Geo] es un tipo de datos XDM estándar que describe el área geográfica donde se observó un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Describe las coordenadas geográficas de un lugar. |
| `_id` | Cadena | ID única generada por el sistema para las coordenadas. |
| `city` | Cadena | El nombre de la ciudad. |
| `countryCode` | Cadena | Código alfa-2 <a href="https://datahub.io/core/country-list">de dos caracteres</a> ISO 3166-1 para el país. |
| `dmaID` | Número entero | La investigación de medios Nielsen designó área de mercado. |
| `msaID` | Número entero | Área estadística metropolitana en los Estados Unidos donde se produjo la observación. |
| `postalCode` | Cadena | Código postal de la ubicación. Los códigos postales no están disponibles para todos los países. En algunos países, esto solo contendrá parte del código postal. |
| `stateProvince` | Cadena | El estado o la parte provincial de la observación. El formato sigue la norma [ISO 3166-2 (país y subdivisión)](http://www.unece.org/cefact/locode/subdivisions.html) . |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)