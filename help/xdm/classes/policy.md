---
title: Policy Class
description: This document provides an overview of the Policy class in Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---

# 



![](../images/classes/policy.png)

| Propiedad | Data type | Descripción |
| --- | --- | --- |
| `assignedBeneficiary` | [](../data-types/person.md) | Captures the beneficiary (or beneficiaries) assigned to the policy. |
| `benefitAmount` | [[!UICONTROL Moneda]](../data-types/currency.md) | The amount to be paid as per the policy terms. |
| `location` | [](../data-types/postal-address.md) | The location in which the insurance policy is issued. |
| `owner` |  | Captures the policy holder&#39;s profile information. |
| `owner.faxPhone` | [[!UICONTROL Número de teléfono]](../data-types/phone-number.md) | The owner&#39;s fax phone number. |
| `owner.homeAddress` | [](../data-types/postal-address.md) | The owner&#39;s home address. |
| `owner.homePhone` | [[!UICONTROL Número de teléfono]](../data-types/phone-number.md) | The owner&#39;s home phone number. |
| `owner.mobilePhone` | [[!UICONTROL Número de teléfono]](../data-types/phone-number.md) | The owner&#39;s mobile phone number. |
| `owner.personalEmail` | [](../data-types/email-address.md) | The owner&#39;s personal email address. |
| `ID` | [!UICONTROL Cadena] | An identifier for the insurance policy. |
| `_id` | [!UICONTROL Cadena] | A unique, system-generated string identifier for the record. This field is used to track the uniqueness of an individual record, prevent duplication of data, and to look up that record in downstream services.<br><br> However, you can still opt to supply your own unique ID values if you wish. |
| `endDate` |  | The date when the insurance policy coverage ends (or ended). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolean] | Indicates whether the policy has a beneficiary assigned. |
| `name` | [!UICONTROL Cadena] | The name of the insurance policy. |
| `startDate` |  | The date when the insurance policy coverage starts (or started). |
| `type` | [!UICONTROL Cadena] | The type of insurance policy, such as home, automobile, renter, or boat. |

{style=&quot;table-layout:auto&quot;}
