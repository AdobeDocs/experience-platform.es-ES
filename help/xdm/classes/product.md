---
title: Clase de producto
description: Obtenga información acerca de la clase de producto en el modelo de datos de Experience (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---

# [!UICONTROL Product] clase

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Product] captura el conjunto mínimo de propiedades que definen un producto comercial.

![](../images/classes/product.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `productListPrice` | [Moneda](../data-types/currency.md) | Describe el precio predeterminado del producto antes de rebajas y descuentos. |
| `_id` | Cadena | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no se le proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `productDescription` | Cadena | Una descripción del producto. |
| `productID` | Cadena | Un identificador único del producto. |
| `productLastModifiedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) marca de tiempo de la última modificación de este producto para cualquier actualización. |
| `productManufacturedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) marca de tiempo del momento en el que se creó este producto. |
| `productName` | Cadena | Nombre del producto. |
| `productRating` | Cadena | La clasificación de revisión del cliente del producto. |

{style="table-layout:auto"}

## Grupos de campos compatibles {#field-groups}

El Adobe proporciona varios grupos de campos estándar para su uso con el [!UICONTROL Product] clase. A continuación se muestra una lista de algunos grupos de campos utilizados comúnmente para la clase:

* [[!UICONTROL Catálogo de productos]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoría de producto]](../field-groups/product/product-category.md)
