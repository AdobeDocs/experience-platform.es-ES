---
title: Clase de relación de persona de la cuenta XDM
description: Obtenga información acerca de la clase de relación de persona de la cuenta XDM en el modelo de datos de experiencia (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# [!UICONTROL Relación de persona de la cuenta XDM] clase

>[!IMPORTANT]
>
>El propósito de esta clase es que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Relación de persona de la cuenta XDM] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una persona asociada a una cuenta comercial.

![La estructura de la clase de relación de persona de la cuenta empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-account-person-relation.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la cuenta en la relación cuenta-persona. |
| `accountPersonKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de relación cuenta-persona. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de origen externo]](../../data-types/external-source-system-audit-attributes.md) | Si la relación cuenta-persona proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `personKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto de la persona en la relación cuenta-persona. |
| `_id` | Cadena | Un identificador único del registro. Es un valor generado por el sistema que es independiente de los demás campos de ID capturados por la clase. |
| `accountID` | Cadena | Un identificador único de la cuenta en la relación cuenta-persona. |
| `accountPersonID` | Cadena | Identificador único de la entidad de relación cuenta-persona. |
| `currencyCode` | Cadena | El código de divisa en formato ISO 4217 usado para la relación entre la cuenta y la persona. |
| `isActive` | Booleano | Indica si la relación entre la cuenta y la persona está activa. |
| `isDeleted` | Booleano | Indica si esta relación cuenta-persona se ha eliminado en el Marketo Engage.<br><br>Al usar el [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md)Sin embargo, cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Por configuración `isDeleted` hasta `true`Sin embargo, puede utilizar el campo para filtrar qué registros se han eliminado de las fuentes al consultar el lago de datos. |
| `isDirect` | Booleano | Indica si se trata de una relación directa entre la cuenta y la persona. |
| `isPrimary` | Booleano | Indica si la persona es el contacto principal de esta cuenta. |
| `personID` | Cadena | Un identificador único de la persona en la relación cuenta-persona. |
| `personRoles` | Matriz de cadenas | Muestra las funciones de la persona en la relación cuenta-persona. |
| `relationEndDate` | DateTime | La fecha en la que terminó la relación entre la cuenta y la persona. |
| `relationStartDate` | DateTime | La fecha en la que comenzó la relación entre la cuenta y la persona. |
| `relationshipSource` | Cadena | Origen de la relación cuenta-persona. |

{style="table-layout:auto"}

Consulte la guía de [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
