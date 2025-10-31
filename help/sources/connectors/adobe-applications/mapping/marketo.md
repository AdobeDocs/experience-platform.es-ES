---
keywords: Experience Platform;inicio;temas populares;Marketo Engage;marketo engage;Marketo;asignación
solution: Experience Platform
title: Asignación de campos para Marketo Engage Source
description: Las siguientes tablas contienen las asignaciones entre los campos de los conjuntos de datos de Marketo y sus campos XDM correspondientes.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 5%

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
>El campo de origen `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` es un campo calculado que debe agregarse usando la opción **[!UICONTROL Add calculated field]** en la interfaz de usuario de Experience Platform. Lea el tutorial sobre [agregar campos calculados](../../../../data-prep/ui/mapping.md#calculated-fields) para obtener más información.

| Campo de origen de Marketo | ID de tipo de actividad | Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------------- | ---------------- | -------------- | ---------------- | ----- |
| `_id` |  | `_id` | `_id` |  |
|  |  | `"Marketo"` | `personKey.sourceType` |  |
|  |  | `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `leadId` |  | `personID` | `personKey.sourceID` |  |
|  |  | `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `activityTypeId` |  | `eventType` | `eventType` |  |
| <ul><li>Si <code>activityTypeId</code> es 1, 2, 3, 9, 10 u 11 → marca <code>productionBy</code> como <strong>self</strong>.</li><li>Si <code>activityTypeId</code> es la marca de → <code>producida por} 6, 7, 8, 12, 21, 22, 24, 25, 27, 32, 34, 35, 36, 46, 101, 104, 110, 113, 114 o 115</code> como <strong>sistema</strong>.</li><li>Para todos los demás valores → marca <code>productionBy</code> como <strong>self</strong>.</li></ul> |  | `producedBy` | `producedBy` |  |
| `activityDate` |  | `timestamp` | `timestamp` |  |
| `attributes.Webpage URL` |  | `web.webPageDetails.URL` | `web.webPageDetails.URL` |  |
| `attributes.User Agent` |  | `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |  |
| `attributes.Client IP Address` |  | `environment.ipV4` | `environment.ipV4` |  |
| `attributes.Search Query` |  | `search.keywords` | `search.keywords` |  |
| `attributes.Search Engine` |  | `search.searchEngine` | `search.searchEngine` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.name` | `web.webPageDetails.name` |  |
| `attributes.Personalized URL` | 1 | `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |  |
| `attributes.Query Parameters` | 1 | `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |  |
| `attributes.Referrer URL` |  | `web.webReferrer.URL` | `web.webReferrer.URL` |  |
| `primaryAttributeValueId when activityTypeId in (24, 25)` | 24, 25 | `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |  |
| `attributes.Is Primary` | 34,35,36 | `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |  |
| primaryAttributeValueId cuando activityTypeId en (34, 35, 36) | 34, 35, 36 | `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |  |
| `attributes.Role` | 34, 35, 36 | `opportunityEvent.role` | `opportunityEvent.role` |  |
| `attributes.Created Date` |  | `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |  |
| `attributes.Form Name` |  | `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |  |
| `attributes.Lead Source` |  | `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |  |
| `attributes.List Name` |  | `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |  |
| `attributes.SFDC Type` |  | `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |  |
| `attributes.Source Type` |  | `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |  |
| primaryAttributeValue cuando activityTypeId = 21 | 21 | `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |  |
| `attributes.Converted Status` | 21 | `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |  |
| `attributes.Send Notification Email` | 21 | `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |  |
| primaryAttributeValueId cuando activityTypeId en (7, 8, 9, 10, 11, 27) | 7, 8, 9, 10, 11, 27 | `iif(${directMarketing\\.mailingID} != null && ${directMarketing\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `directMarketing.mailingKey` |  |
| primaryAttributeValueId cuando activityTypeId en (7, 8, 9, 10, 11, 27) | 7, 8, 9, 10, 11, 27 | `directMarketing.mailingName` | `directMarketing.mailingName` |  |
|  |  | `directMarketing.testVariantName` | `directMarketing.testVariantName` |  |
| `attributes.Test Variant` |  | `directMarketing.testVariantID` | `directMarketing.testVariantID` |  |
| `attributes.Subcategory` <ul><li><strong>activityTypeId = 8</strong><ul><li>1099 → MENSAJE BLOQUEADO</li><li>1003 → SPAM BLOQUEADO EN SOURCE</li><li>1004 → SPAM BLOQUEADO EN EL MENSAJE</li><li>2003 → DIRECCIÓN DE CORREO ELECTRÓNICO NO VÁLIDA</li><li>ERROR DE DIRECCIÓN DE CORREO ELECTRÓNICO → 2001</li><li> `&rarr;` RAZÓN DESCONOCIDA DE LA DEVOLUCIÓN</li></ul></li><li><strong>activityTypeId = 27</strong><ul><li>3999 → MENSAJE NO ACEPTADO</li><li>3001 → BUZÓN LLENO</li><li>TIEMPO DE ESPERA DE → 3004</li><li>ERROR DE DNS DE → 4003</li><li>4002 MENSAJE DE → DEMASIADO GRANDE</li><li>4006 → INFRACCIÓN DE DIRECTIVA</li><li>4999 → FALLO TRANSITORIO</li><li>9999 → RESPUESTA INCORRECTA RECIBIDA</li><li> → RAZÓN DESCONOCIDA DE LA DEVOLUCIÓN SUAVE</li></ul></li></ul> | 8, 27 | `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |  |
| `attributes.Details` |  | `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |  |
| `attributes.Email` |  | `directMarketing.email` | `directMarketing.email` |  |
| `attributes.Is Mobile Device` |  | `device.isMobileDevice` | `device.isMobileDevice` |  |
| `attributes.device` |  | `device.model` | `device.model` |  |
| `attributes.Platform` |  | `environment.operatingSystem` | `environment.operatingSystem` |  |
| `attributes.Link` |  | `directMarketing.linkURL` | `directMarketing.linkURL` |  |
| primaryAttributeValueId cuando activityTypeId = 3 atributos más.ID de vínculo | 3 | `iif(${web\\.webInteraction\\.linkID} != null && ${web\\.webInteraction\\.linkID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.webInteraction\\.linkID}, \"sourceKey\", concat(${web\\.webInteraction\\.linkID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.webInteraction.webInteractionKey` |  |
| primaryAttributeValueId cuando activityTypeId = 2 atributos más.ID de formulario web | 2 | `iif(${web\\.fillOutForm\\.webFormID} != null && ${web\\.fillOutForm\\.webFormID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.fillOutForm\\.webFormID}, \"sourceKey\", concat(${web\\.fillOutForm\\.webFormID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.fillOutForm.webFormKey` |  |
| primaryAttributeValueId cuando activityTypeId = 2 else null | 2 | `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |  |
| primaryAttributeValueId cuando activityTypeId = 3 atributos más.Link | 3 | `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |  |
| `attributes.Change Value` | 22 | `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |  |
| `attributes.New Value` | 22 | `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |  |
| `attributes.Old Value` | 22 | `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |  |
| `attributes.Priority` | 22 | `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |  |
| `attributes.Reason` | 22 | `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |  |
| `attributes.Relative Score` | 22 | `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |  |
| `attributes.Relative Urgency` | 22 | `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |  |
| primaryAttributeValueId cuando activityTypeId = 22 | 22 | `iif(${leadOperation\.changeScore\.scoreAttributeID} != null && ${leadOperation\.changeScore\.scoreAttributeID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeScore\.scoreAttributeID}, "sourceKey", concat(${leadOperation\.changeScore\.scoreAttributeID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeScore.scoreAttributeKey` |  |
| primaryAttributeValueId cuando activityTypeId = 22 | 22 | `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |  |
| `attributes.Urgency` | 22 | `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |  |
| `attributes.Data Value Changes` |  | `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |  |
| primaryAttributeValueId cuando activityTypeId = 104 | 104 | `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |  |
| `attributes.Acquired By` | 104 | `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |  |
| `attributes.Success` | 104 | `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |  |
| `attributes.New Status ID` | 104 | `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |  |
| `attributes.New Status` | 104 | `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |  |
| `attributes.Old Status ID` | 104 | `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |  |
| `attributes.Old Status` | 104 | `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |  |
| `attributes.Reason` | 104 | `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |  |
| `attributes.Date` | 46 | `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |  |
| `attributes.Description` | 46 | `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |  |
| `attributes.Source` | 46 | `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |  |
| primaryAttributeValue cuando activityTypeId = 46 | 46 | `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |  |
| primaryAttributeValueId cuando activityTypeId = 110 | 110 | `iif(${leadOperation\\.callWebhook\\.webhookID} != null && ${leadOperation\\.callWebhook\\.webhookID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.callWebhook.webhookKey` |  |
| primaryAttributeValueId cuando activityTypeId = 110 | 110 | `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |  |
| `attributes.Error Type` | 110 | `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |  |
| primaryAttributeValueId cuando activityTypeId = 115 | 115 | `iif(${leadOperation\\.changeCampaignCadence\\.campaignID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeCampaignCadence.campaignKey` |  |
| `attributes.New Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |  |
| `attributes.Previous Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |  |
| primaryAttributeValueId cuando activityTypeId = 114 | 113 | `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |  |
| `attributes.Track ID` | 113 | `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |  |
| `attributes.Stream Name` | 113 | `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |  |
| primaryAttributeValueId cuando activityTypeId = 115 | 115 | `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |  |
| `attributes.New Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |  |
| `attributes.New Track Name` | 115 | `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |  |
| `attributes.Previous Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |  |
| `attributes.Previous Stream Name` | 115 | `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |  |
| primaryAttributeValueId cuando activityTypeId = 101 | 101 | `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |  |
| primaryAttributeValueId cuando activityTypeId = 101 | 101 | `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |  |
| `attributes.New Stage ID` | 101 | `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |  |
| `attributes.New Stage` | 101 | `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |  |
| `attributes.Old Stage ID` | 101 | `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |  |
| `attributes.Old Stage` | 101 | `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |  |
| `attributes.Reason` | 101 | `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |  |
| `attributes.Merge IDs` cuando activityTypeId = 32 | 32 | `json_to_object(${leadOperation\.mergeLeads\.mergeIDs})` | `leadOperation.mergeLeads.sourceKeys` |  |
| `attributes.Master Updated` | 32 | `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |  |
| `attributes.Merged in Sales` | 32 | `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |  |
| `attributes.Merge Source` | 32 | `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |  |
| primaryAttributeValueId cuando activityTypeId = 6 | 6 | `iif(${directMarketing\.emailSent\.mailingID} != null && ${directMarketing\.emailSent\.mailingID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${directMarketing\.emailSent\.mailingID}, "sourceKey", concat(${directMarketing\.emailSent\.mailingID},"@${MUNCHKIN_ID}.Marketo")), null)` | `directMarketing.emailSent.mailingKey` |  |
| primaryAttributeValueId cuando activityTypeId = 6 | 6 | `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |  |
| `attributes.Test Variant` | 6 | `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |  |
| Nota: derivado del valor de los activos secundarios |  | `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |  |
| `attributes.Campaign Run ID` | 6 | `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |  |
|  |  | `directMarketing.automationRunID` | `directMarketing.automationRunID` |  |

{style="table-layout:auto"}

## Programas {#programs}

Lea la [descripción general de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) para obtener más información sobre la clase XDM. Para obtener más información sobre los grupos de campos XDM, lea la guía [Grupo de campos de esquema de detalles de Campaign empresarial](../../../../xdm/field-groups/b2b-campaign/details.md).

>[!NOTE]
>
>Para los tipos de etiquetas personalizados, vaya a esquemas y cree nuevos grupos de campos. A continuación, añada todos los nombres de campo adicionales necesarios para asignar los campos de origen con campos XDM de destino.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `"Marketo"` | `campaignKey.sourceType` |  |
| `channel` | `channelName` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `cost` | `actualCost.amount` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `description` | `campaignDescription` |  |
| `endDate` | `campaignEndDate` |  |
| `id` | `campaignKey.sourceID` |  |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |  |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` es una identidad secundaria. CRM_TYPE y CRM_ORG_ID se reemplazarán como parte de la API de exploración |
| `integrationPartner` | `integrationPartnerName` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `name` | `campaignName` |  |
| `startDate` | `campaignStartDate` |  |
| `status` | `campaignStatus` |  |
| `type` | `campaignType` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |  |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |  |
| `webinarSessionDescription` | `webinarSessionDescription` |  |
| `webinarSessionName` | `webinarSessionName` |  |

{style="table-layout:auto"}

## Pertenencia a programas {#program-memberships}

Lea la [descripción general de los miembros de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) para obtener más información sobre la clase XDM. Para obtener más información sobre los grupos de campos XDM, lea la guía del campo de esquema [Detalles de miembro de XDM Business Campaign](../../../../xdm/field-groups/b2b-campaign-members/details.md).

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | --------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `id` | `campaignMemberKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Relación |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relación |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |  |
| `reachedSuccess` | `hasReachedSuccess` |  |
| `isExhausted` | `isExhausted` |  |
| `statusName` | `memberStatus` |  |
| `statusReason` | `memberStatusReason` |  |
| `membershipDate` | `membershipDate` |  |
| `nurtureCadence` | `nurtureCadence` |  |
| `trackName` | `nurtureTrackName` |  |
| `webinarUrl` | `webinarConfirmationUrl` |  |
| `registrationCode` | `webinarRegistrationID` |  |
| `reachedSuccessDate` | `reachedSuccessDate` |  |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` es una identidad secundaria. CRM_TYPE y CRM_ORG_ID se reemplazarán como parte de la API de exploración |
| `sfdc.lastStatus` | `lastStatus` |  |
| `sfdc.hasResponded` | `hasResponded` |  |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Compañías {#companies}

Lea la [descripción general de la cuenta empresarial de XDM](../../../../xdm/classes/b2b/business-account.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` | |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` | |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| <ul><li><code>iif(mktoCdpExternalId != null &amp;&amp; mktoCdpExternalId != &quot;&quot;, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, mktoCdpExternalId, &quot;sourceKey&quot;, concat(mktoCdpExternalId,&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(msftCdpExternalId != null &amp;&amp; msftCdpExternalId != &quot;&quot;, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, msftCdpExternalId, &quot;sourceKey&quot;, concat(msftCdpExternalId,&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` es una identidad secundaria. CRM_ORG_ID y CRM_TYPE se reemplazarán como parte de la API de exploración |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |
| `billingCity` | `accountBillingAddress.city` | |
| `billingCountry` | `accountBillingAddress.country` | |
| `billingPostalCode` | `accountBillingAddress.postalCode` | |
| `billingState` | `accountBillingAddress.state` | |
| `billingStreet` | `accountBillingAddress.street1` | |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` | |
| `sicCode` | `accountOrganization.SICCode` | |
| `industry` | `accountOrganization.industry` | |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` | |
| `website` | `accountOrganization.website` | |
| `mainPhone` | `accountPhone.number` | |
| `company` | `accountName` | |
| `companyNotes` | `accountDescription` | |
| `site` | `accountSite` | |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` | |
| `marketoIsDeleted` | `isDeleted` | |

{style="table-layout:auto"}

## Listas estáticas {#static-lists}

Lea la [descripción general de la lista de marketing empresarial de XDM](../../../../xdm/classes/b2b/business-marketing-list.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `id` | `marketingListKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `name` | `marketingListName` |  |
| `description` | `marketingListDescription` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Pertenencia a lista estática {#static-list-memberships}

Lea la [descripción general de los miembros de la lista de marketing empresarial de XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |  |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | Relación |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relación |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Cuentas con nombre {#named-accounts}

>[!IMPORTANT]
>
>El conjunto de datos de cuentas con nombre solo es necesario con la función de marketing basado en cuentas (ABM) de Marketo. Si no utiliza ABM, no es necesario configurar asignaciones para cuentas con nombre.

Lea la [descripción general de la cuenta empresarial de XDM](../../../../xdm/classes/b2b/business-account.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | --------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |  |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` es una identidad secundaria. CRM_TYPE y CRM_ORG_ID se reemplazarán como parte de la API de exploración |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `city` | `accountBillingAddress.city` |  |
| `country` | `accountBillingAddress.country` |  |
| `state` | `accountBillingAddress.state` |  |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `sicCode` | `accountOrganization.SICCode` |  |
| `industry` | `accountOrganization.industry` |  |
| `logoUrl` | `accountOrganization.logoUrl` |  |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `name` | `accountName` |  |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |  |
| `sourceType` | `accountSourceType` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Oportunidades {#opportunities}

Lea la [descripción general de la oportunidad empresarial de XDM](../../../../xdm/classes/b2b/business-opportunity.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | --------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `id` | `opportunityKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` es una identidad secundaria. CRM_TYPE y CRM_ORG_ID se reemplazarán como parte de la API de exploración |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Relación |
| `description` | `opportunityDescription` |  |
| `name` | `opportunityName` |  |
| `stage` | `opportunityStage` |  |
| `type` | `opportunityType` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `expectedRevenue` | `expectedRevenue.amount` |  |
| `amount` | `opportunityAmount.amount` |  |
| `closeDate` | `expectedCloseDate` |  |
| `fiscalQuarter` | `fiscalQuarter` |  |
| `fiscalYear` | `fiscalYear` |  |
| `forecastCategory` | `forecastCategory` |  |
| `forecastCategoryName` | `forecastCategoryName` |  |
| `isClosed` | `isClosed` |  |
| `isWon` | `isWon` |  |
| `quantity` | `opportunityQuantity` |  |
| `probability` | `probabilityPercentage` |  |
| `iif(mktoCdpSourceCampaignId != null && mktoCdpSourceCampaignId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpSourceCampaignId, "sourceKey", concat(mktoCdpSourceCampaignId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Solo para clientes con integración de Salesforce |
| `lastActivityDate` | `lastActivityDate` |  |
| `leadSource` | `leadSource` |  |
| `nextStep` | `nextStep` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Funciones de contacto de oportunidad {#opportunity-contact-roles}

Lea la [descripción general de la relación personal de la oportunidad empresarial de XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) para obtener más información sobre la clase XDM.

| Conjunto de datos Source | Campo de destino XDM | Notas |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `"Marketo"` | `opportunityPersonKey.sourceType` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `id` | `opportunityPersonKey.sourceID` |  |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relación |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | Relación |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` es una identidad secundaria. CRM_TYPE y CRM_ORG_ID se reemplazarán como parte de la API de exploración |
| `isPrimary` | `isPrimary` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `role` | `personRole` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |

{style="table-layout:auto"}

## Personas {#persons}

Lea la [descripción general del perfil individual de XDM](../../../../xdm/classes/individual-profile.md) para obtener más información sobre la clase XDM. Para obtener más información sobre los grupos de campos XDM, lea la guía [Grupo de campos de esquema de detalles de persona de negocios de XDM](../../../../xdm/field-groups/profile/business-person-details.md) y la guía [Grupo de campos de campos de componentes de persona de negocios de XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Campo de origen | Campo XDM de destino | Notas |
|---|---|---|
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `"Marketo"` | `b2b.personKey.sourceType` | |
| `address` | `workAddress.street1` | |
| `city` | `workAddress.city` | |
| `company` | `organizations` | |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | Identidad principal. MUNCHKIN_ID se reemplazará como parte de la API de exploración |
| `country` | `workAddress.country` | |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `dateOfBirth` | `person.birthDate` | |
| `email` | `personComponents.workEmail.address` | |
| `email` | `workEmail.address` | |
| `fax` | `faxPhone.number` | |
| `firstName` | `person.name.firstName` | |
| `id` | `b2b.personKey.sourceID` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` | |
| <ul><li><code>iif(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId, null), &quot;sourceKey&quot;, concat(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId, null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(decode(msftType, &quot;Contacto&quot;, msftContactId, &quot;Posible cliente&quot;, msftLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null), &quot;sourceKey&quot;, concat(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `personComponents.sourceExternalKey` | |
| <ul><li><code>iif(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId, null), &quot;sourceKey&quot;, concat(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId, null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(decode(msftType, &quot;Contacto&quot;, msftContactId, &quot;Posible cliente&quot;, msftLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null), &quot;sourceKey&quot;, concat(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` es una identidad secundaria |
| `iif(ecids != null, to_object('ECID',arrays_to_objects('id',explode(ecids))), null)` | `identityMap` | Este es un campo calculado |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` | |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.convertedContactKey` | Este es un campo calculado |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceConvertedContactKey` | Este es un campo calculado |
| `iif(unsubscribed == 'true', 'n', 'y' )` | `consents.marketing.email.val` | Si la cancelación de la suscripción es verdadera (es decir, valor = 1), establezca conents.marketing.email.val como &quot;n&quot;. Si la cancelación de la suscripción es falsa (es decir, el valor = 0), establezca conents.marketing.email.val como nulo |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` | |
| `lastName` | `person.name.lastName` | |
| `leadPartitionId` | `b2b.personGroupID` | |
| `leadPartitionId` | `personComponents.personGroupID` | |
| `leadScore` | `b2b.personScore` | |
| `leadScore` | `personComponents.personScore` | |
| `leadSource` | `b2b.personSource` | |
| `leadSource` | `personComponents.personSource` | |
| `leadStatus` | `b2b.personStatus` | |
| `leadStatus` | `personComponents.personStatus` | |
| `marketingSuspended` | `b2b.isMarketingSuspended` | |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` | |
| `marketoIsDeleted` | `isDeleted` | |
| `middleName` | `person.name.middleName` | |
| `mktoCdpConvertedDate` | `b2b.convertedDate` | |
| `mktoCdpIsConverted` | `b2b.isConverted` | |
| `mobilePhone` | `mobilePhone.number` | |
| `personType` | `b2b.personType` | |
| `personType` | `personComponents.personType` | |
| `phone` | `workPhone.number` | |
| `postalCode` | `workAddress.postalCode` | |
| `salutation` | `person.name.courtesyTitle` | |
| `state` | `workAddress.state` | |
| `title` | `extendedWorkDetails.jobTitle` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |

{style="table-layout:auto"}

## Próximos pasos

Al leer este documento, ha obtenido insight en la relación de asignación entre sus [!DNL Marketo] conjuntos de datos y sus campos XDM correspondientes. Vea el tutorial sobre [creación de una [!DNL Marketo] conexión de origen](../../../tutorials/ui/create/adobe-applications/marketo.md) para completar su flujo de datos de [!DNL Marketo].