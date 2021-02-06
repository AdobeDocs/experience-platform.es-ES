---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;comercio;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de comercio
topic: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias comerciales (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 3%

---


# [!UICONTROL Tipo ] de datos de comercio

[!UICONTROL El ] comercio es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los registros relacionados con la actividad de compra y venta.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `order` | [[!UICONTROL Pedido]](./order.md) | Describe el pedido realizado para uno o más productos. |
| `cartAbandons` | [[!UICONTROL Medida]](./measure.md) | Se utiliza para describir cuándo el usuario ha identificado que una lista de producto ya no es accesible ni puede comprar. |
| `checkouts` | [[!UICONTROL Medida]](./measure.md) | Acción durante el proceso de cierre de compra de una lista de producto. Puede haber más de un evento de cierre de compra si hay varios pasos en un proceso de cierre de compra. Si hay varios pasos, la información de tiempo de evento y la página o experiencia a la que se hace referencia se utilizan para identificar el paso y los eventos individuales representados en orden. |
| `inStorePurchase` | [[!UICONTROL Medida]](./measure.md) | Describe un valor asociado con una compra en el almacén para uso de análisis. |
| `productListAdds` | [[!UICONTROL Medida]](./measure.md) | La adición de un producto a la lista del producto, como un producto que se agrega al carro de compras. |
| `productListOpens` | [[!UICONTROL Medida]](./measure.md) | Inicializaciones de una nueva lista de producto, como un carro de compras que se está creando. |
| `productListRemovals` | [[!UICONTROL Medida]](./measure.md) | Eliminación o eliminación de una entrada de producto de una lista de producto, como por ejemplo la eliminación de un producto del carro de compras. |
| `productListReopens` | [[!UICONTROL Medida]](./measure.md) | Una lista de producto que se abandonó anteriormente y que el usuario ha reactivado. |
| `productListViews` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha producido una vista o vistas de una lista de producto. |
| `productViews` | [[!UICONTROL Medida]](./measure.md) | Describe cuándo se ha producido una vista o vistas de un producto individual. |
| `purchases` | [[!UICONTROL Medida]](./measure.md) | Se utiliza para rastrear cuándo se ha aceptado un pedido. El evento de compra es la única acción requerida en una conversión de comercio. El evento de compra debe tener una lista de producto referenciada. |
| `saveForLaters` | [[!UICONTROL Medida]](./measure.md) | Una lista de producto se guarda para un uso futuro, como una lista deseada. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)