---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;elemento de pago;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de artículo de pago
topic: overview
description: Este documento proporciona una visión general del tipo de datos del Modelo de datos de experiencia de artículo de pago (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 5%

---


# [!UICONTROL Tipo de ] datos de elementos de pago

[!UICONTROL Elementos ] de pago es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe un pago asociado a un pedido que define el tipo de pago, el importe y la moneda asociada.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `currencyCode` | Cadena | Código de moneda ISO 4217 utilizado para los totales del pedido. Todas las instancias deben cumplir la expresión regular `^[A-Z]{3}$`. Algunos ejemplos son `USD` y `EUR`. |
| `paymentAmount` | Duplicada | El valor del pago. |
| `paymentType` | Cadena | El método de pago para este pedido. Los valores de enumeración aceptados incluyen: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Cadena | Identificador de transacción único para este artículo de pago. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)