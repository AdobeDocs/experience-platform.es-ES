---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;elemento de pago;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de artículo de pago
topic-legacy: overview
description: Este documento proporciona una descripción general del tipo de datos Modelo de datos de experiencia de artículo de pago (XDM).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 5%

---

# [!UICONTROL Payment Item] tipo de datos

[!UICONTROL Payment Item] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe un pago asociado a un pedido que define el tipo de pago, la cantidad y la moneda asociada.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `currencyCode` | Cadena | El código de moneda ISO 4217 utilizado para los totales de pedidos. Todas las instancias deben cumplir la expresión regular `^[A-Z]{3}$`. Algunos ejemplos son `USD` y `EUR`. |
| `paymentAmount` | Duplicada | El valor del pago. |
| `paymentType` | Cadena | Método de pago para esta orden. Los valores de enumeración aceptados incluyen: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Cadena | Identificador de transacción único para esta partida de pago. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
