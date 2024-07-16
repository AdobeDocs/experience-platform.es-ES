---
title: Tipo de datos de la cuenta financiera
description: Obtenga información sobre el tipo de datos XDM de cuenta financiera.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 8%

---

# [!UICONTROL Tipo de datos de la cuenta financiera]

[!UICONTROL Cuenta financiera] es un tipo de datos XDM estándar que describe los detalles de una cuenta financiera, incluido su tipo, propietario y saldo actual.

![](../images/data-types/financial-account.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Moneda]](./currency.md) | El saldo actual de la cuenta. |
| `financialAccountId` | [!UICONTROL Cadena] | ID único de la cuenta. |
| `financialAccountName` | [!UICONTROL Cadena] | El nombre asignado a la cuenta. |
| `financialAccountType` | [!UICONTROL Cadena] | El tipo de cuenta financiera, como corriente, ahorros o jubilación. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
