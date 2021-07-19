---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;poi;interacción;punto de interés;punto de interés;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de interacción del punto de interés
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de interacción de puntos de interés.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 2%

---

# [!UICONTROL Tipo de datos de ] interacción de puntos de interés

[!UICONTROL La ] interacción del punto de interés es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica la información de identidad a las aplicaciones móviles a medida que los dispositivos móviles se encuentran dentro del intervalo.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Detalles del punto de interés]](./poi-details.md) | Describe los detalles del punto de interés que provocó el evento. |
| `poiEntries` | Objeto | Describe el número de veces que una persona ha ingresado al punto de interés. Contiene dos propiedades: <ul><li>`id`: Identificador único de la medida.</li><li>`value`: El valor cuantificable de la medida.</li></ul> |
| `poiExits` | Objeto | Describe el número de veces que una persona ha salido del punto de interés. Contiene dos propiedades: <ul><li>`id`: Identificador único de la medida.</li><li>`value`: El valor cuantificable de la medida.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
