---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;interacción web;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de interacción Web
topic: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias (XDM) de interacción con la Web.
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 3%

---


# [!UICONTROL Tipo ] de datos de interacción Web

[!UICONTROL La ] interacción web es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe la información sobre las interacciones que se produjeron en una página web después de que se completó la carga de la página inicial. Está diseñado para registrar interacciones en aplicaciones web enriquecidas que no déclencheur una carga de página nueva, como aplicaciones web de una sola página (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Medida]](./measure.md) | Medición que rastrea el clic de un vínculo Web. |
| `URL` | Cadena | El vínculo o la dirección URL reales que se utilizan para esta interacción web. |
| `name` | Cadena | Nombre normativo utilizado para este vínculo web. Se utiliza con fines de clasificación. |
| `type` | Cadena | Tipo de vínculo. Esta propiedad debe ser igual a uno de los siguientes valores de enumeración: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)