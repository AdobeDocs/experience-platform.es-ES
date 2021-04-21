---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;pedido;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de pedido
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias de pedidos (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---

# [!UICONTROL Order] tipo de datos

[!UICONTROL Order] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe el orden colocado para una lista de productos.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `payments` | Matriz de [[!UICONTROL Payment Items]](./payment-item.md) | La lista de pagos para este pedido. |
| `currencyCode` | Cadena | El código de moneda ISO 4217 utilizado para los totales de pedidos. Todas las instancias deben cumplir la expresión regular `^[A-Z]{3}$`. Algunos ejemplos son `USD` y `EUR`. |
| `priceTotal` | Duplicada | El precio total de este pedido después de aplicar todos los descuentos e impuestos. |
| `purchaseID` | Cadena | Identificador único asignado por el vendedor para esta compra o contrato. Como esto lo define el vendedor, no hay garantía de que el ID sea único. |
| `purchaseOrderNumber` | Cadena | Identificador único asignado por el comprador para esta compra o contrato. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
