---
title: Product Class
description: This document provides an overview of the Product class in Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 12%

---

# 



![](../images/classes/product.png)

| Propiedad | Data type | Descripción |
| --- | --- | --- |
| `productListPrice` | [Moneda](../data-types/currency.md) | Describes the default price of the product before sales and discounting. |
| `_id` | Cadena | A unique, system-generated string identifier for the record. This field is used to track the uniqueness of an individual record, prevent duplication of data, and to look up that record in downstream services.<br><br> However, you can still opt to supply your own unique ID values if you wish. |
| `productDescription` | Cadena | A description of the product. |
| `productID` | Cadena | A unique identifier for the product. |
| `productLastModifiedDate` | DateTime | [](https://datatracker.ietf.org/doc/html/rfc3339) |
| `productManufacturedDate` | DateTime | [](https://datatracker.ietf.org/doc/html/rfc3339) |
| `productName` | Cadena | Nombre del producto. |
| `productRating` | Cadena | The customer review rating of the product. |

{style=&quot;table-layout:auto&quot;}

## Compatible field groups {#field-groups}

[!DNL XDM Individual Profile] The following is a list of some commonly used field groups for the class:

* [](../field-groups/product/product-catalog.md)
* [](../field-groups/product/product-category.md)
