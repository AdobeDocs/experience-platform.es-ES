---
title: Clase de cuenta comercial XDM
description: Este documento proporciona información general sobre la clase de cuenta empresarial XDM en el Modelo de datos de experiencia (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 3%

---

# [!UICONTROL Cuenta comercial XDM] class

>[!IMPORTANT]
>
>Esta clase está diseñada para ser utilizada por organizaciones con acceso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Debe tener acceso a CDP B2B Edition en tiempo real para que esta clase participe en [Perfil del cliente en tiempo real](../../../profile/home.md).

[!UICONTROL Cuenta comercial XDM] es una clase estándar de Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una cuenta comercial.

![](../../images/classes/b2b/business-account.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de cuenta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la cuenta procede de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del valor `accountID`. |
| `accountID` | Cadena | Identificador único de la entidad de cuenta. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [relaciones de esquema en tiempo real CDP B2B Edition](../../tutorials/relationship-b2b.md) para conocer cómo se relaciona esta clase conceptualmente con las otras clases B2B y cómo puede establecer estas relaciones en la interfaz de usuario de Adobe Experience Platform.
