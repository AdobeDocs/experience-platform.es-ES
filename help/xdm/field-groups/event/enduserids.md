---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;enduserids;usuario final;usuario final;ids;
solution: Experience Platform
title: Grupo de campos de esquema de detalles del ID del usuario final
description: Este documento proporciona información general sobre el grupo de campos de esquema Detalles del ID de usuario final.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 4%

---


# [!UICONTROL Detalles del ID del usuario final] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles del ID del usuario final] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md), se utiliza para describir la información de identidad de un individuo en varias aplicaciones de Adobe. El grupo de campos proporciona un nivel de raíz `endUserIDs` objeto, que contiene un objeto de sólo lectura `_experience` campo cuyos valores se actualizan automáticamente a medida que se incorporan los datos.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `aacustomid` | [Identidad](../../data-types/identity.md) | ID de usuarios finales personalizados para Adobe Analytics Cloud. |
| `aaid` | [Identidad](../../data-types/identity.md) | ID de usuarios finales de Adobe Analytics Cloud. |
| `acid` | [Identidad](../../data-types/identity.md) | ID de usuarios finales de Adobe Campaign. |
| `adcloud` | [Identidad](../../data-types/identity.md) | ID de usuarios finales de Adobe Advertising Cloud. |
| `emailid` | [Identidad](../../data-types/identity.md) | ID de direcciones de correo electrónico. |
| `mcid` | [Identidad](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). El MCID ahora se conoce como ID de Experience Cloud (ECID). |
| `phonenumberid` | [Identidad](../../data-types/identity.md) | ID de número de teléfono. |
| `tntid` | [Identidad](../../data-types/identity.md) | ID de usuarios finales de Adobe Target. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
