---
title: Tipo de datos de la cuenta financiera
description: Este documento proporciona información general sobre el tipo de datos XDM de cuenta financiera.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 5%

---

# [!UICONTROL Cuenta financiera] tipo de datos

[!UICONTROL Cuenta financiera] es un tipo de datos XDM estándar que describe los detalles de una cuenta financiera, incluido su tipo, propietario y saldo actual.

![](../images/data-types/financial-account.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Moneda]](./currency.md) | El saldo actual de la cuenta. |
| `financialAccountId` | [!UICONTROL Cadena] | ID único de la cuenta. |
| `financialAccountName` | [!UICONTROL Cadena] | El nombre asignado a la cuenta. |
| `financialAccountType` | [!UICONTROL Cadena] | El tipo de cuenta financiera, como corriente, ahorros o jubilación. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
