---
title: Grupo de campos de esquema de detalles de depósito
description: Este documento proporciona información general del grupo de campos de esquema Detalles de depósito.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 2%

---

# [!UICONTROL Detalles de depósito] grupo de campos de esquema

[!UICONTROL Detalles de depósito] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un solo `personalFinances.deposits` a un esquema, que captura detalles sobre un depósito financiero.

![](../../images/field-groups/deposit-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `account` | [[!UICONTROL Cuenta financiera]](../../data-types/financial-account.md) | Describe la cuenta financiera asociada con el depósito. |
| `transaction` | [[!UICONTROL Transacción]](../../data-types/transaction.md) | Describe la transacción financiera asociada con el depósito. |
| `mobileDeposit` | [!UICONTROL Booleana] | Indica si el depósito se realizó a través de una plataforma móvil. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
