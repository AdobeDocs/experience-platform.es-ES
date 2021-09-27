---
title: Clase de miembros de XDM Business Campaign
description: Este documento proporciona información general sobre la clase de miembros de la campaña empresarial XDM en el Modelo de datos de experiencia (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign ] Membersclass

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la edición B2B de la plataforma de datos del cliente en tiempo real.

[!UICONTROL La ] pertenencia a XDM Business Campaign es una clase estándar de Experience Data Model (XDM) que describe un contacto o posible cliente asociado a una campaña empresarial.

![](../../images/classes/b2b/business-campaign-members.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la campaña asociada. |
| `campaignMemberKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de pertenencia a la campaña. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la pertenencia a la campaña proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `personKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la persona que es miembro de la campaña asociada. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del `campaignMemberID`. |
| `campaignID` | Cadena | Un ID único para la campaña asociada. |
| `campaignMemberID` | Cadena | Un ID único para la entidad de pertenencia a la campaña. |
| `personId` | Cadena | Un ID único para la persona que es miembro de la campaña asociada. |
