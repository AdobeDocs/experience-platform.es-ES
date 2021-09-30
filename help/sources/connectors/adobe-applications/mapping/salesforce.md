---
keywords: Experience Platform;inicio;temas populares;Salesforce;salesforce;asignación de campos;asignación de campos;asignación;marketing;B2B;b2b
solution: Experience Platform
title: Campos de asignación de Salesforce
topic-legacy: overview
description: Las tablas siguientes contienen las asignaciones entre los campos de origen de Salesforce y sus correspondientes campos XDM.
source-git-commit: 00207ae10979b48d190cbda63aecf55e0f6d0f9c
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---

# [!DNL Salesforce] asignaciones de campos

Las tablas siguientes contienen las asignaciones entre los campos de origen [!DNL Salesforce] y los campos correspondientes del Modelo de datos de experiencia (XDM).

## Contacto {#contact}

| Campo de origen | Ruta de campo XDM de Target | Notas |
| --- | --- | --- |
| `AccountId` | `b2b.accountID` |
| `AccountId` | `personComponents.sourceAccountID` |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `Birthdate` | `person.birthDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Department` | `extendedWorkDetails.departments` |
| `Email` | `workEmail.address` | Esta es la identidad secundaria. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `Id` | `personID` | Esta es la identidad principal |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `MailingCity` | `workAddress.city` |
| `MailingCountry` | `workAddress.country` |
| `MailingLatitude` | `workAddress._schema.latitude` |
| `MailingLongitude` | `workAddress._schema.longitude` |
| `MailingPostalCode` | `workAddress.postalCode` |
| `MailingState` | `workAddress.state` |
| `MailingStreet` | `workAddress.street1` |
| `MobilePhone` | `mobilePhone.number` |
| `Name` | `person.name.fullName` |
| `OtherCity` | `otherAddress.city` |
| `OtherCountry` | `otherAddress.country` |
| `OtherLatitude` | `otherAddress._schema.latitude` |
| `OtherLongitude` | `otherAddress._schema.longitude` |
| `OtherPhone` | `otherPhone.number` |
| `OtherPostalCode` | `otherAddress.postalCode` |
| `OtherState` | `otherAddress.state` |
| `OtherStreet` | `otherAddress.street1` |
| `Phone` | `workPhone.number` |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |
| `Salutation` | `person.name.courtesyTitle` |
| `Title` | `extendedWorkDetails.jobTitle` |

{style=&quot;table-layout:auto&quot;}

## Posible cliente {#lead}

| Campo de origen | Ruta de campo XDM de Target | Notas |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedContactId` | `b2b.convertedContactID` |
| `ConvertedContactId` | `personComponents.sourceConvertedContactID` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | Esta es la identidad secundaria |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `Id` | `personID` | Esta es la identidad principal |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `Latitude` | `workAddress._schema.latitude` |
| `Longitude` | `workAddress._schema.longitude` |
| `MiddleName` | `person.name.middleName` |
| `Name` | `person.name.fullName` |
| `PostalCode` | `workAddress.postalCode` |
| `Salutation` | `person.name.courtesyTitle` |
| `State` | `workAddress.state` |
| `Status` | `b2b.personStatus` |
| `Status` | `personComponents.personStatus` |
| `Street` | `workAddress.street1` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `Suffix` | `person.name.suffix` |

{style=&quot;table-layout:auto&quot;}

## Cuenta {#account}

| Campo de origen | Ruta de campo XDM de Target | Notas |
| --- | --- | --- |
| `AccountNumber` | `accountNumber` |
| `AccountSource` | `accountSourceType` |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |
| `BillingCity` | Dirección | `accountBillingAddress.city` |
| `BillingCountry` | `accountBillingAddress.country` |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |
| `BillingState` | `accountBillingAddress.state` |
| `BillingStreet` | `accountBillingAddress.street1` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `accountDescription` |
| `DunsNumber` | `accountOrganization.DUNSNumber` | característica data.com |
| `Fax` | `accountFax.number` |
| `Id` | `accountID` | Esta es la identidad principal |
| `Industry` | `accountOrganization.industry` |
| `Jigsaw` | `accountOrganization.jigsaw` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `NaicsCode` | `accountOrganization.NAICSCode` | característica data.com |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | característica data.com |
| `Name` | `accountName` |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `Ownership` | `accountOwnership` |
| `ParentId` | `accountParentID` |
| `Phone` | `accountPhone.number` |
| `Rating` | `accountOrganization.rating` |
| `ShippingCity` | `accountShippingAddress.city` |
| `ShippingCountry` | `accountShippingAddress.country` |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |
| `ShippingState` | `accountShippingAddress.state` |
| `ShippingStreet` | `accountShippingAddress.street1` |
| `Sic` | `accountOrganization.SICCode` |
| `SicDesc` | `accountOrganization.SICDescription` |
| `Site` | `accountSite` |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |
| `Tradestyle` | `accountTradeStyle` | característica data.com |
| `Type` | `accountType` |

{style=&quot;table-layout:auto&quot;}

## Oportunidad {#opportunity}

| Campo de origen | Ruta de campo XDM de Target | Notas |
| --- | --- | --- |
| `AccountId` | `accountID` | Relación |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignID` |
| `CloseDate` | `actualCloseDate` / `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityID` | Esta es la identidad principal |
| `IsClosed` | `isClosed` |
| `IsWon` | `isWon` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `leadSource` |
| `Name` | `opportunityName` |
| `NextStep` | `nextStep` |
| `Probability` | `probabilityPercentage` |
| `StageName` | `opportunityStage` |
| `TotalOpportunityQuantity` | `opportunityQuantity` |
| `Type` | `opportunityType` |

