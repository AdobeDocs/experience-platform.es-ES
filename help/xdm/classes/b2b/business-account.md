---
title: Clase de cuenta empresarial de XDM
description: Obtenga información acerca de la clase de cuenta empresarial XDM en Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# clase [!UICONTROL XDM Business Account]

>[!IMPORTANT]
>
>Esta clase está pensada para que la utilicen organizaciones con acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a Real-Time CDP B2B Edition para que esta clase pueda participar en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL La cuenta empresarial de XDM] es una clase de modelo de datos de experiencia (XDM) estándar que captura las propiedades mínimas requeridas de una cuenta comercial.

![La estructura de la clase de cuenta empresarial de XDM tal como aparece en la interfaz de usuario](../../images/classes/b2b/business-account.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de cuenta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema Source externo]](../../data-types/external-source-system-audit-attributes.md) | Si la cuenta proviene de un sistema de origen externo, este objeto captura atributos de auditoría para ese sistema. |
| `_id` | Cadena | Un identificador único del registro. Es un valor generado por el sistema que es independiente del identificador `accountKey`. |
| `isDeleted` | Booleano | Indica si esta entidad de cuenta se ha eliminado en el Marketo Engage.<br><br>Al usar el [conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Al establecer `isDeleted` en `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |

{style="table-layout:auto"}

Consulte la guía sobre [relaciones de esquema en Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para obtener información sobre cómo se relaciona conceptualmente esta clase con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
