---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;esquemas;commerce;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de Commerce
description: Este documento proporciona información general sobre el tipo de datos del modelo de datos de experiencia comercial (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 3%

---

# [!UICONTROL Comercio] tipo de datos

[!UICONTROL Comercio] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los registros relacionados con la actividad de compra y venta.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `order` | [[!UICONTROL Pedido]](./order.md) | Describe el pedido realizado de uno o más productos. |
| `cartAbandons` | [[!UICONTROL Medida]](./measure.md) | Se utiliza para describir cuándo el usuario ha identificado una lista de productos como que ya no es accesible o no se puede comprar. |
| `checkouts` | [[!UICONTROL Medida]](./measure.md) | Una acción durante el proceso de cierre de compra de una lista de productos. Puede haber más de un evento de cierre de compra si hay varios pasos en el proceso. Si hay varios pasos, la información de la hora del evento y la página o experiencia de referencia se utilizan para identificar el paso y los eventos individuales representados en orden. |
| `inStorePurchase` | [[!UICONTROL Medida]](./measure.md) | Describe un valor asociado con una compra en tienda para uso de Analytics. |
| `productListAdds` | [[!UICONTROL Medida]](./measure.md) | Adición de un producto a la lista de productos; por ejemplo, un producto que se agrega a un carro de compras. |
| `productListOpens` | [[!UICONTROL Medida]](./measure.md) | Inicializaciones de una nueva lista de productos, como, por ejemplo, la creación de un carro de compras. |
| `productListRemovals` | [[!UICONTROL Medida]](./measure.md) | Eliminación o eliminaciones de una entrada de producto de una lista de productos; por ejemplo, un producto que se está eliminando de un carro de compras. |
| `productListReopens` | [[!UICONTROL Medida]](./measure.md) | Lista de productos abandonada anteriormente que el usuario ha reactivado. |
| `productListViews` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha producido una vista o vistas de una lista de productos. |
| `productViews` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha producido una vista o vistas de un producto individual. |
| `purchases` | [[!UICONTROL Medida]](./measure.md) | Se utiliza para registrar cuándo se ha aceptado un pedido. El evento de compra es la única acción necesaria en una conversión comercial. El evento de compra debe tener una lista de productos a la que se haga referencia. |
| `saveForLaters` | [[!UICONTROL Medida]](./measure.md) | Se guarda una lista de productos para su uso futuro, como una lista de artículos deseados. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
