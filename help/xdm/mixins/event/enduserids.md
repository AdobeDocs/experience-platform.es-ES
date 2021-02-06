---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;diseño de Esquema;mezcla;mezcla;combinación;enduserids;usuario final;id;
solution: Experience Platform
title: Mezcla de detalles de ID de usuario final
topic: overview
description: Este documento proporciona una visión general de la combinación de detalles del ID de usuario final.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# [!UICONTROL Detalles del ID de usuario final ] mixin

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento en [actualizaciones de nombres de mezcla](../name-updates.md) para obtener más información.

[!UICONTROL ID de usuario final ] Detalla una combinación estándar para la  [[!DNL XDM ExperienceEvent] clase](../../classes/individual-profile.md), utilizada para describir la información de identidad de un individuo en varias aplicaciones de Adobe. La mezcla proporciona un objeto de nivel raíz `endUserIDs`, que contiene un campo de sólo lectura `_experience` cuyos valores se actualizan automáticamente a medida que se ingestan los datos.

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
