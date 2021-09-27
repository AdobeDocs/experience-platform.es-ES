---
title: Clase de campaña empresarial XDM
description: Este documento proporciona una descripción general de la clase XDM Business Campaign en Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL XDM Business ] Campaign

>[!NOTE]
>
>Esta clase solo está disponible para organizaciones que tienen acceso a la edición B2B de la plataforma de datos del cliente en tiempo real.

[!UICONTROL XDM Business ] Campaign es una clase de Experience Data Model (XDM) estándar que captura las propiedades mínimas requeridas de una campaña comercial.

![](../../images/classes/b2b/business-campaign.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para la entidad de campaña. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoría del sistema de fuentes externas]](../../data-types/external-source-system-audit-attributes.md) | Si la campaña procede de un sistema de origen externo, este objeto captura los atributos de auditoría de ese sistema. |
| `_id` | Cadena | Identificador único del registro. Se trata de un valor generado por el sistema que es independiente del `campaignID`. |
| `campaignDescription` | Cadena | Descripción de la campaña. |
| `campaignID` | Cadena | Un identificador único para la entidad de campaña. |
| `campaignName` | Cadena | Nombre de la campaña. |
| `campaignType` | Cadena | El tipo de campaña o audiencia de destino. |
