---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: Mezcla de detalles demográficos
topic: overview
description: Este documento ofrece una visión general de la combinación de Detalles Demográficos.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 3%

---


# [!UICONTROL Mezcla de detalles] demográficos

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre las actualizaciones [de nombres de](../name-updates.md) mezcla para obtener más información.

[!UICONTROL Demographic Details] es una mezcla estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La combinación proporciona un `person` objeto de nivel raíz cuyos subcampos describen información sobre una persona individual.

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `person.name` | [Nombre de la persona](../../data-types/person-name.md) | Objeto cuyos subcampos describen varios elementos del nombre de una persona. |
| `person.birthDate` | Fecha | La fecha completa en la que nació una persona, en forma de una marca de tiempo ISO 8601. |
| `person.birthDayAndMonth` | Cadena | El día y mes en que nació una persona, en el formato MM-DD. Este campo debe utilizarse cuando se conozca el día y mes del nacimiento de una persona, pero no el año. |
| `person.birthYear` | Número entero | El año en que nació una persona, incluido el siglo (como 1989). Este campo debe utilizarse cuando sólo se conozca la edad de la persona, no la fecha de nacimiento completa. |
| `person.gender` | Cadena | La identidad de género de la persona. |
| `person.martialStatus` | Cadena | Describe la relación de una persona con otra importante. |
| `person.nationality` | Cadena | La relación jurídica entre una persona y su estado representado utilizando el código ISO 3166-1 Alpha-2. |
| `person.taxId` | Cadena | La identificación fiscal/fiscal de la persona, como el TIN en Estados Unidos o el CIF/NIF en España. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Esquema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)å completo