---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema Detalles del canal
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del canal .
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 3%

---

# [!UICONTROL Detalles del canal] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles del canal] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), se utiliza para describir información de canal como ID, tipo de canal, tipo de medio y tipo de ubicación.

![](../../images/field-groups/channel-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `channel` | [Canal de experiencia](../../data-types/experience-channel.md) | Un objeto que describe devoluciones de productos, registro de garantías y procesos de carro/pedido de compras. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
