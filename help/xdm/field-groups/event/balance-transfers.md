---
title: Balance Transfers Schema Field Group
description: This document provides an overview of the Balance Transfers schema field group.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 4%

---

# 

[[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) `personalFinances.balanceTransfers`

![](../../images/field-groups/balance-transfers.png)

| Propiedad | Data type | Descripción |
| --- | --- | --- |
| `accountFrom` | [](../../data-types/financial-account.md) | Describes the financial account that balance is being transferred from. |
| `accountTo` | [](../../data-types/financial-account.md) | Describes the financial account that balance is being transferred to. |
| `transaction` | [](../../data-types/transaction.md) | Describes the financial transaction associated with the balance transfer. |

{style=&quot;table-layout:auto&quot;}

[](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json)
