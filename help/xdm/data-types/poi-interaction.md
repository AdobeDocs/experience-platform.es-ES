---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;esquemas;poi;interacción;punto de interés;punto de interés;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de interacción del punto de interés
description: Este documento proporciona información general sobre el tipo de datos XDM de interacción de punto de interés.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---

# [!UICONTROL Interacción del punto de interés] tipo de datos

[!UICONTROL Interacción del punto de interés] es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica información de identidad a aplicaciones móviles a medida que los dispositivos móviles se encuentran dentro del alcance.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Detalles del punto de interés]](./poi-details.md) | Describe los detalles del punto de interés que provocó el evento. |
| `poiEntries` | Objeto | Describe la cantidad de veces que una persona ha ingresado al PDI. Contiene dos propiedades: <ul><li>`id`: Un identificador único para la medida.</li><li>`value`: el valor cuantificable de la medida.</li></ul> |
| `poiExits` | Objeto | Describe la cantidad de veces que una persona ha salido del PDI. Contiene dos propiedades: <ul><li>`id`: Un identificador único para la medida.</li><li>`value`: el valor cuantificable de la medida.</li></ul> |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
