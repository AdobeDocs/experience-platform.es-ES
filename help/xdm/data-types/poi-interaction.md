---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;interaction;point of interest;point-of-interest;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de interacción con puntos de interés
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de punto de interés.
translation-type: tm+mt
source-git-commit: 032adc72db7f094b268f14e8f7d48810830a84e4
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 1%

---


# [!UICONTROL Tipo de datos de interacción] del punto de interés

[!UICONTROL La interacción] del punto de interés es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica información de identidad a las aplicaciones móviles a medida que los dispositivos móviles se encuentran dentro del rango.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Detalles del punto de interés]](./poi-details.md) | Describe los detalles del punto de interés que provocó el evento. |
| `poiEntries` | Objeto | Describe el número de veces que una persona ha ingresado al punto de interés. Contiene dos propiedades: <ul><li>`id`:: Un identificador único para la medida.</li><li>`value`:: Valor cuantificable de la medida.</li></ul> |
| `poiExits` | Objeto | Describe el número de veces que una persona ha salido del punto de interés. Contiene dos propiedades: <ul><li>`id`:: Un identificador único para la medida.</li><li>`value`:: Valor cuantificable de la medida.</li></ul> |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
