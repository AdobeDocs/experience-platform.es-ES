---
title: Clase de producto
description: Este documento proporciona información general sobre la clase Product en Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 12%

---

# [!UICONTROL Product] class

En el Modelo de datos de experiencia (XDM), la variable [!UICONTROL Product] captura el conjunto mínimo de propiedades que definen un producto minorista.

![](../images/classes/product.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `productListPrice` | [Moneda](../data-types/currency.md) | Describe el precio predeterminado del producto antes de ventas y descuentos. |
| `_id` | Cadena | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo se genera a partir del sistema, no se proporciona un valor explícito durante el consumo de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `productDescription` | Cadena | Descripción del producto. |
| `productID` | Cadena | Identificador único del producto. |
| `productLastModifiedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) marca de tiempo de la última modificación de este producto para cualquier actualización. |
| `productManufacturedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) marca de tiempo de la creación de este producto. |
| `productName` | Cadena | Nombre del producto. |
| `productRating` | Cadena | Clasificación de cliente del producto. |

{style=&quot;table-layout:auto&quot;}

## Grupos de campos compatibles {#field-groups}

Adobe proporciona varios grupos de campos estándar para su uso con la variable [!UICONTROL Product] Clase . A continuación se muestra una lista de algunos grupos de campos que se utilizan con más frecuencia para la clase :

* [[!UICONTROL Catálogo de productos]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoría del producto]](../field-groups/product/product-category.md)
