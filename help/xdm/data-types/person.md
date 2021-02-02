---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;persona;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de persona
topic: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias personales (XDM).
translation-type: tm+mt
source-git-commit: 194b604d4b23f2acfaa4243155b04a6793fb0727
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de datos personales

 Persona es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe a una persona individual. Este tipo de datos puede representar a una persona que actúa en diferentes funciones, como cliente, contacto o propietario.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `name` | [[!UICONTROL Nombre de la persona]](./person-name.md) | Describe detalles sobre el nombre completo de la persona. |
| `birthDate` | Fecha | La fecha completa en que nació una persona. El formato de fecha (sin tiempo) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `birthDayAndMonth` | Cadena | El día y mes en que nació una persona, en el formato MM-DD. Este campo debe utilizarse cuando se conozca el día y mes del nacimiento de una persona, pero no el año. El formato de esta propiedad debe cumplir con esta expresión regular `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Número entero | El año en que nació una persona, incluido el siglo (por ejemplo, `1983`). Este campo debe utilizarse cuando sólo se conozca la edad de la persona y no la fecha de nacimiento completa. Este valor debe estar entre 1 y 32767. |
| `gender` | Cadena | La identidad de género de la persona. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> El valor predeterminado para este valor es `not_specified`. |
| `maritalStatus` | Cadena | Describe la relación de una persona con otra importante. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> El valor predeterminado para este valor es `not_specified`. |
| `nationality` | Cadena | La relación jurídica entre una persona y su estado representado utilizando el código ISO 3166-1 Alpha-2. El formato de esta propiedad debe cumplir con esta expresión regular `^[A-Z]{2}$`. |
| `taxId` | Cadena | El impuesto o la identificación fiscal de la persona, como el número de identificación fiscal del contribuyente (TIN) en los Estados Unidos o el certificado de identificación fiscal (CIF/NIF) en España. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)