---
keywords: Experience Platform;inicio;temas populares;Marketo Engage;marketo engage;Marketo;asignación
solution: Experience Platform
title: Asignación de campos para Marketo Engage Source
description: Las siguientes tablas contienen las asignaciones entre los campos de los conjuntos de datos de Marketo y sus campos XDM correspondientes.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 2%

---

# [!DNL Marketo Engage] asignaciones de campo {#marketo-engage-field-mappings}

Las tablas siguientes contienen las asignaciones entre los campos de los nueve conjuntos de datos [!DNL Marketo] y sus campos correspondientes del Modelo de datos de experiencia (XDM).

>[!TIP]
>
>Todos los conjuntos de datos de [!DNL Marketo] excepto `Activities` ahora admiten `isDeleted`. Los flujos de datos existentes incluirán automáticamente `isDeleted`, pero solamente ingerirán el indicador para los datos recién ingeridos. Si desea aplicar el indicador a todos los datos históricos, debe detener los flujos de datos existentes y volver a crearlos con la nueva asignación. Tenga en cuenta que si elimina `isDeleted`, ya no tendrá acceso a la funcionalidad. Es fundamental que la asignación se mantenga después de rellenarse automáticamente.

## Actividades {#activities}

El origen [!DNL Marketo] ahora admite actividades estándar adicionales. Para usar actividades estándar, debe actualizar el esquema con la [utilidad de generación automática de esquemas](../marketo/marketo-namespaces.md), porque si crea un nuevo flujo de datos de `activities` sin actualizar el esquema, las plantillas de asignación fallarán, ya que los nuevos campos de destino no estarán presentes en el esquema. Si decide no actualizar el esquema, aún puede crear un nuevo flujo de datos y descartar cualquier error. Sin embargo, los campos nuevos o actualizados no se incorporarán en Experience Platform.

Lea la documentación sobre [clase de evento de experiencia XDM](../../../../xdm/classes/experienceevent.md) para obtener más información sobre la clase XDM y los grupos de campos XDM.

