---
title: Recopilación de información comercial y de producto mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo agregar datos relacionados con productos o un carro de compras mediante el SDK web de Adobe Experience Platform.
keywords: productos;comercio;medidas;medida;pedido;cartAbandons;cierres de compra;productListAdds;productListOpens;productListRemovals;productListReopens;productListViews;productViews;purchases;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# Recopilar información comercial y de productos

Si tiene productos en el sitio, este es un conjunto predeterminado de elementos que puede que desee enviar para habilitar la mayoría de las funciones desde el Adobe. Aunque esto es una sugerencia, proporciona un conjunto de datos muy sólido desde el principio.

Este documento usa el [Detalles comerciales de ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) grupo de campos de esquema. El `commerce` grupo de campos se divide en dos partes: la variable `commerce` y el objeto `productListItems` matriz. El `commerce` permite indicar qué acciones se están produciendo en el `productListItems` matriz.

>[!TIP]
>
>Si está familiarizado con Adobe Analytics, puede usar el `commerce` está más estrechamente relacionado con la variable `events` variable. El `productListItems` está más estrechamente relacionado con el `products` variable.

## Acciones relacionadas con los productos

A continuación se muestra una lista de `measures` disponible en el `commerce` objeto.

>[!TIP]
>
>Una medida tiene dos campos: `id` y `value`. La mayoría de las veces, utilizará el `value` solo de campo (por ejemplo, `'value':1`). El `id` Este campo le permite establecer un identificador único que puede utilizar para realizar un seguimiento del momento en el que se envió la medida. Consulte la documentación de XDM para [Medida](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Medida** | **Recomendación** | **Descripción** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Opcional | El usuario ya no puede comprar ni acceder al carro de compras. |
| [cierres](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Muy recomendado | Un usuario ya no está buscando productos, pero está en el proceso de comprar un producto. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Muy recomendado | Se agrega un producto a una lista. Asegúrese de configurar el producto en la `productListItems` al mismo tiempo. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Opcional | Se crea una nueva lista de productos. (Por ejemplo, se crea un nuevo carro de compras). |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Muy recomendado | Los productos se eliminan de las listas de productos. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Opcional | El usuario reactiva una lista de productos. Esto suele ocurrir en las campañas de remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Muy recomendado | Se muestra una lista de productos. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Muy recomendado | Se ha producido una vista de un producto. Asegúrese de configurar el producto visualizado en la `productListItems`. |
| [compras](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Muy recomendado | Se acepta una solicitud. Debe tener una lista de productos. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Opcional | Se ha guardado un producto para uso futuro. |

A continuación se muestra un ejemplo de cómo configuraría estos `Measures` en el SDK.

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

El objeto de comercio también tiene un campo especial para recopilar detalles de pedidos denominado `order`.

| **Pedido** | **Opción** | **Recomendación** | **Descripción** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | El [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) divisa del total del pedido. |
| [pagos[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | La lista de pagos de un pedido. A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) incluye lo siguiente. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Opcional | El [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) divisa de esta forma de pago. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Muy recomendado | El valor del pago en el código de divisa especificado. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Muy recomendado | El tipo de pago (por ejemplo, `credit_card`, `gift_card`, `paypal`). Consulte la lista de [valores conocidos](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) para obtener más información. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Opcional | Un ID único para esta transacción de pago. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Muy recomendado | El total de este pedido después de aplicar todos los descuentos e impuestos. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Muy recomendado | El identificador único asignado por el vendedor a esta compra. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Opcional | Un identificador único asignado por el comprador a esta compra. |

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
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Opcional | El [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) moneda para el producto. Esto solo es útil cuando puede tener productos con diferentes códigos de moneda y cuando se aplica. Por ejemplo, cuando hay una compra o una adición al carro de compras. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Muy recomendado | Solo debe configurarse cuando corresponda. Por ejemplo, es posible que no se pueda establecer en `productView` debido a que diferentes variaciones del producto pueden tener diferentes precios, pero en un `productListAdds` evento. |
| [producto](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Muy recomendado | ID de XDM para el producto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Muy recomendado | El método que el visitante utilizó para agregar un producto a la lista. Configurado con `productListAdds` medidas, y solo deben utilizarse cuando se añada un producto a la lista. Los ejemplos incluyen `add to cart button`, `quick add` y `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Muy recomendado | Se establece en el nombre para mostrar o en un nombre legible en lenguaje natural del producto. |
| [cantidad](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Muy recomendado | El número de unidades que el cliente ha indicado que necesita del producto. Debe configurarse en `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Muy recomendado | Almacén de la unidad. Es el identificador único del producto. |

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
