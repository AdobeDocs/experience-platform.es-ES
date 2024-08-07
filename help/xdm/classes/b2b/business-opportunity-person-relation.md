---
title: Clase de relación de persona de oportunidad empresarial XDM
description: Obtenga información acerca de la clase de relación de persona de oportunidad empresarial de XDM en Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 3%

---

# [!UICONTROL Relación de persona de oportunidad empresarial de XDM] clase

>[!IMPORTANT]
>
>Esta clase está pensada para que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Relación personal de oportunidad empresarial de XDM] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una persona asociada a una oportunidad comercial.

![La estructura de la clase de persona de oportunidad empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-opportunity-person-relation.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema Source externo]](../../data-types/external-source-system-audit-attributes.md) | Si la relación de persona de negocios proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la oportunidad en la relación oportunidad-persona. |
| `opportunityPersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de relación oportunidad-persona. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la persona en la relación oportunidad-persona. |
| `_id` | Cadena | Un identificador único del registro. Es un valor generado por el sistema que es independiente de los demás campos de ID capturados por la clase. |
| `isDeleted` | Booleano | Indica si esta entidad de la lista de marketing se ha eliminado en el Marketo Engage.<br><br>Al usar el [conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Al establecer `isDeleted` en `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |
| `isPrimary` | Booleano | Indica si la persona es el contacto principal de esta oportunidad. |
| `opportunityID` | Cadena | Un identificador único de la oportunidad en la relación oportunidad-persona. |
| `opportunityPersonID` | Cadena | Un identificador único de la entidad de relación oportunidad-persona |
| `personID` | Cadena | Un identificador único de la persona en la relación oportunidad-persona. |
| `personRole` | Cadena | La función de la persona en la relación persona-oportunidad. |

{style="table-layout:auto"}

Consulte la guía sobre [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para obtener información sobre cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