>[!NOTE]
>
>El campo de origen `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` es un campo calculado que debe agregarse usando la opción **[!UICONTROL Agregar campo calculado]** en la interfaz de usuario de Experience Platform. Lea el tutorial sobre [agregar campos calculados](../../../../data-prep/ui/mapping.md#calculated-fields) para obtener más información.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `"Marketo"` | `personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `personID` | `personKey.sourceID` |
| `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `eventType` | `eventType` |
| `producedBy` | `producedBy` |
| `timestamp` | `timestamp` |
| `web.webPageDetails.URL` | `web.webPageDetails.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |
| `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |
| `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |
| `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |
| `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |
| `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |
| `iif(${leadOperation\\.callWebhook\\.webhookKey\\.sourceID} != null && ${leadOperation\\.callWebhook\\.webhookKey\\.sourceID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookKey\\.sourceID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookKey\\.sourceInstanceID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `leadOperation.callWebhook.webhookKey` |
| `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |
| `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |
| `iif(${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceInstanceID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `leadOperation.changeCampaignCadence.campaignKey` |
| `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |
| `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |
| `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |
| `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |
| `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |
| `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |
| `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |
| `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |
| `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |
| `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |
| `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |
| `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |
| `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |
| `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |
| `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |
| `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |
| `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |
| `iif(${leadOperation\.mergeLeads\.sourceIDs} != null && ${leadOperation\.mergeLeads\.sourceIDs} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.mergeLeads\.sourceIDs}, "sourceKey", concat(${leadOperation\.mergeLeads\.sourceIDs},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.mergeLeads.sourceKeys` |
| `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |
| `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |
| `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |
| `iif(${directMarketing\\.emailSent\\.mailingID} != null && ${directMarketing\\.emailSent\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.emailSent\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.emailSent\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `directMarketing.emailSent.mailingKey` |
| `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |
| `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |
| `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |
| `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` | Este es un campo calculado. |

{style="table-layout:auto"}

## Programas {#programs}

Lea la [descripción general de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) para obtener más información sobre la clase XDM. Para obtener más información sobre los grupos de campos XDM, lea la guía [Grupo de campos de esquema de detalles de Campaign empresarial](../../../../xdm/field-groups/b2b-campaign/details.md).

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `id` | `campaignKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` es la identidad secundaria. Los valores de `{CRM_ORG_ID}` y `{CRM_TYPE}` se reemplazarán automáticamente. |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |
| `integrationPartner` | `integrationPartnerName` |
| `webinarSessionName` | `webinarSessionName` |
| `webinarSessionDescription` | `webinarSessionDescription` |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Pertenencia a programas {#program-memberships}

Lea la [descripción general de los miembros de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) para obtener más información sobre la clase XDM. Para obtener más información sobre los grupos de campos XDM, lea la guía del campo de esquema [Detalles de miembro de XDM Business Campaign](../../../../xdm/field-groups/b2b-campaign-members/details.md).

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `id` | `campaignMemberKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Relación |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relación |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` es la identidad secundaria. Los valores de `{CRM_ORG_ID}` y `{CRM_TYPE}` se reemplazarán automáticamente. |
| `sfdc.lastStatus` | `lastStatus` |
| `sfdc.hasResponded` | `hasResponded` |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Compañías {#companies}

Lea la [descripción general de la cuenta empresarial de XDM](../../../../xdm/classes/b2b/business-account.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| <ul><li>`iif(mktoCdpExternalId != null && mktoCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpExternalId, "sourceKey", concat(mktoCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(msftCdpExternalId != null && msftCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", msftCdpExternalId, "sourceKey", concat(msftCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` es la identidad secundaria. Los valores de `{CRM_ORG_ID}` y `{CRM_TYPE}` se reemplazarán automáticamente. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Listas estáticas {#static-lists}

Lea la [descripción general de la lista de marketing empresarial de XDM](../../../../xdm/classes/b2b/business-marketing-list.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | `"${MUNCHKIN_ID}"` se reemplazará como parte de la API de Explorar. |
| `id` | `marketingListKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Pertenencia a lista estática {#static-list-memberships}

Lea la [descripción general de los miembros de la lista de marketing empresarial de XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | Relación |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relación |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Cuentas con nombre {#named-accounts}

>[!IMPORTANT]
>
>El conjunto de datos de cuentas con nombre solo es necesario con la función de marketing basado en cuentas (ABM) de Marketo. Si no utiliza ABM, no es necesario configurar asignaciones para cuentas con nombre.

Lea la [descripción general de la cuenta empresarial de XDM](../../../../xdm/classes/b2b/business-account.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `iif(externalSourceId != null && externalSourceId != "", to_object("sourceType", externalSourceType, "sourceInstanceID", externalSourceInstanceId, "sourceID", externalSourceId, "sourceKey", externalSourceKey), iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null))` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` es la identidad secundaria. Los valores de `{CRM_ORG_ID}` y `{CRM_TYPE}` se reemplazarán automáticamente. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `sourceType` | `accountSourceType` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Oportunidades {#opportunities}

Lea la [descripción general de la oportunidad empresarial de XDM](../../../../xdm/classes/b2b/business-opportunity.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `id` | `opportunityKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | Identidad secundaria. Los valores de `{CRM_ORG_ID}` y `{CRM_TYPE}` se reemplazarán automáticamente. |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Relación |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Este conjunto de datos de origen solo está disponible para usuarios con la integración [!DNL Salesforce]. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Funciones de contacto de oportunidad {#opportunity-contact-roles}

Lea la [descripción general de la relación personal de la oportunidad empresarial de XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityPersonKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `id` | `opportunityPersonKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará como parte de la API Explorar. |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` es la identidad secundaria. Los valores de `{CRM_ORG_ID}` y `{CRM_TYPE}` se reemplazarán automáticamente. |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | Relación |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relación |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Personas {#persons}

Lea la [descripción general del perfil individual de XDM](../../../../xdm/classes/individual-profile.md) para obtener más información sobre la clase XDM. Para obtener más información sobre los grupos de campos XDM, lea la guía [Grupo de campos de esquema de detalles de persona de negocios de XDM](../../../../xdm/field-groups/profile/business-person-details.md) y la guía [Grupo de campos de campos de componentes de persona de negocios de XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `b2b.personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `id` | `b2b.personKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | Identidad principal. El valor de `"${MUNCHKIN_ID}"` se reemplazará automáticamente. |
| `iif(unsubscribed == 'true', 'n', 'y' ))` | `consents.marketing.email.val` | Si la cancelación de la suscripción es `true` (por ejemplo, value = `1`), establezca `consents.marketing.email.val` como (`n`). Si la cancelación de la suscripción es `false` (por ejemplo, value = `0`), establezca `consents.marketing.email.val` como `null`. |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` es la identidad secundaria. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `b2b.companyName` |
| `website` | `b2b.companyWebsite` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `personComponents.sourceExternalKey` |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |
| `marketoIsDeleted` | `isDeleted` |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", mktoCdpCnvContactPersonId, \"sourceKey\", concat(mktoCdpCnvContactPersonId,\"@${MUNCHKIN_ID}.Marketo\")), null)` | `b2b.convertedContactKey` | Este es un campo calculado. |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", mktoCdpCnvContactPersonId, \"sourceKey\", concat(mktoCdpCnvContactPersonId,\"@${MUNCHKIN_ID}.Marketo\")), null)` | `personComponents.sourceConvertedContactKey` | Este es un campo calculado. |

{style="table-layout:auto"}

## Pasos siguientes

Al leer este documento, ha obtenido insight en la relación de asignación entre sus [!DNL Marketo] conjuntos de datos y sus campos XDM correspondientes. Vea el tutorial sobre [creación de una [!DNL Marketo] conexión de origen](../../../tutorials/ui/create/adobe-applications/marketo.md) para completar su flujo de datos de [!DNL Marketo].
