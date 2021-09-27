---
title: Clase de relación de persona de oportunidad empresarial XDM
description: Este documento proporciona una descripción general de la clase de relación de persona de oportunidad empresarial XDM en el Modelo de datos de experiencia (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 3%

---

# [!UICONTROL XDM Business Oportunity Person ] Relationship

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la edición B2B de la plataforma de datos del cliente en tiempo real.

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
