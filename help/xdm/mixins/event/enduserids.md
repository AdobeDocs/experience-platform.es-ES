---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: Mezcla de ID de usuario final de ExperienceEvent
topic: overview
description: Este documento proporciona información general sobre la combinación de ID de usuario final de ExperienceEvent.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# [!UICONTROL Mezcla de ID de usuario] final de ExperienceEvent

[!UICONTROL ExperienceEvent EndUserIDs] es una combinación estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/individual-profile.md), que se utiliza para describir la información de identidad de un individuo en varias aplicaciones Adobe. La mezcla proporciona un `endUserIDs` objeto de nivel raíz, que contiene un campo de solo lectura `_experience` cuyos valores se actualizan automáticamente a medida que se ingestan datos.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `aacustomid` | [Identidad](../../data-types/identity.md) | ID de usuario final personalizados para Adobe Analytics Cloud. |
| `aaid` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Analytics Cloud. |
| `acid` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Campaign. |
| `adcloud` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Advertising Cloud. |
| `emailid` | [Identidad](../../data-types/identity.md) | ID de direcciones de correo electrónico. |
| `mcid` | [Identidad](../../data-types/identity.md) | ID de Adobe Marketing Cloud. |
| `phonenumberid` | [Identidad](../../data-types/identity.md) | ID de número de teléfono. |
| `tntid` | [Identidad](../../data-types/identity.md) | ID de usuario final para Adobe Target. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
