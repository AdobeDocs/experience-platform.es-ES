---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;campos;esquemas;esquemas;persona;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de persona
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de persona (XDM).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---

# Tipo de datos [!UICONTROL Persona]

[!UICONTROL Persona] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe a una persona individual. Este tipo de datos puede representar a una persona que tiene varias funciones, como cliente, contacto o propietario.

![imagen de persona](../images/data-types/person.PNG){width=500}

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `name` | [[!UICONTROL Nombre de persona]](./person-name.md) | Describe los detalles del nombre completo de la persona. |
| `birthDate` | Fecha | La fecha completa en la que nació una persona. El formato de fecha (sin hora) debe seguir el estándar [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `birthDayAndMonth` | Cadena | El día y el mes de nacimiento de una persona en formato MM-DD. Este campo debe usarse cuando se conoce el día y el mes del nacimiento de una persona, pero no el año. El formato de esta propiedad debe ajustarse a esta expresión regular `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Entero | El año en que nació una persona, incluido el siglo (por ejemplo, `1983`). Este campo debe usarse cuando solo se conoce la edad de la persona y no la fecha de nacimiento completa. Este valor debe estar entre 1 y 32767. |
| `gender` | Cadena | La identidad de género de la persona. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> El valor predeterminado es `not_specified`. |
| `maritalStatus` | Cadena | Describe la relación de una persona con su pareja. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> El valor predeterminado es `not_specified`. |
| `nationality` | Cadena | La relación jurídica entre una persona y su estado representada mediante el código ISO 3166-1 Alpha-2. El formato de esta propiedad debe ajustarse a esta expresión regular `^[A-Z]{2}$`. |
| `taxId` | Cadena | CIF El ID fiscal de la persona, como el Número de Identificación Fiscal (TIN) en EE. UU. o el Certificado de Identificación Fiscal (/NIF) en España. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
