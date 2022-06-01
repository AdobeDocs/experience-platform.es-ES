---
keywords: Experience Platform;inicio;temas populares;Salesforce;salesforce;asignación de campos;asignación de campos;asignación;marketing;B2B;b2b
title: Campos de asignación de Microsoft Dynamics
description: Las tablas siguientes contienen las asignaciones entre los campos de origen de Microsoft Dynamics y sus campos XDM correspondientes.
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: a278f27223c9a5d0b97a0aa6b5d943caf5f6b10e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 7%

---

# [!DNL Microsoft Dynamics] asignaciones de campos

Las tablas siguientes contienen las asignaciones entre [!DNL Microsoft Dynamics] los campos de origen y los campos correspondientes del Modelo de datos de experiencia (XDM).

## Contactos {#contacts}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `birthdate` | `person.birthDate` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `contactid` | `b2b.personKey.sourceID` |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `department` | `extendedWorkDetails.departments` |
| `fullname` | `person.name.fullName` |
| `suffix` | `person.name.suffix` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | Identificador secundario. |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `lastname` | `person.name.lastName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |
| `telephone1` | `workPhone.number` |

{style=&quot;table-layout:auto&quot;}

## Posibles clientes {#leads}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `telephone1` | `workPhone.number` |
| `mobilephone` | `mobilePhone.number` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | Identificador secundario |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `fax` | `faxPhone.number` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `lastname` | `person.name.lastName` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `leadid` | `b2b.personKey.sourceID` |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |

{style=&quot;table-layout:auto&quot;}

## Cuentas {#accounts}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `accountid` | `accountKey.sourceID` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `accountnumber` | `accountNumber` |
| `accountratingcode` | `accountOrganization.rating` |
| `address1_addressid` | `accountPhysicalAddress._id` |
| `address1_city` | `accountPhysicalAddress.city` |
| `address1_country` | `accountPhysicalAddress.country` |
| `address1_county` | `accountPhysicalAddress.region` |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |
| `address1_line1` | `accountPhysicalAddress.street1` |
| `address1_line2` | `accountPhysicalAddress.street2` |
| `address1_line3` | `accountPhysicalAddress.street3` |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |
| `address1_name` | `accountPhysicalAddress.label` |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `accountDescription` |
| `fax` | `accountFax.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `name` | `accountName` |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |
| `revenue` | `accountOrganization.annualRevenue.amount` |
| `sic` | `accountOrganization.SICCode` |
| `telephone1` | `accountPhone.number` |
| `tickersymbol` | `accountOrganization.tickerSymbol` |
| `websiteurl` | `accountOrganization.website` |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |

{style=&quot;table-layout:auto&quot;}

## Oportunidades {#opportunities}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `name` | `opportunityName` |
| `"Dynamics"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |
| `actualclosedate` | `actualCloseDate` |
| `actualvalue` | `opportunityAmount.amount` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |
| `closeprobability` | `probabilityPercentage` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `opportunityDescription` |
| `estimatedclosedate` | `expectedCloseDate` |
| `estimatedvalue` | `expectedRevenue.amount` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `opportunityid` | `opportunityKey.sourceID` |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `salesstage` | `opportunityStage` |
| `stepname` | `nextStep` |

{style=&quot;table-layout:auto&quot;}

## Funciones de contacto de oportunidad {#opportunity-contact-roles}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `connectionid` | `opportunityPersonKey.sourceID` |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `connectionrole1.name` | `personRole` |
| `record1objecttypecode` | *Un grupo de campos personalizados debe definirse como esquema de destino.* Consulte la sección del apéndice para ver los pasos sobre [cómo asignar un campo de origen de tipo lista de selección a un esquema XDM de destino](#picklist-type-fields) para obtener más información. | Para obtener una lista de posibles valores y etiquetas para la variable `record1objecttypecode` campo de origen, consulte [[!DNL Microsoft Dynamics] documento de referencia de la entidad de conexión](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options). |
| `record2objecttypecode` | *Un grupo de campos personalizados debe definirse como esquema de destino.* Consulte la sección del apéndice para ver los pasos sobre [cómo asignar un campo de origen de tipo lista de selección a un esquema XDM de destino](#picklist-type-fields) para obtener más información. | Para obtener una lista de posibles valores y etiquetas para la variable `record2objecttypecode` campo de origen, consulte [[!DNL Microsoft Dynamics] documento de referencia de la entidad de conexión](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options). |

{style=&quot;table-layout:auto&quot;}

## Campañas {#campaigns}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `"Dynamics"` | `campaignKey.sourceType` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | La variable `extSourceSystemAudit.externalKey` es la identidad secundaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `description` | `campaignDescription` |
| `name` | `campaignName` |
| `totalactualcost` | `actualCost.amount` |
| `budgetedcost` | `budgetedCost.amount` |
| `expectedrevenue` | `expectedRevenue.amount` |
| `actualend` | `campaignEndDate` |
| `actualstart` | `campaignStartDate` |
| `expectedresponse` | `expectedResponse` |
| `utcconversiontimezonecode` | `timeZone` |
| `utcconversiontimezonecode` | `timezoneName` |

{style=&quot;table-layout:auto&quot;}

## Lista de marketing {#marketing-list}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `description` | `marketingListDescription` |
| `listname` | `marketingListName` |
| `listid` | `marketingListKey.sourceID` |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## Miembros de la lista de marketing {#marketing-list-members}

| Campo de origen | Campo XDM de Target | Notas |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | Identidad primaria. El valor de `"${CRM_ORG_ID}"` se reemplazará automáticamente. |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## Apéndice

Las secciones siguientes proporcionan información adicional que puede utilizar al configurar asignaciones B2B para sus [!DNL Microsoft] Origen de Dynamics.

### Campos de tipo lista de selección {#picklist-type-fields}

Puede usar [campos calculados](../../../../data-prep/ui/mapping.md#calculated-fields) asignación de un campo de origen de tipo lista de selección [!DNL Microsoft Dynamics] a un campo XDM de destino.

Por ejemplo, la variable `genderCode` El campo incluye dos opciones:

| Valor | Etiqueta |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

Puede utilizar las siguientes opciones para asignar la variable `genderCode` campo de origen a `person.gender` campo de destino:

#### Usar un operador lógico

| Campo de origen | Campo XDM de Target |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

En este escenario, el valor corresponde a la clave, si la clave se encuentra en opciones, o `default`, si `default` está presente y no se encuentra la clave. El valor corresponde a `null` si las opciones son `null` o no hay `default` y la clave no se encuentra.

#### Uso de un campo calculado

| Campo de origen | Campo XDM de Target |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>Una iteración anidada de la operación anterior sería similar a: `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))`.

Para obtener más información, consulte [documento en operadores lógicos en [!DNL Data Prep]](../../../../data-prep/functions.md##logical-operators)