{style=&quot;table-layout:auto&quot;}

## Función de contacto de oportunidad {#opportunity-contact-role}

| Campo de origen | Ruta de campo XDM de Target | Notas |
| --- | --- | --- |
| `ContactId` | `personID` | Relación |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Id` | `opportunityPersonID` | Esta es la identidad principal |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `OpportunityId` | `opportunityID` | Relación |
| `Role` | `personRole` |

{style=&quot;table-layout:auto&quot;}

## Campaign {#campaign}

| Campo de origen | Ruta de campo XDM de Target | Notas |
| --- | --- | --- |
| `Id` | `xdm: campaignID` | Esta es la identidad principal |
| `Name` | `xdm: campaignName` |
| `ParentId` | `xdm: parentCampaignID` |
| `Type` | `xdm: campaignType` |
| `Status` | `xdm: campaignStatus` |
| `StartDate` | `xdm: campaignStartDate` |
| `EndDate` | `xdm: campaignEndDate` |
| `ExpectedRevenue` | `xdm: expectedRevenue.amount` |
| `BudgetedCost` | `xdm: budgetedCost.amount` |
| `ActualCost` | `xdm: actualCost.amount` |
| `ExpectedResponse` | `xdm: expectedResponse` |
| `IsActive` | `xdm: isActive` |
| `Description` | `xdm: campaignDescription` |
| `CreatedDate` | `xdm: extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `xdm: extSourceSystemAudit.lastUpdatedDate` |
| `LastActivityDate` | `xdm: extSourceSystemAudit.lastActivityDate` |
| `LastViewedDate` | `xdm: extSourceSystemAudit.lastViewedDate` |
| `LastReferencedDate` | `xdm: extSourceSystemAudit.lastReferencedDate` |

## Miembro de la campaña {#campaign-member}

| Campo de origen | Ruta de campo XDM de Target | Notas |
| --- | --- | --- |
| `Id` | `campaignMemberID` | Esta es la identidad principal |
| `CampaignId` | `campaignID` | Relación |
| `LeadOrContactId` | `personID` | Relación |
| `Status` | `memberStatus` |
| `HasResponded` | `hasResponded` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `FirstRespondedDate` | `firstRespondedDate` |

## Pasos siguientes

Al leer este documento, ha adquirido información sobre la relación de asignación entre los [!DNL Salesforce] campos de origen y sus correspondientes campos XDM. Consulte el tutorial sobre la [creación de una [!DNL Salesforce] conexión de origen](../../../tutorials/ui/create/crm/salesforce.md) para iniciar el flujo de datos [!DNL Salesforce].
