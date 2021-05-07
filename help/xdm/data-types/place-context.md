---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;contexto;contexto;contextoUbicación;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Colocar tipo de datos de contexto
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de contexto de ubicación.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 4%

---

# [!UICONTROL Place context] tipo de datos

[!UICONTROL Place context] es un tipo de datos XDM estándar que describe la ubicación de un evento observado, incluida la información del punto de interés y las coordenadas geográficas.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Describe detalles sobre la interacción de puntos de interés (POI). |
| `activePOIs` | Matriz de [[!UICONTROL Point of interest details]](./poi-details.md) | Describe los puntos de interés que provocaron el evento. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Describe la ubicación geográfica en la que se entregó la experiencia. |
| `localTime` | DateTime | Marca de tiempo en formato [RFC 3339](https://tools.ietf.org/html/rfc3339), que indica la hora local que se utiliza con un desplazamiento de zona horaria declarado. El patrón de formato es `yyyy-MM-dd'T'HH:mm:ssXXX` (por ejemplo, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Número entero | El desplazamiento de zona horaria local actual en minutos desde UTC para el valor `localTime`. Esto debería incluir el desplazamiento actual del horario de verano, si corresponde. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
