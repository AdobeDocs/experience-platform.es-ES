---
title: Quote Request Details Schema Field Group
description: This document provides an overview of the Quote Request Details schema field group.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 6%

---

# 

[[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) `quotes`

![](../../images/field-groups/quote-request-details.png)

| Propiedad | Data type | Descripción |
| --- | --- | --- |
| `discount` | [[!UICONTROL Moneda]](../../data-types/currency.md) | The discount amount for a quote displayed to a visitor. |
| `premium` | [[!UICONTROL Moneda]](../../data-types/currency.md) | The premium amount for a quote displayed to a visitor. |
| `location` | [!UICONTROL Cadena] | The postal code used for finding retailers near the visitor&#39;s location. |
| `requestID` | [!UICONTROL Cadena] | A unique identifier for the quote request. |
| `selectedRetailer` | [!UICONTROL Cadena] | The selected retailer for the quote request, if applicable. |

{style=&quot;table-layout:auto&quot;}

[](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json)
