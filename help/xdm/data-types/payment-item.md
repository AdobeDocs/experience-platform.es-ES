---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;elemento de pago;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de elemento de pago
description: Obtenga información sobre el tipo de datos Modelo de datos de experiencia (XDM) de artículo de pago.
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 7%

---

# [!UICONTROL Elemento de pago] tipo de datos

[!UICONTROL Elemento de pago] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe un pago asociado a un pedido y que define el tipo de pago, el importe y la moneda asociada.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `currencyCode` | Cadena | El código de divisa en formato ISO 4217 usado para el total del pedido. Todas las instancias deben ajustarse a la expresión regular `^[A-Z]{3}$`. Algunos ejemplos son `USD` y `EUR`. |
| `paymentAmount` | Doble | El valor del pago. |
| `paymentType` | Cadena | El método de pago de este pedido. Los valores de enumeración aceptados incluyen: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Cadena | El identificador único de transacción de este elemento de pago. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
