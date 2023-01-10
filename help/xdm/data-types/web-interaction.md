---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;interacción web;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de interacción web
description: Este documento proporciona una descripción general del tipo de datos de interacción web del Modelo de datos de experiencia (XDM).
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# [!UICONTROL Interacción web] tipo de datos

[!UICONTROL Interacción web] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe información sobre las interacciones que se produjeron en una página web después de completarse la carga inicial de la página. Está diseñado para registrar interacciones en aplicaciones web enriquecidas que no déclencheur una nueva carga de página, como aplicaciones web de una sola página (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Medida]](./measure.md) | Medición que realiza un seguimiento del clic en un vínculo web. |
| `URL` | Cadena | El vínculo o la URL reales utilizados para esta interacción web. |
| `name` | Cadena | Nombre normativo utilizado para este vínculo web. Se utiliza con fines de clasificación. |
| `type` | Cadena | El tipo de vínculo. Esta propiedad debe ser igual a uno de los siguientes valores de enumeración: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
