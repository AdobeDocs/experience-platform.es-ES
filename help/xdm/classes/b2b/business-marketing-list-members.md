---
title: Clase de miembros de lista de marketing empresarial de XDM
description: Este documento proporciona información general sobre la clase de miembros de lista de marketing empresarial de XDM en el modelo de datos de experiencia (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---

# [!UICONTROL Miembros de lista de marketing empresarial de XDM] clase

>[!IMPORTANT]
>
>El propósito de esta clase es que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Miembros de lista de marketing empresarial de XDM] es una clase de modelo de datos de experiencia (XDM) estándar que describe miembros, personas o contactos asociados a una lista de marketing.

![La estructura de la clase Miembros de la lista de marketing empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-marketing-list-members.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de origen externo]](../../data-types/external-source-system-audit-attributes.md) | Si la pertenencia a la lista de marketing proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `marketingListKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la lista de marketing a la que está abonada la persona. |
| `marketingListMemberKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de pertenencia a la lista de marketing. |
| `personKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto de la persona que es miembro de la lista de marketing. |
| `_id` | Cadena | Un identificador único del registro. Es un valor generado por el sistema que es independiente del `marketingListMemberID`. |
| `isDeleted` | Booleano | Indica si esta entidad miembro de la lista de marketing se ha eliminado en el Marketo Engage.<br><br>Al usar el [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md)Sin embargo, cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Por configuración `isDeleted` hasta `true`Sin embargo, puede utilizar el campo para filtrar qué registros se han eliminado de las fuentes al consultar el lago de datos. |
| `marketingListID` | Cadena | Un ID único para la lista de marketing. |
| `marketingListMemberID` | Cadena | ID único de la entidad de pertenencia a lista de marketing. |
| `personId` | Cadena | Un ID único para la persona. |

{style="table-layout:auto"}

Consulte la guía de [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
