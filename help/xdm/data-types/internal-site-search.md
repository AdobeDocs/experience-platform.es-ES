---
title: Internal Site Search Data Type
description: This document provides an overview of the Internal Site Search XDM data type.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# 



![](../images/data-types/internal-site-search.png)

| Propiedad | Data type | Descripción |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Boolean] | Indicates whether a visitor used a suggested or autocompleted search value to execute the search. |
| `autoCompleteTypedValue` | [!UICONTROL Cadena] | For autocomplete scenarios, users sometimes abandon their search and select a specific term from the dropdown. This value tracks what the user started to type in order to generate the specific set of suggested search terms. |
| `autoCompleteValue` | [!UICONTROL Cadena] | For autocomplete scenarios, users sometimes abandon their search and select a specific term from the dropdown menu. This value is used to track the specific terms selected. |
| `instances` | [!UICONTROL Número entero] | The number of times the internal site search occurred. |
| `locationInPage` | [!UICONTROL Cadena] | When multiple search boxes exist on the page, this value should be used to identify the specific location the user used to search. |
| `nullInstances` | [!UICONTROL Número entero] | The number of times the internal site search occurred that provided zero results. |
| `numberOfResults` | [!UICONTROL Número entero] | The total number of search results returned. |
| `postalCode` | [!UICONTROL Cadena] | The postal code used for the search, if applicable. |
| `productFindingMethods` | [!UICONTROL Cadena] | The internal site search term value with merchandising binding. This value indicates what term was searched for immediately before viewing a product. |
| `radiusDistance` | [!UICONTROL Número entero] | `radiusType` |
| `radiusType` | [!UICONTROL Número entero] | `radiusDistance` |
| `refinementInstances` | [!UICONTROL Número entero] | The number of times the internal site search was refined. |
| `refinementType` | Array of strings | Lists the refinement types applied to the search results. Examples include department, brand, price, in-store, review rating, color, material, and so on. |
| `refinementValue` | [!UICONTROL Cadena] | The value that the search was refined to. |
| `resultsPageNumber` | [!UICONTROL Número entero] | For paginated search results, this value tracks the page of results the visitor is viewing. |
| `resultsPerPage` | [!UICONTROL Número entero] | For paginated search results, this value tracks the number of search results displayed per page. |
| `searchType` | [!UICONTROL Cadena] | Captures the method of search being executed, if applicable. Examples could include a type-ahead search, directly typed search, or any other type of custom search functionality a site might have. |
| `sortOrder` | [!UICONTROL Cadena] | `sortType` |
| `term` | [!UICONTROL Cadena] | The internal site search term entered by the visitor. |

{style=&quot;table-layout:auto&quot;}

[](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json)
