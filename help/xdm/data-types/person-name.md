---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;nombre completo;xdm:nombreCompleto;nombrePersona;nombre;tipoDeDatos;tipoDeDatos;TipoDeDatos;
solution: Experience Platform
title: Tipo de datos de nombre de persona
description: Este documento proporciona información general sobre el tipo de datos XDM Nombre de persona .
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# [!UICONTROL Nombre de la persona] tipo de datos

[!UICONTROL Nombre de la persona] es un tipo de datos XDM estándar que describe el nombre completo de una persona. Como las convenciones para las estructuras de nombres difieren ampliamente entre idiomas y culturas, los nombres siempre deben modelarse usando este tipo de datos.

Además, el tipo de datos proporciona varias propiedades opcionales que se pueden utilizar en situaciones en las que sea necesario utilizar solo un fragmento del nombre completo, como la creación de un saludo formal o informal.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Propiedad | Descripción |
| --- | --- |
| `courtesyTitle` | Abreviación del título, honorífico o saludo de una persona (por ejemplo, `Mr.`, `Miss.`o `Dr.`). |
| `firstName` | El primer segmento del nombre en el orden de escritura aceptado más comúnmente en el idioma del nombre. |
| `fullName` | El nombre completo de la persona, en el orden de escritura más comúnmente aceptado en el idioma del nombre. |
| `lastName` | El último segmento del nombre en el orden de escritura aceptado más comúnmente en el idioma del nombre. |
| `middleName` | Se han proporcionado nombres intermedios, alternativos o adicionales entre el nombre y los apellidos. |
| `suffix` | Grupo de cartas proporcionadas después del nombre de una persona para proporcionar información adicional (por ejemplo, `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, etc.). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos de nombre de persona, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
