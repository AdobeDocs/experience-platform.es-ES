---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalles de marketing de campaña
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de marketing de campaña .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] esquema de detalles de marketing de Campaign

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL La ] información de marketing de Campaign es un grupo de campos de esquema estándar para la  [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md), que se utiliza para describir la información de campaña de marketing como el grupo de campaña, el nombre y el código de seguimiento.

![](../../images/field-groups/campaign-marketing-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Un objeto que describe información de campañas de marketing como grupo de campañas, nombre y código de seguimiento. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
