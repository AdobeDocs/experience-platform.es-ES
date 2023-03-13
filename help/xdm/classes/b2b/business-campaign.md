---
title: Clase de campaña empresarial de XDM
description: Este documento proporciona información general sobre la clase de campaña empresarial de XDM en el modelo de datos de experiencia (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# [!UICONTROL Campaña empresarial de XDM] clase

>[!IMPORTANT]
>
>El propósito de esta clase es que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Campaña empresarial de XDM] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una campaña empresarial.

![La estructura de la clase de campaña empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-campaign.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de campaña. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de origen externo]](../../data-types/external-source-system-audit-attributes.md) | Si la campaña proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `_id` | Cadena | Un identificador único del registro. Es un valor generado por el sistema que es independiente del `campaignID`. |
| `campaignDescription` | Cadena | Una descripción de la campaña. |
| `campaignID` | Cadena | Un identificador único de la entidad de campaña. |
| `campaignName` | Cadena | Nombre de la campaña. |
| `campaignType` | Cadena | El tipo de campaña o la audiencia de destino. |

{style="table-layout:auto"}

Para obtener información sobre cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform, consulte la guía sobre [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para ver los campos adicionales compatibles con esta clase, consulte la referencia de grupo de campos para [[!UICONTROL Detalles de la campaña empresarial de XDM]](../../field-groups/b2b-campaign/details.md).
