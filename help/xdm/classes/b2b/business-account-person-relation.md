---
title: Clase de relación de persona de cuenta comercial XDM
description: Este documento proporciona información general sobre la clase de relación de persona de cuenta empresarial XDM en el Modelo de datos de experiencia (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# [!UICONTROL Relación de persona de cuenta comercial XDM] class

>[!IMPORTANT]
>
>Esta clase está diseñada para ser utilizada por organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase participe en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Relación de persona de cuenta comercial XDM] es una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una persona asociada a una cuenta comercial.

![La estructura de la clase de relación de persona de cuenta empresarial XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-account-person-relation.png)

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
| `isDeleted` | Booleano | Indica si esta relación cuenta-persona se ha eliminado en el Marketo Engage.<br><br>Al usar la variable [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Si configura `isDeleted` a `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |
| `isDirect` | Booleano | Indica si se trata de una relación directa entre la cuenta y la persona. |
| `isPrimary` | Booleano | Indica si la persona es el contacto principal de esta cuenta. |
| `personID` | Cadena | Identificador único de la persona en la relación entre cuenta y persona. |
| `personRoles` | Matriz de cadenas | Enumera las funciones de la persona en la relación entre cuenta y persona. |
| `relationEndDate` | DateTime | La fecha en la que finalizó la relación entre la cuenta y la persona. |
| `relationStartDate` | DateTime | La fecha en la que se inició la relación entre la cuenta y la persona. |
| `relationshipSource` | Cadena | Origen de la relación entre la cuenta y la persona. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
