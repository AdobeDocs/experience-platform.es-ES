---
title: Recopilar información de comercio, productos y pedidos mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo agregar datos relacionados con productos o un carro de compras mediante el SDK web de Adobe Experience Platform.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# Recopilar información comercial, de productos y de pedidos

Si su organización vende productos o servicios, puede utilizar esta página como guía sobre cómo rastrear esos productos y servicios.

Esta página utiliza el XDM [Esquema de Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) grupo de campos.

Este grupo de campos consta de dos partes principales:

* El `commerce` objeto. Este objeto permite indicar qué acciones se producen en el `productListItems` matriz.
* El `productListItems` matriz.

>[!TIP]
>
>Si está familiarizado con Adobe Analytics, la variable `commerce` contiene datos similares a eventos de comercio en el `events` variable. El `productListItems` la matriz de objetos contiene datos similares a los de `products` variable.

## El `commerce` objeto {#commerce-object}

Esta sección describe los campos disponibles en la variable `commerce` objeto.

>[!TIP]
>
>Una medida tiene dos campos: `id` y `value`. La mayoría de las veces, solo se utiliza el `value` field (por ejemplo, `'value':1`). El `id` Este campo permite establecer un identificador único para el seguimiento del envío de la medida. Consulte la documentación de XDM para [Medida](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) para obtener más información.

| Medida | Recomendación | Descripción |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Opcional | El usuario ya no puede comprar ni acceder al carro de compras. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Muy recomendado | Un usuario ya no está buscando productos, pero está en el proceso de comprar un producto. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Muy recomendado | Se agrega un producto a una lista. Asegúrese de configurar el producto en la `productListItems` al mismo tiempo. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Opcional | Se crea una nueva lista de productos. Por ejemplo, se crea un nuevo carro de compras. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Muy recomendado | Los productos se eliminan de las listas de productos. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Opcional | El usuario reactiva una lista de productos. Esta acción suele ocurrir en campañas de remarketing. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Muy recomendado | Se muestra una lista de productos. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Muy recomendado | Se produjo una vista de un producto. Asegúrese de configurar el producto visualizado en la `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Muy recomendado | Se acepta una solicitud. Debe tener una lista de productos. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Opcional | Se ha guardado un producto para uso futuro. |

{style="table-layout:auto"}

### `Commerce` ejemplos de objeto

Expanda la sección siguiente para ver un ejemplo de un comando del SDK web que utiliza un campo del `commerce` objeto.

+++`productViews`

Un SDK web básico `sendEvent` llamada configurar el `productViews` field a `1`:

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

## El `order` objeto {#order-object}

El `commerce` contiene un objeto dedicado para recopilar detalles de pedidos. Esto se denomina `order` objeto.

En esta sección se describen todos los campos admitidos por la variable `order` objeto.

| Campo | Opción | Recomendación | Descripción |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | El [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) divisa del total del pedido. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | La lista de pagos de un pedido. A [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) incluye lo siguiente. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Opcional | El [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) divisa de esta forma de pago. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Muy recomendado | El valor del pago en el código de divisa especificado. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Muy recomendado | El tipo de pago (por ejemplo, `credit_card`, `gift_card`, `paypal`). Consulte la lista de [valores conocidos](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) para obtener más información. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Opcional | Un ID único para esta transacción de pago. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Muy recomendado | El total de este pedido después de aplicar todos los descuentos e impuestos. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Muy recomendado | El identificador único asignado por el vendedor a esta compra. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Opcional | Un identificador único asignado por el comprador a esta compra. |

### Ejemplos de objetos de pedidos

Expanda la sección siguiente para ver un ejemplo de un comando del SDK web que utiliza el `commerce` objeto.

+++`Order` ejemplo de objeto

Un SDK web `sendEvent` llamada configurar el `order` que se aplica a varios productos de la `productListItems` matriz:

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
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Opcional | El [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) la moneda del producto. Por lo general, este campo solo se aplica cuando hay varios productos en la lista de productos con códigos de moneda diferentes. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Muy recomendado | Establezca este campo solo cuando corresponda. Por ejemplo, es posible que no se pueda establecer en `productView` debido a que diferentes variaciones del producto pueden tener diferentes precios, pero en un `productListAdds` evento. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Muy recomendado | ID de XDM para el producto. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Muy recomendado | El método que el visitante utilizó para agregar un producto a la lista. Configurado con `productListAdds` y solo se utiliza cuando se añade un producto a la lista. Los ejemplos incluyen `add to cart button`, `quick add` y `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Muy recomendado | El nombre para mostrar o el nombre en lenguaje natural del producto. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Muy recomendado | El número de unidades que el cliente ha indicado que necesita del producto. Debe configurarse en `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`, etc. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Muy recomendado | Almacén de la unidad. Es el identificador único del producto. |

### Ejemplos de listas de productos

Expanda las secciones siguientes para ver ejemplos de comandos del SDK web que utilizan `productListItems` objeto.

+++`productListItems` ejemplo

Un SDK web `sendEvent` llamada configurar el `productViews` para varios productos en la `productListItems` matriz:

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

+++`productListAdds` ejemplo

Un SDK web `sendEvent` llamada configurar el `productListAdds` evento para varios productos en la `productListItems` matriz:

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

+++`checkouts` ejemplo

Un SDK web `sendEvent` llamada configurar el `checkouts` evento para varios productos en la `productListItems` matriz:

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
