---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;persona;detalles de persona;detalles de persona del perfil;persona;
solution: Experience Platform
title: Grupo de campos de esquema de detalles demográficos
description: Obtenga información acerca del grupo de campos del esquema Detalles demográficos.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---


# [!UICONTROL Datos demográficos] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Datos demográficos] es un grupo de campos de esquema estándar para [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). El grupo de campos proporciona un nivel de raíz `person` objeto, cuyos subcampos describen información sobre una persona individual.

![](../../images/field-groups/demographic-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `person.name` | [Nombre de persona](../../data-types/person-name.md) | Un objeto cuyos subcampos describen varios elementos del nombre de una persona. |
| `person.birthDate` | Fecha | La fecha completa en la que nació una persona, en forma de marca de tiempo ISO 8601. |
| `person.birthDayAndMonth` | Cadena | El día y el mes de nacimiento de una persona en formato MM-DD. Este campo debe usarse cuando se conoce el día y el mes del nacimiento de una persona, pero no el año. |
| `person.birthYear` | Número entero | El año en que nació una persona, incluido el siglo (como 1989). Este campo debe usarse cuando solo se conoce la edad de la persona, no la fecha de nacimiento completa. |
| `person.gender` | Cadena | La identidad de género de la persona. |
| `person.martialStatus` | Cadena | Describe la relación de una persona con su pareja. |
| `person.nationality` | Cadena | La relación jurídica entre una persona y su estado representada mediante el código ISO 3166-1 Alpha-2. |
| `person.taxId` | Cadena | CIF El ID fiscal de la persona, como el TIN en EE. UU. o el NIF/en España. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)