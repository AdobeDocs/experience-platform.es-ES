---
title: Clase de oportunidad empresarial XDM
description: Este documento proporciona información general sobre la clase de oportunidad empresarial XDM en el Modelo de datos de experiencia (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 6%

---

# [!UICONTROL Oportunidad comercial XDM] class

[!UICONTROL Oportunidad comercial XDM] es una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una oportunidad comercial.

![](../../images/classes/b2b/business-opportunity.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la cuenta a la que se asocia esta oportunidad. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la oportunidad proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `opportunityKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de oportunidad. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del valor `opportunityID`. |
| `accountID` | Cadena | Un ID único para la cuenta a la que se asocia esta oportunidad. |
| `opportunityDescription` | Cadena | Una descripción de la oportunidad. |
| `opportunityID` | Cadena | Un ID único para la entidad de oportunidad. |
| `opportunityName` | Cadena | El nombre de la oportunidad. |
| `opportunityStage` | Cadena | La fase de ventas de la oportunidad. |
| `opportunityType` | Cadena | El tipo de oportunidad. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
