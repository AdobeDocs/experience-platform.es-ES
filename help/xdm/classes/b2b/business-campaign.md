---
title: Clase de campaña empresarial XDM
description: Este documento proporciona una descripción general de la clase XDM Business Campaign en Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---

# [!UICONTROL Campaña empresarial XDM] class

[!UICONTROL Campaña empresarial XDM] es una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una campaña comercial.

![](../../images/classes/b2b/business-campaign.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de campaña. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la campaña procede de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del valor `campaignID`. |
| `campaignDescription` | Cadena | Descripción de la campaña. |
| `campaignID` | Cadena | Un identificador único para la entidad de campaña. |
| `campaignName` | Cadena | Nombre de la campaña. |
| `campaignType` | Cadena | El tipo de campaña o audiencia de destino. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
