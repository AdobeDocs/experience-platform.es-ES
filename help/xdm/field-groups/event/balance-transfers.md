---
title: Grupo de campos de esquema de transferencias de saldo
description: Obtenga información sobre el grupo de campos de esquema Transferencias de saldo.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# [!UICONTROL Transferencias de saldo] grupo de campos de esquema

[!UICONTROL Transferencias de saldo] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). El grupo de campos proporciona un único objeto `personalFinances.balanceTransfers` a un esquema, que captura detalles sobre una transferencia de saldo financiero entre cuentas.

![](../../images/field-groups/balance-transfers.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Cuenta financiera]](../../data-types/financial-account.md) | Describe la cuenta financiera desde la que se transfiere el saldo. |
| `accountTo` | [[!UICONTROL Cuenta financiera]](../../data-types/financial-account.md) | Describe la cuenta financiera a la que se transfiere el saldo. |
| `transaction` | [[!UICONTROL Transacción]](../../data-types/transaction.md) | Describe la transacción financiera asociada con la transferencia de saldo. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
