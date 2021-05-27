---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;persona;detalles de persona;detalles de persona de perfil;persona;
solution: Experience Platform
title: Grupo de campos de esquema Detalles demográficos
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles demográficos .
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---


# [!UICONTROL Grupo de campos Demographic ] Detailsschema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL Demographic ] Detail es un grupo de campos de esquema estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). El grupo de campos proporciona un objeto `person` de nivel raíz cuyos subcampos describen información sobre una persona individual.

![](../../images/field-groups/demographic-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `person.name` | [Nombre de la persona](../../data-types/person-name.md) | Un objeto cuyos subcampos describen varios elementos del nombre de una persona. |
| `person.birthDate` | Fecha  | La fecha completa en la que nació una persona, en forma de una marca de tiempo ISO 8601. |
| `person.birthDayAndMonth` | Cadena | El día y mes en que nació una persona, con el formato MM-DD. Este campo debe utilizarse cuando se conozca el día y el mes del nacimiento de una persona, pero no el año. |
| `person.birthYear` | Número entero | El año en que nació una persona, incluido el siglo (como 1989). Este campo debe utilizarse cuando solo se conozca la edad de la persona, no la fecha de nacimiento completa. |
| `person.gender` | Cadena | La identidad de género de la persona. |
| `person.martialStatus` | Cadena | Describe la relación de una persona con otra importante. |
| `person.nationality` | Cadena | La relación jurídica entre una persona y su estado representado utilizando el código ISO 3166-1 Alpha-2. |
| `person.taxId` | Cadena | La identificación fiscal/fiscal de la persona, como el TIN en EE.UU. o el CIF/NIF en España. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)