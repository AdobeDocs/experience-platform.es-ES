---
title: Clase de miembros de lista de marketing empresarial de XDM
description: Obtenga información acerca de la clase de miembros de la lista de marketing empresarial de XDM en el modelo de datos de experiencia (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---

# [!UICONTROL Miembros de la lista de marketing empresarial de XDM] clase

>[!IMPORTANT]
>
>Esta clase está pensada para que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Miembros de la lista de marketing empresarial de XDM] es una clase estándar de modelo de datos de experiencia (XDM) que describe miembros, personas o contactos asociados con una lista de marketing.

![La estructura de la clase de miembros de la lista de marketing empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-marketing-list-members.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema Source externo]](../../data-types/external-source-system-audit-attributes.md) | Si la pertenencia a la lista de marketing proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la lista de marketing a la que está abonada la persona. |
| `marketingListMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de pertenencia a la lista de marketing. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto de la persona que es miembro de la lista de marketing. |
| `_id` | Cadena | Un identificador único del registro. Este es un valor generado por el sistema que es independiente de `marketingListMemberID`. |
| `isDeleted` | Booleano | Indica si esta entidad miembro de la lista de marketing se ha eliminado en el Marketo Engage.<br><br>Al usar el [conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Al establecer `isDeleted` en `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |
| `marketingListID` | Cadena | Un ID único para la lista de marketing. |
| `marketingListMemberID` | Cadena | ID único de la entidad de pertenencia a lista de marketing. |
| `personId` | Cadena | Un ID único para la persona. |

{style="table-layout:auto"}

Consulte la guía sobre [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para obtener información sobre cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
