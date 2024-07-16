---
title: Grupo de campos de esquema de detalles de depósito
description: Obtenga información acerca del grupo de campos de esquema Detalles de depósito.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL Detalles de depósito] grupo de campos de esquema

[!UICONTROL Detalles de depósito] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un solo campo `personalFinances.deposits` a un esquema, que captura detalles sobre un depósito financiero.

![](../../images/field-groups/deposit-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `account` | [[!UICONTROL Cuenta financiera]](../../data-types/financial-account.md) | Describe la cuenta financiera asociada con el depósito. |
| `transaction` | [[!UICONTROL Transacción]](../../data-types/transaction.md) | Describe la transacción financiera asociada con el depósito. |
| `mobileDeposit` | [!UICONTROL Booleano] | Indica si el depósito se realizó a través de una plataforma móvil. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
