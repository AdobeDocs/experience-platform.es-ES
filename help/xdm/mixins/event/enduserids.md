---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;mezcla;mezcla;enduserids;usuario final;usuario final;id;
solution: Experience Platform
title: Mezcla de detalles de ID de usuario final
topic-legacy: overview
description: Este documento proporciona información general sobre la mezcla de Detalles del ID de usuario final.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# [!UICONTROL End User ID Details] mixto

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../name-updates.md) para obtener más información.

[!UICONTROL End User ID Details] es una mezcla estándar para la  [[!DNL XDM ExperienceEvent] clase](../../classes/individual-profile.md), utilizada para describir la información de identidad de una persona en varias aplicaciones de Adobe. La mezcla proporciona un objeto `endUserIDs` de nivel raíz, que contiene un campo `_experience` de solo lectura cuyos valores se actualizan automáticamente a medida que se introducen datos.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

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

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
