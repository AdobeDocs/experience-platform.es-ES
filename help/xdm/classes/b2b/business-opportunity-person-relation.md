---
title: Clase de relación de persona de oportunidad empresarial XDM
description: Este documento proporciona una descripción general de la clase de relación de persona de oportunidad empresarial XDM en el Modelo de datos de experiencia (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 3%

---

# [!UICONTROL XDM Business Oportunity Person ] Relationship

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la plataforma de datos del cliente en tiempo real B2B Edition.

[!UICONTROL La ] relación de persona de oportunidad comercial XDM es una clase estándar del Modelo de datos de experiencia (XDM) que captura las propiedades mínimas requeridas de una persona asociada con una oportunidad comercial.

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

Consulte la guía sobre las [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
