---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;persona;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de persona
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias personales (XDM).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 4%

---

# [!UICONTROL Persona] tipo de datos

[!UICONTROL Persona] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe a una persona individual. Este tipo de datos puede representar a una persona que actúa en varias funciones, como un cliente, un contacto o un propietario.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `name` | [[!UICONTROL Nombre de la persona]](./person-name.md) | Describe detalles sobre el nombre completo de la persona. |
| `birthDate` | Fecha | La fecha completa de nacimiento de una persona. El formato de fecha (sin hora) debe seguir el [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) estándar. |
| `birthDayAndMonth` | Cadena | El día y mes en que nació una persona, con el formato MM-DD. Este campo debe utilizarse cuando se conozca el día y el mes del nacimiento de una persona, pero no el año. El formato de esta propiedad debe cumplir esta expresión regular `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Número entero | El año en que nació una persona, incluido el siglo (por ejemplo, `1983`). Este campo debe utilizarse cuando solo se conozca la edad de la persona y no la fecha de nacimiento completa. Este valor debe estar entre 1 y 32767. |
| `gender` | Cadena | La identidad de género de la persona. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> El valor predeterminado es `not_specified`. |
| `maritalStatus` | Cadena | Describe la relación de una persona con otra importante. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> El valor predeterminado es `not_specified`. |
| `nationality` | Cadena | La relación jurídica entre una persona y su estado representado utilizando el código ISO 3166-1 Alpha-2. El formato de esta propiedad debe cumplir esta expresión regular `^[A-Z]{2}$`. |
| `taxId` | Cadena | La identificación fiscal o fiscal de la persona, como el número de identificación fiscal del contribuyente (TIN) en los EE.UU. o el número de identificación fiscal del certificado (CIF/NIF) en España. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
