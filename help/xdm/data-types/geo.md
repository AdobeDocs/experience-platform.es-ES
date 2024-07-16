---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;geografía;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos geográficos
description: Obtenga información sobre el tipo de datos XDM geográfico.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 35%

---

# [!UICONTROL Tipo de datos geográfico]

[!UICONTROL Geo] es un tipo de datos XDM estándar que describe el área geográfica donde se observó un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Describe las coordenadas geográficas de un lugar. |
| `_id` | Cadena | ID único generado por el sistema para las coordenadas. |
| `city` | Cadena | El nombre de la ciudad. |
| `countryCode` | Cadena | El código de dos caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> del país. |
| `dmaID` | Entero | El área de mercado designada por la investigación de medios de Nielsen. |
| `msaID` | Entero | El área estadística metropolitana de los Estados Unidos donde ocurrió la observación. |
| `postalCode` | Cadena | El código postal de la ubicación. Los códigos postales no están disponibles en todos los países. En algunos países, solo se usa una parte del código postal. |
| `stateProvince` | Cadena | Estado o parte de provincia de la observación. El formato sigue el estándar [ISO 3166-2 (país y subdivisión)](https://www.unece.org/cefact/locode/subdivisions.html). |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
