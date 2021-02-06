---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;poi;interacción;punto de interés;punto de interés;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de interacción del punto de interés
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de punto de interés.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# [!UICONTROL Tipo de ] datos de interacción de puntos de interés

[!UICONTROL La ] interacción de puntos de interés es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica información de identidad a las aplicaciones móviles a medida que los dispositivos móviles se encuentran dentro del rango.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Detalles del punto de interés]](./poi-details.md) | Describe los detalles del punto de interés que provocó el evento. |
| `poiEntries` | Objeto | Describe el número de veces que una persona ha ingresado al punto de interés. Contiene dos propiedades: <ul><li>`id`:: Un identificador único para la medida.</li><li>`value`:: Valor cuantificable de la medida.</li></ul> |
| `poiExits` | Objeto | Describe el número de veces que una persona ha salido del punto de interés. Contiene dos propiedades: <ul><li>`id`:: Un identificador único para la medida.</li><li>`value`:: Valor cuantificable de la medida.</li></ul> |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
