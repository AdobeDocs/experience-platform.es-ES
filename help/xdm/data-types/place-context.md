---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;contexto de lugar;contexto de lugar;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de contexto del lugar
description: Este documento proporciona información general sobre el tipo de datos XDM de contexto de ubicación.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 4%

---

# [!UICONTROL Contexto del lugar] tipo de datos

[!UICONTROL Contexto del lugar] es un tipo de datos XDM estándar que describe la ubicación de un evento observado, incluida la información de puntos de interés y las coordenadas geográficas.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interacción del punto de interés]](./poi-interaction.md) | Describe los detalles de la interacción del punto de interés (PDI). |
| `activePOIs` | Matriz de [[!UICONTROL Detalles del punto de interés]](./poi-details.md) | Describe los puntos de interés que provocaron el evento. |
| `geo` | [[!UICONTROL Ubicación geográfica]](./geo.md) | Describe la ubicación geográfica donde se entregó la experiencia. |
| `localTime` | DateTime | Una marca de tiempo en [RFC 3339](https://tools.ietf.org/html/rfc3339) , que indica la hora local con un desplazamiento de zona horaria establecido. El patrón de formato es `yyyy-MM-dd'T'HH:mm:ssXXX` (por ejemplo, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Número entero | La diferencia de la zona horaria local actual en minutos UTC en el caso de `localTime` valor. Debe incluir la diferencia del horario de verano actual, si corresponde. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
