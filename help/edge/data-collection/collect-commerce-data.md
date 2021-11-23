---
title: Recopilación de información comercial y de producto mediante el SDK web de Adobe Experience Platform
description: Aprenda a añadir datos relacionados con productos o un carro de compras mediante el SDK web de Adobe Experience Platform.
keywords: products;comercio;medidas;medida;pedido;cartAbandons;cierres de compra;productListAdd;productListOpens;productListRemovals;productListReopens;productListViews;productViews;compras;saveForLaters;currencyCode;pagos;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 22d15dde62f3113167684c7a76a2265e6f0e7bab
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 6%

---

# Recopilar información comercial y de producto

Si tiene productos en el sitio, este es un conjunto predeterminado de cosas que puede querer enviar para habilitar el máximo número de funcionalidades desde el Adobe. Aunque se trata de una sugerencia, proporciona un conjunto de datos muy sólido desde el principio.

Este documento utiliza la variable [Detalles comerciales de ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) grupo de campos de esquema. La variable `commerce` el grupo de campos se divide en dos partes: el `commerce` y `productListItems` matriz. La variable `commerce` El objeto permite indicar qué acciones están sucediendo con el `productListItems` matriz.

>[!TIP]
>
>Si está familiarizado con Adobe Analytics, la variable `commerce` está más estrechamente relacionado con el `events` variable. La variable `productListItems` está más estrechamente relacionado con el `products` variable.

## Acciones relacionadas con los productos

A continuación se muestra una lista de `measures` disponible en el `commerce` objeto.

>[!TIP]
>
>Una medida tiene dos campos: `id` y `value`. La mayoría de las veces, utilizará la variable `value` solo campo (por ejemplo, `'value':1`). La variable `id` permite establecer un identificador único que se puede utilizar para realizar un seguimiento del momento en que se envió la medida. Consulte la documentación de XDM para [Medida](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Medida** | **Recomendación** | **Descripción** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Opcional | El usuario ya no puede acceder ni comprar un carro de compras. |
| [cierres de compra](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Muy recomendado | Un usuario ya no está buscando productos, pero está en proceso de adquirir un producto. |
| [productListAdd](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Muy recomendado | Un producto se añade a una lista. Asegúrese de establecer el producto en la variable `productListItems` al mismo tiempo. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Opcional | Se crea una nueva lista de productos. (Por ejemplo, se crea un nuevo carro de compras). |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Muy recomendado | Un producto se elimina de una lista de productos. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Opcional | El usuario reactiva una lista de productos. Esto suele ocurrir en campañas de remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Muy recomendado | Se ve una lista de productos. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Muy recomendado | Se ha producido una vista de un producto. Asegúrese de establecer el producto visualizado en la variable `productListItems`. |
| [compras](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Muy recomendado | Se acepta un pedido. Debe tener una lista de productos. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Opcional | Un producto se guarda para uso futuro. |

A continuación, se muestra un ejemplo de cómo configurar estas `Measures` en el SDK.

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

El objeto commerce también tiene un campo especial para recopilar detalles de pedidos llamados `order`.

| **Pedido** | **Opción** | **Recomendación** | **Descripción** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | La variable [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) moneda para el total del pedido. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | La lista de pagos de un pedido. A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) incluye lo siguiente: |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Opcional | La variable [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) para este método de pago. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Muy recomendado | El valor del pago en el código de moneda especificado. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Muy recomendado | El tipo de pago (por ejemplo, `credit_card`, `gift_card`, `paypal`). Consulte la lista de [valores conocidos](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) para obtener más información. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Opcional | Un ID exclusivo para esta transacción de pago. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Muy recomendado | El total de este pedido después de aplicar todos los descuentos e impuestos. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Muy recomendado | Identificador único asignado por el vendedor para esta compra. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Opcional | Identificador único asignado por el comprador para esta compra. |

A continuación, se muestra un ejemplo de una compra típica en el SDK.

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

## Listas de productos

La lista de productos indica qué productos están relacionados con la acción correspondiente. Es una lista de [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Cada producto tiene una serie de campos opcionales.

| **Campo** | **Recomendación** | **Descripción** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Opcional | La variable [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) moneda para el producto. Esto solo es útil cuando se pueden tener productos con diferentes códigos de moneda y cuando se aplican. Por ejemplo, cuando hay una compra o un anuncio al carro de compras. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Muy recomendado | Solo debe configurarse cuando corresponda. Por ejemplo, es posible que no sea posible establecer en `productView` porque las diferentes variaciones del producto pueden tener precios diferentes pero en un `productListAdds`. |
| [producto](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Muy recomendado | ID XDM para el producto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Muy recomendado | Método que el visitante utilizó para agregar un elemento de producto a la lista. Configure con `productListAdds` y solo debe usarse cuando se agrega un producto a la lista. Los ejemplos incluyen `add to cart button`, `quick add` y `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Muy recomendado | Se establece en el nombre para mostrar o en el nombre legible en lenguaje natural del producto. |
| [cantidad](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Muy recomendado | Número de unidades que el cliente ha indicado que requiere del producto. Debe configurarse en `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Muy recomendado | Conservar unidad de mantenimiento. Es el identificador único del producto. |

## Ejemplos

`productViews` evento

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

`productListAdds` evento

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

`checkouts` evento

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

`order` evento

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
