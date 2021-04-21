---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;comercio;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de comercio
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia comercial (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# [!UICONTROL Commerce] tipo de datos

[!UICONTROL Commerce] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los registros relacionados con la actividad de compra y venta.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `order` | [[!UICONTROL Order]](./order.md) | Describe el orden de uno o más productos. |
| `cartAbandons` | [[!UICONTROL Measure]](./measure.md) | Se utiliza para describir cuándo el usuario ha identificado una lista de productos como que ya no es accesible o no se puede adquirir. |
| `checkouts` | [[!UICONTROL Measure]](./measure.md) | Acción durante el proceso de cierre de compra de una lista de productos. Puede haber más de un evento de cierre de compra si hay varios pasos en un proceso de cierre de compra. Si hay varios pasos, la información de tiempo del evento y la página o experiencia a las que se hace referencia se utilizan para identificar el paso y los eventos individuales representados en orden. |
| `inStorePurchase` | [[!UICONTROL Measure]](./measure.md) | Describe un valor asociado con una compra en la tienda para uso de análisis. |
| `productListAdds` | [[!UICONTROL Measure]](./measure.md) | Adición de un producto a la lista de productos, como cuando se agrega un producto a un carro de compras. |
| `productListOpens` | [[!UICONTROL Measure]](./measure.md) | Inicializaciones de una nueva lista de productos, como la creación de un carro de compras. |
| `productListRemovals` | [[!UICONTROL Measure]](./measure.md) | Eliminación o eliminación de una entrada de producto de una lista de productos, como por ejemplo si un producto se elimina de un carro de compras. |
| `productListReopens` | [[!UICONTROL Measure]](./measure.md) | Lista de productos que anteriormente se abandonó y que el usuario ha reactivado. |
| `productListViews` | [[!UICONTROL Measure]](./measure.md) | Describe cuándo se ha producido una vista o vistas de una lista de productos. |
| `productViews` | [[!UICONTROL Measure]](./measure.md) | Describe cuándo se ha producido una vista o vistas de un producto individual. |
| `purchases` | [[!UICONTROL Measure]](./measure.md) | Se utiliza para rastrear cuándo se ha aceptado un pedido. El evento de compra es la única acción requerida en una conversión de comercio. El evento de compra debe tener una referencia a la lista de productos. |
| `saveForLaters` | [[!UICONTROL Measure]](./measure.md) | Se guarda una lista de productos para su uso futuro, como una lista de deseos. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
