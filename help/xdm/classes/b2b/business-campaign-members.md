---
title: Clase de miembros de XDM Business Campaign
description: Este documento proporciona información general sobre la clase de miembros de la campaña empresarial XDM en el Modelo de datos de experiencia (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 4%

---

# [!UICONTROL Miembros de XDM Business Campaign] class

[!UICONTROL Miembros de XDM Business Campaign] es una clase estándar de Experience Data Model (XDM) que describe un contacto o posible cliente asociado a una campaña empresarial.

![](../../images/classes/b2b/business-campaign-members.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la campaña asociada. |
| `campaignMemberKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de pertenencia a la campaña. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la pertenencia a la campaña proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `personKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la persona que es miembro de la campaña asociada. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del valor `campaignMemberID`. |
| `campaignID` | Cadena | Un ID único para la campaña asociada. |
| `campaignMemberID` | Cadena | Un ID único para la entidad de pertenencia a la campaña. |
| `personId` | Cadena | Un ID único para la persona que es miembro de la campaña asociada. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
