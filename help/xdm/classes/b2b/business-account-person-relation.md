---
title: Clase de relación de persona de cuenta comercial XDM
description: Este documento proporciona información general sobre la clase de relación de persona de cuenta empresarial XDM en el Modelo de datos de experiencia (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# [!UICONTROL XDM Business Account Person ] Relationship

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la plataforma de datos del cliente en tiempo real B2B Edition.

[!UICONTROL XDM Business Account Person ] una clase estándar del Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una persona asociada a una cuenta comercial.

![](../../images/classes/b2b/business-account-person-relation.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la cuenta en la relación entre cuenta y persona. |
| `accountPersonKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de relación entre cuenta y persona. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la relación entre cuenta y persona proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `personKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la persona en la relación entre cuenta y persona. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente de los demás campos de ID capturados por la clase . |
| `accountID` | Cadena | Identificador único de la cuenta en la relación entre cuenta y persona. |
| `accountPersonID` | Cadena | Identificador único de la entidad de relación entre cuenta y persona. |
| `currencyCode` | Cadena | Código de moneda ISO 4217 utilizado para la relación entre la cuenta y la persona. |
| `isActive` | Booleano | Indica si la relación entre la cuenta y la persona está activa. |
| `isDirect` | Booleano | Indica si se trata de una relación directa entre la cuenta y la persona. |
| `isPrimary` | Booleano | Indica si la persona es el contacto principal de esta cuenta. |
| `personID` | Cadena | Identificador único de la persona en la relación entre cuenta y persona. |
| `personRole` | Cadena | Función de la persona en la relación entre cuenta y persona. |
| `relationEndDate` | DateTime | La fecha en la que finalizó la relación entre la cuenta y la persona. |
| `relationStartDate` | DateTime | La fecha en la que se inició la relación entre la cuenta y la persona. |

Consulte la guía sobre las [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
