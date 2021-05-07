---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;enduserids;usuario final;usuario final;id;
solution: Experience Platform
title: Grupo de campos de esquema de detalles de ID de usuario final
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del ID de usuario final .
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL End User ID Details] es un grupo de campos de esquema estándar para la  [[!DNL XDM ExperienceEvent] clase](../../classes/individual-profile.md), que se utiliza para describir la información de identidad de una persona en varias aplicaciones de Adobe. El grupo de campos proporciona un objeto `endUserIDs` de nivel raíz, que contiene un campo `_experience` de solo lectura cuyos valores se actualizan automáticamente a medida que se introducen datos.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `aacustomid` | [Identidad](../../data-types/identity.md) | ID de usuario final personalizados para Adobe Analytics Cloud. |
| `aaid` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Analytics Cloud. |
| `acid` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Campaign. |
| `adcloud` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Advertising Cloud. |
| `emailid` | [Identidad](../../data-types/identity.md) | ID de direcciones de correo electrónico. |
| `mcid` | [Identidad](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identidad](../../data-types/identity.md) | ID de número de teléfono. |
| `tntid` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Target. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
