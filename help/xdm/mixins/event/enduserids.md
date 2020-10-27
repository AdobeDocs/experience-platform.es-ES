---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: Mezcla de detalles de ID de usuario final
topic: overview
description: Este documento proporciona una visión general de la combinación de detalles del ID de usuario final.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---


# [!UICONTROL Mezcla de detalles] de ID de usuario final

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre las actualizaciones [de nombres de](../name-updates.md) mezcla para obtener más información.

[!UICONTROL Detalles] de ID de usuario final es una combinación estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/individual-profile.md), que se utiliza para describir la información de identidad de una persona en varias aplicaciones de Adobe. La mezcla proporciona un `endUserIDs` objeto de nivel raíz, que contiene un campo de solo lectura `_experience` cuyos valores se actualizan automáticamente a medida que se ingestan datos.

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
