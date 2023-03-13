---
title: Clase de miembros de XDM Business Campaign
description: Este documento proporciona información general sobre la clase de miembros de XDM Business Campaign en el modelo de datos de experiencia (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 1%

---

# [!UICONTROL Miembros de campaña empresarial de XDM] clase

>[!IMPORTANT]
>
>El propósito de esta clase es que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Miembros de campaña empresarial de XDM] es una clase de modelo de datos de experiencia (XDM) estándar que describe un contacto o posible cliente asociado a una campaña empresarial.

![La estructura de la clase de miembros de XDM Business Campaign tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-campaign-members.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la campaña asociada. |
| `campaignMemberKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de pertenencia a la campaña. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de origen externo]](../../data-types/external-source-system-audit-attributes.md) | Si la pertenencia a la campaña proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `personKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto de la persona que es miembro de la campaña asociada. |
| `_id` | Cadena | Un identificador único del registro. Es un valor generado por el sistema que es independiente del `campaignMemberID`. |

{style="table-layout:auto"}

Para obtener información sobre cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform, consulte la guía sobre [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para ver los campos adicionales compatibles con esta clase, consulte la referencia de grupo de campos para [[!UICONTROL Detalles del miembro de la campaña empresarial de XDM]](../../field-groups/b2b-campaign-members/details.md).
