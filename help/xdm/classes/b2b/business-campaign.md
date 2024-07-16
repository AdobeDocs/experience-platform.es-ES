---
title: Clase de campaña empresarial de XDM
description: Obtenga información acerca de la clase de campaña empresarial XDM en Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# clase [!UICONTROL XDM Business Campaign]

>[!IMPORTANT]
>
>Esta clase está pensada para que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una campaña empresarial.

![La estructura de la clase de XDM Business Campaign tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-campaign.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de campaña. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema Source externo]](../../data-types/external-source-system-audit-attributes.md) | Si la campaña proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `_id` | Cadena | Un identificador único del registro. Este es un valor generado por el sistema que es independiente de `campaignID`. |
| `campaignDescription` | Cadena | Una descripción de la campaña. |
| `campaignID` | Cadena | Un identificador único de la entidad de campaña. |
| `campaignName` | Cadena | Nombre de la campaña. |
| `campaignType` | Cadena | El tipo de campaña o la audiencia de destino. |

{style="table-layout:auto"}

Para obtener información sobre cómo se relaciona conceptualmente esta clase con otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform, consulte la guía sobre [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Para obtener campos adicionales compatibles con esta clase, consulte la referencia de grupo de campos para [[!UICONTROL Detalles de XDM Business Campaign]](../../field-groups/b2b-campaign/details.md).
