---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;transacción;tipo de datos;tipo de datos;tipo de datos;
title: Tipo de datos de transacción
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias de transacciones (XDM).
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 8%

---

#  Tipo de datos de transacción

 Transactionis es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles de una transacción monetaria.

![Estructura de las transacciones](../images/data-types/transaction.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Moneda]](./currency.md) | Describe la cantidad de moneda intercambiada como parte de la transacción. |
| `transactionDate` | [!UICONTROL DateTime] | Marca de fecha y hora del momento en que se produjo la transacción. |
| `transactionId` | [!UICONTROL Cadena] | Identificador único de la transacción. |
| `transactionType` | [!UICONTROL Cadena] | Tipo de transacción que utiliza el visitante. |

{style=&quot;table-layout:auto&quot;}
