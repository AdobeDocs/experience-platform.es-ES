---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;contexto;contexto;contextoUbicación;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Colocar tipo de datos de contexto
description: Este documento proporciona información general sobre el tipo de datos XDM de contexto de ubicación.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---

# [!UICONTROL Contexto del lugar] tipo de datos

[!UICONTROL Contexto del lugar] es un tipo de datos XDM estándar que describe la ubicación de un evento observado, incluida la información del punto de interés y las coordenadas geográficas.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interacción con puntos de interés]](./poi-interaction.md) | Describe detalles sobre la interacción de puntos de interés (POI). |
| `activePOIs` | Matriz de [[!UICONTROL Detalles del punto de interés]](./poi-details.md) | Describe los puntos de interés que provocaron el evento. |
| `geo` | [[!UICONTROL Ubicación geográfica]](./geo.md) | Describe la ubicación geográfica en la que se entregó la experiencia. |
| `localTime` | DateTime | Una marca de tiempo en [RFC 3339](https://tools.ietf.org/html/rfc3339) , indicando la hora local que utiliza con un desplazamiento de zona horaria declarado. El patrón de formato es `yyyy-MM-dd'T'HH:mm:ssXXX` (por ejemplo, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Número entero | El desplazamiento de zona horaria local actual en minutos desde UTC para la variable `localTime` valor. Esto debería incluir el desplazamiento actual del horario de verano, si corresponde. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
