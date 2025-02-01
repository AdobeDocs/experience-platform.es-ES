---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;fullName;xdm:fullName;nombre de persona;nombre;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos del nombre de persona
description: Obtenga información sobre el tipo de datos XDM de nombre de persona.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 6%

---

# [!UICONTROL Tipo de datos del nombre de la persona]

[!UICONTROL Nombre de persona] es un tipo de datos XDM estándar que describe el nombre completo de una persona. Dado que las convenciones para las estructuras de nombres difieren ampliamente entre idiomas y referencias culturales, los nombres siempre deben modelarse con este tipo de datos.

Además, el tipo de datos proporciona una serie de propiedades opcionales que se pueden utilizar en situaciones que requieren utilizar solo un fragmento del nombre completo, como la creación de un saludo formal o informal.

![](../images/data-types/person-name.png){width=500}

| Propiedad | Descripción |
| --- | --- |
| `courtesyTitle` | Una abreviatura del título, el honor o el saludo de una persona (como `Mr.`, `Miss.` o `Dr.`). |
| `firstName` | El primer segmento del nombre en el orden de escritura más comúnmente aceptado en el idioma del nombre. |
| `fullName` | El nombre completo de la persona, en el orden de escritura más comúnmente aceptado en el idioma del nombre. |
| `lastName` | El último segmento del nombre en el orden de escritura más comúnmente aceptado en el idioma del nombre. |
| `middleName` | Segundos nombres, nombres alternativos o adicionales que se ponen entre el primer nombre y los apellidos. |
| `suffix` | Un grupo de cartas proporcionadas después del nombre de una persona para proporcionar información adicional (como `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, etc.). |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos del nombre de la persona, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
