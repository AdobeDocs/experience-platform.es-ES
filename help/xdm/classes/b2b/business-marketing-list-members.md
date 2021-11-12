---
title: Clase de miembros de la lista de marketing empresarial XDM
description: Este documento proporciona información general sobre la clase de miembros de la lista de marketing empresarial XDM en el modelo de datos de experiencia (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# [!UICONTROL Miembros de la lista de marketing empresarial XDM] class

[!UICONTROL Miembros de la lista de marketing empresarial XDM] es una clase estándar de Experience Data Model (XDM) que describe miembros, personas o contactos asociados a una lista de marketing.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la pertenencia a la lista de marketing proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `marketingListKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la lista de marketing a la que pertenece la persona. |
| `marketingListMemberKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de pertenencia a la lista de marketing. |
| `personKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la persona que es miembro de la lista de marketing. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del valor `marketingListMemberID`. |
| `marketingListID` | Cadena | Un ID único para la lista de marketing. |
| `marketingListMemberID` | Cadena | Un ID único para la entidad de pertenencia a la lista de marketing. |
| `personId` | Cadena | Un ID único para la persona. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
