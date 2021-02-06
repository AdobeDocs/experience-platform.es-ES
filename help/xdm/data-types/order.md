---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;orden;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de pedido
topic: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de pedido (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de datos del pedido

 Pedidos es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe el pedido realizado para una lista de producto.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `payments` | Matriz de [[!UICONTROL elementos de pago]](./payment-item.md) | La lista de los pagos para este pedido. |
| `currencyCode` | Cadena | Código de moneda ISO 4217 utilizado para los totales del pedido. Todas las instancias deben cumplir la expresión regular `^[A-Z]{3}$`. Algunos ejemplos son `USD` y `EUR`. |
| `priceTotal` | Duplicada | El precio total de este pedido después de haber aplicado todos los descuentos e impuestos. |
| `purchaseID` | Cadena | Identificador único asignado por el vendedor para esta compra o contrato. Dado que esto lo define el vendedor, no hay garantía de que el ID sea único. |
| `purchaseOrderNumber` | Cadena | Identificador único asignado por el comprador para esta compra o contrato. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)