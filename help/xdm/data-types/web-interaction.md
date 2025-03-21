---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;interacción web;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de interacción web
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia (XDM) de interacción web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 10%

---

# [!UICONTROL Tipo de datos de interacción web]

[!UICONTROL Interacción web] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe información sobre las interacciones que se produjeron en una página web después de que se completara la carga inicial de la página. Está diseñado para registrar interacciones en aplicaciones web enriquecidas que no almacenan en déclencheur SPA una nueva carga de página, como aplicaciones web de una sola página ().

![imagen de interacción web](../images/data-types/web-interaction.PNG){width=500}

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Medida]](./measure.md) | Una medición que rastrea el clic de un vínculo web. |
| `URL` | Cadena | El vínculo o la URL real usada para esta interacción web. |
| `name` | Cadena | El nombre normativo utilizado para este vínculo web. Se utiliza con fines de clasificación. |
| `type` | Cadena | El tipo de vínculo. Esta propiedad debe ser igual a uno de los siguientes valores de enumeración: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
