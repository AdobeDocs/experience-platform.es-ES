---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;dirección;xdm:dirección;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de elemento de lista de productos
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM del elemento de lista de productos.
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# [!UICONTROL Tipo de ] datos de la lista de productos

[!UICONTROL El ] elemento de lista de productos es un tipo de datos XDM estándar que describe un producto seleccionado por un cliente con opciones específicas, precios y contexto de uso para un punto de tiempo específico.

Los valores capturados en este tipo de datos pueden diferir del registro del producto. Por ejemplo, el registro de producto contiene detalles del sistema de información del producto que son coherentes para todos los clientes, donde el artículo de la lista de productos tiene el precio real ofrecido al cliente en el momento de la compra, que puede variar debido a campañas de ventas o precios de temporada.

![](../images/data-types/product-list-item.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `SKU` | [!UICONTROL Cadena] | Unidad de mantenimiento de existencias (SKU), el identificador único de un producto definido por el proveedor. |
| `_id` | [!UICONTROL Cadena] | Identificador de elemento de línea para esta entrada de producto. El producto en sí se identifica mediante `product`. |
| `currencyCode` | [!UICONTROL Cadena] | El código de divisa alfabética [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) utilizado para fijar el precio del producto. |
| `name` | [!UICONTROL Cadena] | Nombre para mostrar del producto tal como se presenta al usuario para esta vista de producto. |
| `priceTotal` | [!UICONTROL Duplicada] | El precio total del artículo de línea de producto. |
| `product` | [!UICONTROL Cadena]  (URI) | El URI `$id` del esquema XDM que captura el propio producto. |
| `productAddMethod` | [!UICONTROL Cadena] | Método que el visitante utilizó para agregar un elemento de producto a la lista. |
| `quantity` | [!UICONTROL Número entero] | Número de unidades que el cliente ha indicado que requiere del producto. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos de dirección postal, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
