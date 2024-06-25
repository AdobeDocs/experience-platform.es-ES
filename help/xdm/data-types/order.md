---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;campos;esquemas;esquemas;orden;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos del pedido
description: Obtenga información sobre el tipo de datos del modelo de datos de experiencia de pedido (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL Pedido] tipo de datos

[!UICONTROL Pedido] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe el pedido realizado para una lista de productos.

![Un diagrama de la [!UICONTROL Pedido] tipo de datos.](../images/data-types/order.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| ID de compra | `purchaseID` | Cadena | Un identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único, ya que el ID lo define el vendedor. |
| Número del orden de compra | `purchaseOrderNumber` | Cadena | Un identificador único asignado por el comprador a esta compra o contrato. |
| Lista de pagos | `payments` | Matriz de [[!UICONTROL Elementos de pago]](./payment-item.md) | La lista de pagos de este pedido. Los pagos se detallan en la [!UICONTROL Elementos de pago] especificación. |
| Lista de reembolsos | `refunds` | Matriz de [[!UICONTROL Artículos de reembolso]](./refund-item.md) | La lista de reembolsos de este pedido. Los reembolsos se detallan en la [!UICONTROL Artículos de reembolso] especificación. |
| Información de retorno | `returns` | [[!UICONTROL Información de retorno]](./return.md) | La RMA (Autorización de Devolución de Mercancía) emitida. Las devoluciones se detallan en la [!UICONTROL Información de retorno] especificación. |
| Moneda | `currencyCode` | Cadena | El código de divisa en formato ISO 4217 usado para el total del pedido. Algunos ejemplos son `USD` y `EUR`. Todas las instancias deben coincidir con el patrón `^[A-Z]{3}$`. |
| Importe de impuestos | `taxAmount` | Número | El importe del impuesto pagado por el comprador como parte del pago final. |
| Importe de descuento | `discountAmount` | Número | La diferencia entre el precio normal y el precio especial se aplica a todo el pedido, en lugar de a productos individuales. |
| Precio total | `priceTotal` | Número | El precio total de este pedido después de aplicar todos los descuentos e impuestos. |
| Tipo de pedido | `orderType` | Cadena | El tipo de pedido que se ha realizado. Los valores posibles son `checkout` y `instant_purchase`. |
| Fecha de última actualización | `lastUpdatedDate` | Cadena | Hora a la que se actualiza por última vez un registro de pedido determinado en el sistema de comercio. Formato: fecha-hora. |
| Fecha de creación | `createdDate` | Cadena | La fecha y hora en que se crea un nuevo pedido en el sistema de comercio. Formato: fecha-hora. |
| Fecha de cancelación | `cancelDate` | Cadena | La fecha/hora en que el comprador inicia la cancelación de un pedido. Formato: fecha-hora. |
| Importe total reembolsado | `refundTotal` | Número | El importe total proporcionado en este reembolso en el pedido, combinando todos los artículos reembolsados y después de cualquier descuento, etc. se han aplicado. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
