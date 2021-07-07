---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema Detalles del canal
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del canal .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] esquema de detalles del canal

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL La ] información de canal es un grupo de campos de esquema estándar para la  [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md), que se utiliza para describir la información de canal como ID, tipo de canal, tipo de medio y tipo de ubicación.

![](../../images/field-groups/channel-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `channel` | [Canal de experiencia](../../data-types/experience-channel.md) | Un objeto que describe devoluciones de productos, registro de garantías y procesos de carro/pedido de compras. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
