---
title: Clase de relación de persona de cuenta comercial XDM
description: Este documento proporciona información general sobre la clase de relación de persona de cuenta empresarial XDM en el Modelo de datos de experiencia (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# [!UICONTROL Relación de persona de cuenta comercial XDM] class

>[!IMPORTANT]
>
>Esta clase está diseñada para ser utilizada por organizaciones con acceso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a CDP B2B Edition en tiempo real para que esta clase participe en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Relación de persona de cuenta comercial XDM] es una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una persona asociada a una cuenta comercial.

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

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
