---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;esquemas;commerce;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de Commerce
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia comercial (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!UICONTROL Comercio] tipo de datos

[!UICONTROL Comercio] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los registros relacionados con la compra y venta.

![Un diagrama de la [!UICONTROL Comercio] tipo de datos.](../images/data-types/commerce.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Pedido] | `order` | [[!UICONTROL Pedido]](./order.md) | Describe el pedido realizado de uno o más productos. |
| [!UICONTROL ID de promoción] | `promotionID` | [!UICONTROL cadena] | Identificador de promoción del pedido realizado, si existe. |
| [!UICONTROL Abandones del carro] | `cartAbandons` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha identificado una lista de productos como que el usuario ya no puede acceder a ella ni comprarla. |
| [!UICONTROL Cierres de compra] | `checkouts` | [[!UICONTROL Medida]](./measure.md) | Una acción durante el proceso de cierre de compra de una lista de productos. Puede haber más de un evento de cierre de compra si hay varios pasos en el proceso. Si hay varios pasos, la información de la hora del evento y la página o experiencia de referencia se utilizan para identificar el paso y los eventos individuales representados en orden. |
| [!UICONTROL La lista de productos agregados (carrito)] | `productListAdds` | [[!UICONTROL Medida]](./measure.md) | Adición de un producto a la lista de productos; por ejemplo, un producto que se agrega a un carro de compras. |
| [!UICONTROL Se abre la lista de productos (carrito)] | `productListOpens` | [[!UICONTROL Medida]](./measure.md) | Inicializaciones de una nueva lista de productos, como, por ejemplo, la creación de un carro de compras. |
| [!UICONTROL Eliminaciones de la lista de productos (carrito)] | `productListRemovals` | [[!UICONTROL Medida]](./measure.md) | Eliminación o eliminaciones de una entrada de producto de una lista de productos; por ejemplo, un producto que se está eliminando de un carro de compras. |
| [!UICONTROL Reaperturas de la lista de productos (carrito)] | `productListReopens` | [[!UICONTROL Medida]](./measure.md) | Lista de productos abandonada anteriormente que el usuario ha reactivado. |
| [!UICONTROL Vistas de lista de productos (carrito)] | `productListViews` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha producido una vista o vistas de una lista de productos.Vista o vistas de una lista de productos. |
| [!UICONTROL Vistas del producto] | `productViews` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha producido una vista o vistas de un producto individual. |
| [!UICONTROL Compras] | `purchases` | [[!UICONTROL Medida]](./measure.md) | Se utiliza para registrar cuándo se ha aceptado un pedido. El evento de compra es la única acción necesaria en una conversión comercial. El evento de compra debe tener una lista de productos a la que se haga referencia. |
| [!UICONTROL Guardar para más tarde] | `saveForLaters` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se guarda una lista de productos para uso futuro, como una lista de artículos deseados. |
| [!UICONTROL Compra en tienda] | `inStorePurchase` | [[!UICONTROL Medida]](./measure.md) | Indica una compra &quot;en tienda&quot;. Esta información se guarda para su uso en análisis. |
| [!UICONTROL Carrito] | `cart` | [[!UICONTROL carrito]](./cart.md) | Las propiedades del carro de compras que contiene uno o más productos. |
| [!UICONTROL Envío] | `shipping` | [[!UICONTROL envío]](./shipping.md) | Los detalles de envío de uno o más productos. |
| [!UICONTROL Facturación] | `billing` | [[!UICONTROL facturación]](#billing) | Los detalles de facturación de uno o más pagos. |
| [!UICONTROL Compra instantánea] | `instantPurchase` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha comprado un producto al instante, lo que podría omitir el carrito o el cierre de compra. |
| [!UICONTROL Aperturas de lista de solicitudes] | `requisitionListOpens` | [[!UICONTROL Medida]](./measure.md) | Indica la inicialización de una nueva lista de solicitudes. |
| [!UICONTROL Eliminaciones de lista de solicitudes] | `requisitionListDeletes` | [[!UICONTROL Medida]](./measure.md) | Indica la eliminación de la lista de solicitudes. |
| [!UICONTROL Adiciones de lista de solicitud] | `requisitionListAdds` | [[!UICONTROL Medida]](./measure.md) | Indica la adición de un producto a una lista de solicitudes. |
| [!UICONTROL Eliminaciones de lista de solicitudes] | `requisitionListRemovals` | [[!UICONTROL Medida]](./measure.md) | Indica la eliminación de un producto de una lista de productos de solicitud. |
| [!UICONTROL Lista de solicitudes] | `requisitionList` | [[!UICONTROL requisador]](./requisition-list.md) | Las propiedades de la lista de solicitudes creada por el cliente. |
| [!UICONTROL Ámbito] | `commerceScope` | [[!UICONTROL ámbito comercial]](./commerce-scope.md) | Los identificadores de ámbito comercial de dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |

{style="table-layout:auto"}

## [!UICONTROL facturación] tipo de datos {#billing}

[!UICONTROL facturación] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene información sobre detalles de facturación. Específicamente, se centra en la dirección de facturación.

![Un diagrama del tipo de datos de facturación.](../images/data-types/billing.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Dirección de facturación] | `address` | [[!UICONTROL Dirección postal]](./postal-address.md) | La dirección de facturación. |

{style="table-layout:auto"}

Para obtener más información sobre [!UICONTROL Comercio] Tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
