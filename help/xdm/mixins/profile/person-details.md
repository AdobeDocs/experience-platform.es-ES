---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;diseño de esquema;mezcla;mezcla;persona;detalles de persona;detalles de persona de perfil;persona;
solution: Experience Platform
title: Mezcla de detalles demográficos
topic-legacy: overview
description: Este documento ofrece una visión general de la mezcla de detalles demográficos.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: 87b638df8a3b27fb6df5dee60b57d817d5e34a80
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---

# [!UICONTROL Demographic Details] mixto

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../name-updates.md) para obtener más información.

[!UICONTROL Demographic Details] es una mezcla estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La mezcla proporciona un objeto `person` de nivel raíz, cuyos subcampos describen información sobre una persona individual.

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `person.name` | [Nombre de la persona](../../data-types/person-name.md) | Un objeto cuyos subcampos describen varios elementos del nombre de una persona. |
| `person.birthDate` | Fecha | La fecha completa en la que nació una persona, en forma de una marca de tiempo ISO 8601. |
| `person.birthDayAndMonth` | Cadena | El día y mes en que nació una persona, con el formato MM-DD. Este campo debe utilizarse cuando se conozca el día y el mes del nacimiento de una persona, pero no el año. |
| `person.birthYear` | Número entero | El año en que nació una persona, incluido el siglo (como 1989). Este campo debe utilizarse cuando solo se conozca la edad de la persona, no la fecha de nacimiento completa. |
| `person.gender` | Cadena | La identidad de género de la persona. |
| `person.martialStatus` | Cadena | Describe la relación de una persona con otra importante. |
| `person.nationality` | Cadena | La relación jurídica entre una persona y su estado representado utilizando el código ISO 3166-1 Alpha-2. |
| `person.taxId` | Cadena | La identificación fiscal/fiscal de la persona, como el TIN en EE.UU. o el CIF/NIF en España. |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
