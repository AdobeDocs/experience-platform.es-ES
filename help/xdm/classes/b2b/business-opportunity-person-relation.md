---
title: Clase de relación de persona de oportunidad empresarial XDM
description: Este documento proporciona una descripción general de la clase de relación de persona de oportunidad empresarial XDM en el Modelo de datos de experiencia (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 4%

---

# [!UICONTROL Relación de persona de oportunidad comercial XDM] class

[!UICONTROL Relación de persona de oportunidad comercial XDM] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una persona asociada con una oportunidad comercial.

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la relación de persona comercial proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `opportunityKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la oportunidad en la relación oportunidad-persona. |
| `opportunityPersonKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de relación entre oportunidad y persona. |
| `personKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la persona en la relación oportunidad-persona. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente de los demás campos de ID capturados por la clase . |
| `opportunityID` | Cadena | Identificador único de la oportunidad en la relación oportunidad-persona. |
| `opportunityPersonID` | Cadena | Un identificador único para la entidad de relación entre oportunidad y persona |
| `isPrimary` | Booleano | Indica si la persona es el contacto principal de esta oportunidad. |
| `personID` | Cadena | Identificador único de la persona en la relación oportunidad-persona. |
| `personRole` | Cadena | El papel de la persona en la relación oportunidad-persona. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
