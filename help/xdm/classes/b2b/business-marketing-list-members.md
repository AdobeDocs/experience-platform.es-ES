---
title: Clase de miembros de la lista de marketing empresarial XDM
description: Este documento proporciona información general sobre la clase de miembros de la lista de marketing empresarial XDM en el modelo de datos de experiencia (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List ] Membersclass

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la plataforma de datos del cliente en tiempo real B2B Edition.

[!UICONTROL La ] pertenencia a la lista de marketing empresarial XDM es una clase estándar del Modelo de datos de experiencia (XDM) que describe miembros, personas o contactos asociados con una lista de marketing.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la pertenencia a la lista de marketing proviene de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `marketingListKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la lista de marketing a la que pertenece la persona. |
| `marketingListMemberKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de pertenencia a la lista de marketing. |
| `personKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la persona que es miembro de la lista de marketing. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del `marketingListMemberID`. |
| `marketingListID` | Cadena | Un ID único para la lista de marketing. |
| `marketingListMemberID` | Cadena | Un ID único para la entidad de pertenencia a la lista de marketing. |
| `personId` | Cadena | Un ID único para la persona. |

Consulte la guía sobre las [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
