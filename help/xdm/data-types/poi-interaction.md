---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;poi;interacción;punto de interés;punto de interés;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de interacción del punto de interés
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de interacción de puntos de interés.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---

# [!UICONTROL Point of interest interaction] tipo de datos

[!UICONTROL Point of interest interaction] es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica la información de identidad a las aplicaciones móviles a medida que los dispositivos móviles se encuentran dentro del rango.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | Describe los detalles del punto de interés que provocó el evento. |
| `poiEntries` | Objeto | Describe el número de veces que una persona ha ingresado al punto de interés. Contiene dos propiedades: <ul><li>`id`: Identificador único de la medida.</li><li>`value`: El valor cuantificable de la medida.</li></ul> |
| `poiExits` | Objeto | Describe el número de veces que una persona ha salido del punto de interés. Contiene dos propiedades: <ul><li>`id`: Identificador único de la medida.</li><li>`value`: El valor cuantificable de la medida.</li></ul> |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
