---
title: Recopilar información de comercio, productos y pedidos mediante Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo agregar datos relacionados con productos o un carro de compras mediante Adobe Experience Platform Web SDK.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# Recopilar información comercial, de productos y de pedidos

Si su organización vende productos o servicios, puede utilizar esta página como guía sobre cómo rastrear esos productos y servicios.

Esta página utiliza el grupo de campos XDM [Esquema de Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md).

Este grupo de campos consta de dos partes principales:

* El objeto `commerce`. Este objeto le permite indicar qué acciones suceden a la matriz `productListItems`.
* La matriz `productListItems`.

>[!TIP]
>
>Si está familiarizado con Adobe Analytics, el objeto `commerce` contiene datos similares a los eventos de comercio en la variable `events`. La matriz de objetos `productListItems` contiene datos similares a la variable `products`.

## El objeto `commerce` {#commerce-object}

Esta sección describe los campos disponibles en el objeto `commerce`.

>[!TIP]
>
>Una medida tiene dos campos: `id` y `value`. La mayoría de las veces, solo utiliza el campo `value` (por ejemplo, `'value':1`). El campo `id` le permite establecer un identificador único para el seguimiento de cuándo se envió la medida. Consulte la documentación de XDM para [Measure](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) para obtener más información.

| Medida | Recomendación | Descripción |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Opcional | El usuario ya no puede comprar ni acceder al carro de compras. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Muy recomendado | Un usuario ya no está buscando productos, pero está en el proceso de comprar un producto. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Muy recomendado | Se agrega un producto a una lista. Asegúrese de establecer el producto en `productListItems` al mismo tiempo. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Opcional | Se crea una nueva lista de productos. Por ejemplo, se crea un nuevo carro de compras. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Muy recomendado | Los productos se eliminan de las listas de productos. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Opcional | El usuario reactiva una lista de productos. Esta acción suele ocurrir en campañas de remarketing. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Muy recomendado | Se muestra una lista de productos. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Muy recomendado | Se produjo una vista de un producto. Asegúrese de establecer el producto visualizado en `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Muy recomendado | Se acepta una solicitud. Debe tener una lista de productos. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Opcional | Se ha guardado un producto para uso futuro. |

{style="table-layout:auto"}

### `Commerce` ejemplos de objeto

Expanda la sección siguiente para ver un ejemplo de un comando de Web SDK con un campo del objeto `commerce`.

+++`productViews`

Una llamada básica de Web SDK `sendEvent` que establece el campo `productViews` en `1`:

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

+++

## El objeto `order` {#order-object}

El objeto `commerce` contiene un objeto dedicado para recopilar detalles de pedidos. Se denomina objeto `order`.

En esta sección se describen todos los campos admitidos por el objeto `order`.

| Campo | Opción | Recomendación | Descripción |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | La divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) para el total del pedido. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | La lista de pagos de un pedido. Un [elemento de pago](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) incluye lo siguiente. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Opcional | La divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) para este método de pago. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Muy recomendado | El valor del pago en el código de divisa especificado. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Muy recomendado | El tipo de pago (por ejemplo, `credit_card`, `gift_card`, `paypal`). Consulte la lista de [valores conocidos](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) para obtener detalles. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Opcional | Un ID único para esta transacción de pago. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Muy recomendado | El total de este pedido después de aplicar todos los descuentos e impuestos. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Muy recomendado | El identificador único asignado por el vendedor a esta compra. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Opcional | Un identificador único asignado por el comprador a esta compra. |

### Ejemplos de objetos de pedidos

Expanda la sección siguiente para ver un ejemplo de un comando de Web SDK que utiliza el objeto `commerce`.

+++Ejemplo de objeto `Order`

Una llamada de Web SDK `sendEvent` que establece el objeto `order` que se aplica a varios productos de la matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

+++

## El objeto de lista de productos {#product-list-object}

La lista de productos indica qué productos están relacionados con la acción correspondiente. Es una lista de [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Cada producto tiene varios campos opcionales.

| Campo | Recomendación | Descripción |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Opcional | La divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) del producto. Por lo general, este campo solo se aplica cuando hay varios productos en la lista de productos con códigos de moneda diferentes. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Muy recomendado | Establezca este campo solo cuando corresponda. Por ejemplo, es posible que no se pueda establecer en el evento `productView` porque distintas variaciones del producto pueden tener precios diferentes pero en un evento `productListAdds`. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Muy recomendado | ID de XDM para el producto. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Muy recomendado | El método que el visitante utilizó para agregar un producto a la lista. Se configura con `productListAdds` medidas y solo se usa cuando se agrega un producto a la lista. Algunos ejemplos son `add to cart button`, `quick add` y `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Muy recomendado | El nombre para mostrar o el nombre en lenguaje natural del producto. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Muy recomendado | El número de unidades que el cliente ha indicado que necesita del producto. Debe establecerse en `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Muy recomendado | Almacén de la unidad. Es el identificador único del producto. |

### Ejemplos de listas de productos

Expanda las secciones siguientes para ver ejemplos de comandos de Web SDK que utilizan el objeto `productListItems`.

+++Ejemplo de `productListItems`

Una llamada de Web SDK `sendEvent` que configura `productViews` para varios productos en la matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

+++

+++Ejemplo de `productListAdds`

Una llamada de Web SDK `sendEvent` que configura el evento `productListAdds` para varios productos en la matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

+++

+++Ejemplo de `checkouts`

Una llamada de Web SDK `sendEvent` que configura el evento `checkouts` para varios productos en la matriz `productListItems`:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

+++
