---
solution: Experience Platform
title: Financial Services Industry Data Model ERD
topic-legacy: overview
description: View an entity relationship diagram (ERD) that describes a standardized data model for the banking, financial services, and insurance (BFSI) industry. This data model is compatible with Experience Data Model (XDM) for use in Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 345380c9d4e371bc90acee1f35e75f9da8f9394e
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# 

The following entity relationship diagram (ERD) represents a standardized data model for the banking, financial services, and insurance (BFSI) industry. The ERD is intentionally presented in a de-normalized fashion and with consideration for how data is stored in Adobe Experience Platform.

>[!NOTE]
>
>The ERD as described is a recommendation for how you should model your data for this industry use case. To make use of this data model in Platform, you must construct the recommended schemas and their relationships yourself. [](../../ui/resources/schemas.md)[](../../tutorials/relationship-ui.md)

Use the following legend to interpret this ERD:

* [](../composition.md#class)
* ****
* The most important fields for a given entity are highlighted in red.
* All the properties that could be used to identify individual customers are marked as &quot;identity&quot;, with one of these properties marked as a &quot;primary identity&quot;.
* Entity relationships are marked as non-dependent, since cookie-based events often cannot determine the person or individual who did the transaction.

![](../../images/industries/financial.png)

>[!NOTE]
>
>`_id` [](../../classes/experienceevent.md)

## 

The following table outlines the recommended classes and schema field groups for several common financial use cases.

| Caso de uso | Recommended classes and field groups |
| --- | --- |
| Drive personalization at scale for preferred segments through omnichannel reporting insights and automating journeys to increase enrollment to a preferred rewards program. | <ul><li>**[[!UICONTROL Producto]](../../classes/product.md)**:<ul><li>[](../../field-groups/product/product-category.md)</li></ul></li><li>**[](../../classes/experienceevent.md)**<ul><li>[](../../field-groups/event/card-actions.md)</li><li>[](../../field-groups/event/quote-request-details.md)</li><li>[](../../field-groups/event/deposit-details.md)</li><li>[](../../field-groups/event/channel-details.md)</li><li>[](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[](../../classes/individual-profile.md)**<ul><li>[](../../field-groups/profile/demographic-details.md)</li><li>[](../../field-groups/profile/personal-contact-details.md)</li><li>[](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimize cross-channel personalization across online and offline channels. | <ul><li>**[[!UICONTROL Producto]](../../classes/product.md)**:<ul><li>[](../../field-groups/product/product-category.md)</li></ul></li><li>**[](../../classes/experienceevent.md)**<ul><li>[](../../field-groups/event/channel-details.md)</li></ul></li><li>**[](../../classes/individual-profile.md)**<ul><li>[](../../field-groups/profile/demographic-details.md)</li><li>[](../../field-groups/profile/personal-contact-details.md)</li><li>[](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Drive new revenue opportunities by using insights gained from cross-channel behavior analysis, identifying patterns of product usage that could lead to new product offers. | <ul><li>**[[!UICONTROL Política]](../../classes/policy.md)**</li><li>**[[!UICONTROL Producto]](../../classes/product.md)**:<ul><li>[](../../field-groups/product/product-category.md)</li></ul></li><li>**[](../../classes/experienceevent.md)**<ul><li>[](../../field-groups/event/card-actions.md)</li><li>[](../../field-groups/event/support-site-search.md)</li><li>[](../../field-groups/event/deposit-details.md)</li><li>[](../../field-groups/event/channel-details.md)</li></ul></li><li>**[](../../classes/individual-profile.md)**<ul><li>[](../../field-groups/profile/demographic-details.md)</li><li>[](../../field-groups/profile/personal-contact-details.md)</li><li>[](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
