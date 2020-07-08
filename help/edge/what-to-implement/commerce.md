---
title: Productos
seo-title: Productos de soporte con SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo agregar datos si tiene productos o un carro de compras con el SDK web Experience Platform
seo-description: Obtenga información sobre cómo agregar datos si tiene productos o un carro de compras con el SDK web Experience Platform
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 5%

---


# Productos

Si tiene productos en el sitio, este es un conjunto predeterminado de cosas que puede desear enviar para habilitar la mayor cantidad de funciones de Adobe. Aunque esta es una sugerencia, proporciona un conjunto muy sólido de datos desde el inicio.

Este documento utiliza la combinación Detalles [del comercio de](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent. La `commerce` mezcla se divide en dos partes: el `commerce` objeto y la `productListItems` matriz. El `commerce` objeto permite indicar qué acciones se están realizando en la `productListItems` matriz.

>[!TConsejo]
>
>
>Si está familiarizado con Adobe Analytics, el `commerce` está más relacionado con la `events` variable. El `productListItems` está más relacionado con la `products` variable.

## Acciones relacionadas con los productos

A continuación se muestra una lista de `measures` disponible en el `commerce` objeto.

>[!TConsejo]
>
>
>Una medida tiene dos campos: `id` y `value`. La mayoría de las veces, solo usará el `value` campo (por ejemplo, `'value':1`). El `id` campo permite establecer un identificador único que se puede utilizar para realizar un seguimiento del momento en que se envió la medida. Consulte la documentación de XDM para [Measure](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Medida** | **Recomendación** | **Descripción** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Opcional | El usuario ya no puede acceder a un carro de compras ni adquirirlo. |
| [cierres de compras](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Muy recomendado | Un usuario ya no está buscando productos, pero está en proceso de comprar un producto. |
| [productListAddits](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Muy recomendado | Se agrega un producto a una lista. Asegúrese de configurar el producto al `productListItems` mismo tiempo. |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Opcional | Se crea una nueva lista de producto. (Por ejemplo, se crea un nuevo carro de compras). |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Muy recomendado | Un producto se elimina de una lista de producto. |
| [productListReaperturas](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Opcional | El usuario reactiva una lista de producto. Esto suele ocurrir en campañas de remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Muy recomendado | Se ve una lista de productos. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Muy recomendado | Se produjo una vista de un producto. Asegúrese de configurar el producto visualizado en la `productListItems`. |
| [compras](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Muy recomendado | Se acepta un pedido. Debe tener una lista de producto. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Opcional | Un producto se guarda para su uso futuro. |

A continuación se muestra un ejemplo de cómo se configurarían `Measures` en el SDK.

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

El objeto de comercio también tiene un campo especial para recopilar los detalles del pedido llamados `order`.

| **Pedido** | **Opción** | **Recomendación** | **Descripción** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | Moneda [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) para el total del pedido. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | La lista de los pagos en un pedido. Un [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) incluye lo siguiente. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Opcional | Moneda [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) para este método de pago. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Muy recomendado | El valor del pago en el código de moneda especificado. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Muy recomendado | Tipo de pago (por ejemplo, `credit_card`, `gift_card`, `paypal`). Consulte la lista de valores [](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) conocidos para obtener más información. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Opcional | ID única para esta transacción de pago. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Muy recomendado | Total de este pedido después de aplicar todos los descuentos e impuestos. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Recomendado | Identificador único asignado por el vendedor para esta compra. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Opcional | Identificador único asignado por el comprador para esta compra. |

A continuación se muestra un ejemplo de una compra típica en el SDK.

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

La lista del producto indica qué productos están relacionados con la acción correspondiente. Es una lista de [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Cada producto tiene una serie de campos opcionales.

| **Campo** | **Recomendación** | **Descripción** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Opcional | La moneda [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) para el producto. Esto solo es útil cuando se pueden tener productos con diferentes códigos de moneda y cuando se aplica. Por ejemplo, cuando hay una compra o un complemento al carro de compras. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Muy recomendado | Sólo debe configurarse cuando proceda. Por ejemplo, puede que no sea posible establecer `productView` porque las diferentes variaciones del producto pueden tener precios diferentes pero en un `productListAdds`. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Muy recomendado | ID XDM del producto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Muy recomendado | El método que el visitante utilizó para agregar un elemento de producto a la lista. Se configura con `productListAdds` medidas y solo debe utilizarse cuando se agrega un producto a la lista. Examples include `add to cart button`, `quick add`, and `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Muy recomendado | Se establece en el nombre para mostrar o en el nombre legible en lenguaje natural del producto. |
| [cantidad](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Muy recomendado | Número de unidades que el cliente ha indicado que necesita del producto. Debe estar activado `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Muy recomendado | Unidad de mantenimiento de la tienda. Es el identificador único del producto. |

## Ejemplos

`productView` evento

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

`productView` evento

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

`checkout` evento

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

`purchase` evento

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
