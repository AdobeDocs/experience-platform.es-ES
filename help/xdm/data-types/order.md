---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;campos;esquemas;esquemas;orden;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos del pedido
description: Obtenga información sobre el tipo de datos del modelo de datos de experiencia de pedido (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---

# [!UICONTROL Pedido] tipo de datos

[!UICONTROL Pedido] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe el pedido realizado para una lista de productos.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `payments` | Matriz de [[!UICONTROL Elementos de pago]](./payment-item.md) | La lista de pagos de este pedido. |
| `currencyCode` | Cadena | El código de divisa en formato ISO 4217 usado para el total del pedido. Todas las instancias deben ajustarse a la expresión regular `^[A-Z]{3}$`. Algunos ejemplos son `USD` y `EUR`. |
| `priceTotal` | Doble | El precio total de este pedido después de aplicar todos los descuentos e impuestos. |
| `purchaseID` | Cadena | Un identificador único asignado por el vendedor a esta compra o contrato. Dado que el vendedor define esta opción, no hay garantía de que el ID sea único. |
| `purchaseOrderNumber` | Cadena | El identificador único asignado por el comprador a esta compra o contrato. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
