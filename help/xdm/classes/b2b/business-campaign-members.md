---
title: Clase de miembros de XDM Business Campaign
description: Este documento proporciona información general sobre la clase de miembros de la campaña empresarial XDM en el Modelo de datos de experiencia (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 3%

---

# [!UICONTROL Miembros de XDM Business Campaign] class

>[!IMPORTANT]
>
>Esta clase está diseñada para ser utilizada por organizaciones con acceso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a CDP B2B Edition en tiempo real para que esta clase participe en [Perfil del cliente en tiempo real](../../../profile/home.md).

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
