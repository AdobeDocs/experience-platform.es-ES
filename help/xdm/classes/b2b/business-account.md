---
title: Clase de cuenta empresarial de XDM
description: Este documento proporciona información general sobre la clase de cuenta empresarial XDM en Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# [!UICONTROL Cuenta empresarial de XDM] clase

>[!IMPORTANT]
>
>El propósito de esta clase es que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Cuenta empresarial de XDM] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una cuenta comercial.

![La estructura de la clase de cuenta empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-account.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de cuenta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de origen externo]](../../data-types/external-source-system-audit-attributes.md) | Si la cuenta proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `_id` | Cadena | Un identificador único del registro. Es un valor generado por el sistema que es independiente del `accountKey` identificador. |
| `isDeleted` | Booleano | Indica si esta entidad de cuenta se ha eliminado en el Marketo Engage.<br><br>Al usar el [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md)Sin embargo, cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Por configuración `isDeleted` hasta `true`Sin embargo, puede utilizar el campo para filtrar qué registros se han eliminado de las fuentes al consultar el lago de datos. |

{style="table-layout:auto"}

Consulte la guía de [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
