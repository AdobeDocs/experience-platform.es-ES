---
title: Grupo de campos de esquema de detalles de campaña empresarial de XDM
description: Obtenga información acerca del grupo de campos de esquema Detalles de la campaña empresarial de XDM.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# [!UICONTROL Detalles de XDM Business Campaign] grupo de campos de esquema

[!UICONTROL Detalles de XDM Business Campaign] es un grupo de campos de esquema estándar para la clase [[!UICONTROL XDM Business Campaign]](../../classes/b2b/business-campaign.md), que captura información detallada acerca de una campaña empresarial.

![La estructura del grupo de campos Detalles de la campaña empresarial de XDM tal como aparece en la interfaz de usuario](../../images/field-groups/b2b/business-campaign-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Moneda]](../../data-types/currency.md) | Representa el coste real de la campaña empresarial. |
| `budgetedCost` | [[!UICONTROL Moneda]](../../data-types/currency.md) | Representa el costo presupuestado de la campaña empresarial. |
| `expectedRevenue` | [[!UICONTROL Moneda]](../../data-types/currency.md) | Representa los ingresos que se espera que genere la campaña empresarial. |
| `parentCampaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | El ID compuesto de una campaña principal, si corresponde. |
| `campaignEndDate` | [!UICONTROL DateTime] | Una marca de tiempo ISO 8601 de cuándo terminó la campaña, o terminará. |
| `campaignProgressionName` | [!UICONTROL Cadena] | Nombre de la progresión de la campaña. |
| `campaignStartDate` | [!UICONTROL DateTime] | Una marca de tiempo ISO 8601 de cuándo comenzó la campaña, o comenzará. |
| `campaignStatus` | [!UICONTROL Cadena] | El estado actual de la campaña. |
| `channelName` | [!UICONTROL Cadena] | El nombre del canal asociado con esta campaña. |
| `expectedResponse` | [!UICONTROL Cadena] | La respuesta esperada para la campaña. |
| `integrationPartnerName` | [!UICONTROL Cadena] | El nombre del socio que se ha integrado con esta campaña. |
| `isActive` | [!UICONTROL Booleano] | Indica si esta campaña está activa. |
| `isDeleted` | [!UICONTROL Booleano] | Indica si esta campaña se ha eliminado en el Marketo Engage.<br><br>Al usar el [conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Al establecer `isDeleted` en `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |
| `lastActivityDate` | [!UICONTROL DateTime] | Una marca de tiempo ISO 8601 de la última actividad asociada con la campaña. |
| `timeZone` | [!UICONTROL Cadena] | Zona horaria en la que opera la campaña. |
| `timeZoneDelivery` | [!UICONTROL Cadena] | Zona horaria de envío en la que opera la campaña. |
| `timeZoneName` | [!UICONTROL Cadena] | El nombre de la zona horaria en la que opera la campaña. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Una marca de tiempo ISO 8601 de la última sincronización del historial del seminario web para esta campaña. |
| `webinarHistorySyncStatus` | [!UICONTROL Cadena] | Estado de la sincronización del historial del seminario web de esta campaña. |
| `webinarSessionDescription` | [!UICONTROL Cadena] | Una descripción de la sesión del seminario web asociada con esta campaña. |
| `webinarSessionName` | [!UICONTROL Cadena] | Nombre de la sesión del seminario web asociada con esta campaña. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
