---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de nombre de persona
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM Nombre de persona.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# [!UICONTROL Tipo de datos de nombre] de persona

[!UICONTROL Nombre] de persona es un tipo de datos XDM estándar que describe el nombre completo de una persona. Dado que las convenciones para estructuras de nombres difieren ampliamente entre idiomas y culturas, los nombres siempre deben modelarse usando este tipo de datos.

Además, el tipo de datos proporciona una serie de propiedades opcionales que se pueden utilizar en situaciones que requieran utilizar sólo un fragmento del nombre completo, como la creación de un saludo formal o informal.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Propiedad | Descripción |
| --- | --- |
| `courtesyTitle` | Abreviación del título, honorífico o saludo de una persona (como `Mr.`, `Miss.`o `Dr.`). |
| `firstName` | Primer segmento del nombre en el orden de escritura que se acepta con mayor frecuencia en el idioma del nombre. |
| `fullName` | Nombre completo de la persona, en el orden de escritura más comúnmente aceptado en el idioma del nombre. |
| `lastName` | Último segmento del nombre en el orden de escritura que se acepta con mayor frecuencia en el idioma del nombre. |
| `middleName` | Nombres medios, alternativos o adicionales proporcionados entre el nombre y el apellido. |
| `suffix` | Grupo de cartas proporcionadas después del nombre de una persona para proporcionar información adicional (por ejemplo `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, etc.). |

Para obtener más información sobre el tipo de datos de nombre de persona, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)