---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;geo;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos geográficos
description: Este documento proporciona información general sobre el tipo de datos Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL Geografía] tipo de datos

[!UICONTROL Geografía] es un tipo de datos XDM estándar que describe el área geográfica donde se observó un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Describe las coordenadas geográficas de un lugar. |
| `_id` | Cadena | ID único generado por el sistema para las coordenadas. |
| `city` | Cadena | El nombre de la ciudad. |
| `countryCode` | Cadena | Los dos caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> para el país. |
| `dmaID` | Número entero | La investigación de medios de comunicación de Nielsen designó zona de mercado. |
| `msaID` | Número entero | El área estadística metropolitana en los Estados Unidos donde se produjo la observación. |
| `postalCode` | Cadena | El código postal de la ubicación. Los códigos postales no están disponibles para todos los países. En algunos países, esto solo contiene parte del código postal. |
| `stateProvince` | Cadena | Estado o provincia de la observación. El formato sigue a la variable [ISO 3166-2 (país y subdivisión)](https://www.unece.org/cefact/locode/subdivisions.html) estándar. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
