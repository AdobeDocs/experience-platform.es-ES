---
title: Clase de cuenta comercial XDM
description: Este documento proporciona información general sobre la clase de cuenta empresarial XDM en el Modelo de datos de experiencia (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL XDM Business ] Accountclass

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la edición B2B de la plataforma de datos del cliente en tiempo real.

[!UICONTROL XDM Business ] Account es una clase estándar del Experience Data Model (XDM) que captura las propiedades mínimas requeridas de una cuenta comercial.

![](../../images/classes/b2b/business-account.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la entidad de cuenta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la cuenta procede de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del `accountID`. |
| `accountID` | Cadena | Identificador único de la entidad de cuenta. |
