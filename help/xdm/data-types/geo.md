---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;geo;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos geográficos
topic: overview
description: Este documento proporciona información general sobre el tipo de datos Geo XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de datos geográficos

 Geografía es un tipo de datos XDM estándar que describe el área geográfica donde se observó un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Describe las coordenadas geográficas de un lugar. |
| `_id` | Cadena | ID única generada por el sistema para las coordenadas. |
| `city` | Cadena | El nombre de la ciudad. |
| `countryCode` | Cadena | Código de dos caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> para el país. |
| `dmaID` | Número entero | La investigación de medios Nielsen designó área de mercado. |
| `msaID` | Número entero | Área estadística metropolitana en los Estados Unidos donde se produjo la observación. |
| `postalCode` | Cadena | Código postal de la ubicación. Los códigos postales no están disponibles para todos los países. En algunos países, esto solo contendrá parte del código postal. |
| `stateProvince` | Cadena | El estado o la parte provincial de la observación. El formato sigue el estándar [ISO 3166-2 (país y subdivisión)](http://www.unece.org/cefact/locode/subdivisions.html). |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)