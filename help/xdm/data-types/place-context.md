---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;contexto;contextoUbicación;contexto;tipoDeDatos;tipoDeDatos;tipoDeDatos;
solution: Experience Platform
title: Colocar tipo de datos de contexto
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de contexto de colocación.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---


# [!UICONTROL Colocar tipo ] de datos de contexto

[!UICONTROL Colocar ] contextos es un tipo de datos XDM estándar que describe la ubicación de un evento observado, incluyendo información de puntos de interés y coordenadas geográficas.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interacción con puntos de interés]](./poi-interaction.md) | Describe detalles sobre la interacción entre puntos de interés (POI). |
| `activePOIs` | Matriz de [[!UICONTROL detalles del punto de interés]](./poi-details.md) | Describe los puntos de interés que causaron el evento. |
| `geo` | [[!UICONTROL Ubicación geográfica]](./geo.md) | Describe la ubicación geográfica en la que se entregó la experiencia. |
| `localTime` | DateTime | Marca de hora en formato [RFC 3339](https://tools.ietf.org/html/rfc3339), que indica la hora local que se utiliza con un desplazamiento de zona horaria declarado. El patrón de formato es `yyyy-MM-dd'T'HH:mm:ssXXX` (por ejemplo, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Número entero | El desplazamiento de la zona horaria local actual en minutos desde UTC para el valor `localTime`. Esto debería incluir el desplazamiento actual del horario de verano, si procede. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)