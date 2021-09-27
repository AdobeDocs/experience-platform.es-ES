---
title: Clase de oportunidad empresarial XDM
description: Este documento proporciona información general sobre la clase de oportunidad empresarial XDM en el Modelo de datos de experiencia (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---

# [!UICONTROL Clase de ] oportunidad empresarial XDM

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la edición B2B de la plataforma de datos del cliente en tiempo real.

[!UICONTROL XDM Business ] Oportunityes una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una oportunidad comercial.

![](../../images/classes/b2b/business-opportunity.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la cuenta a la que se asocia esta oportunidad. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la oportunidad proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `opportunityKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de oportunidad. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del `opportunityID`. |
| `accountID` | Cadena | Un ID único para la cuenta a la que se asocia esta oportunidad. |
| `opportunityDescription` | Cadena | Una descripción de la oportunidad. |
| `opportunityID` | Cadena | Un ID único para la entidad de oportunidad. |
| `opportunityName` | Cadena | El nombre de la oportunidad. |
| `opportunityStage` | Cadena | La fase de ventas de la oportunidad. |
| `opportunityType` | Cadena | El tipo de oportunidad. |
