---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;dirección;xdm:address;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos del elemento de lista de productos
description: Obtenga información sobre el tipo de datos XDM del elemento de lista de productos.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 18%

---

# [!UICONTROL Tipo de datos del elemento de lista de productos]

[!UICONTROL Elemento de lista de productos] es un tipo de datos XDM estándar que describe un producto seleccionado por un cliente con opciones, precios y contexto de uso específicos para un punto de tiempo específico.

Los valores capturados en este tipo de datos pueden diferir del registro del producto. Por ejemplo, el registro del producto contiene detalles del sistema de información del producto que son coherentes con todos los clientes, donde el artículo de la lista del producto tiene el precio real ofrecido al cliente en el momento de la compra, que puede variar debido a campañas de ventas o precios estacionales.

![](../images/data-types/product-list-item.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `selectedOptions` | Matriz de objetos | Contiene opciones personalizadas seleccionadas para un producto configurable. Cada elemento de la lista es un objeto con las siguientes propiedades:<ul><li>`attribute`: nombre del atributo configurable.</li><li>`value`: valor del atributo.</li></ul> |
| `SKU` | [!UICONTROL Cadena] | SKU (código de referencia), el identificador único de un producto definido por el proveedor. |
| `_id` | [!UICONTROL Cadena] | El elemento de línea de esta entrada de producto. El producto en sí se identifica mediante `product`. |
| `currencyCode` | [!UICONTROL Cadena] | El [código alfabético de la divisa en formato ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) usado para poner el precio al producto. |
| `discountAmount` | [!UICONTROL Doble] | Si se descuenta el producto, esto representa la diferencia entre el precio normal y el precio especial del producto. |
| `name` | [!UICONTROL Cadena] | El nombre para mostrar del producto tal y como se presenta al usuario en esta vista de producto. |
| `priceTotal` | [!UICONTROL Doble] | El precio total de la línea de producto. |
| `product` | [!UICONTROL Cadena] (URI) | URI `$id` del esquema XDM que captura el producto en sí. |
| `productAddMethod` | [!UICONTROL Cadena] | El método que el visitante utilizó para agregar un producto a la lista. |
| `productImageUrl` | [!UICONTROL Cadena] | Una URL para la imagen principal del producto. |
| `quantity` | [!UICONTROL Entero] | El número de unidades que el cliente ha indicado que necesita del producto. |
| `unitOfMeasureCode` | [!UICONTROL Cadena] | El [código de unidad de medida](https://ucum.org/ucum) estándar para el producto relacionado con la propiedad `quantity`. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos de la dirección postal, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
