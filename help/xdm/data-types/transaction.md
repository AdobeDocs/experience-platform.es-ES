---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;transacción;tipo de datos;tipo de datos;tipo de datos;
title: Tipo de datos de transacción
description: Este documento proporciona información general sobre el tipo de datos XDM (Transaction Experience Data Model).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 5%

---

# [!UICONTROL Transacción] tipo de datos

[!UICONTROL Transacción] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles de una transacción monetaria.

![Estructura de transacciones](../images/data-types/transaction.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Moneda]](./currency.md) | Describe la cantidad de moneda intercambiada como parte de la transacción. |
| `transactionDate` | [!UICONTROL DateTime] | Una marca de tiempo del momento en el que se produjo la transacción. |
| `transactionId` | [!UICONTROL Cadena] | Un identificador único de la transacción. |
| `transactionType` | [!UICONTROL Cadena] | El tipo de transacción que usa el visitante. |

{style="table-layout:auto"}
