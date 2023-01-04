---
title: Grupo de campos de esquema de detalles de miembro de XDM Business Campaign
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del miembro de XDM Business Campaign.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# [!UICONTROL Detalles del miembro de la campaña empresarial XDM] grupo de campos de esquema

[!UICONTROL Detalles del miembro de la campaña empresarial XDM] es un grupo de campos de esquema estándar para la variable [[!UICONTROL Miembros de XDM Business Campaign] class](../../classes/b2b/business-campaign-members.md), que captura información detallada sobre una campaña empresarial.

![La estructura del grupo de campos Detalles del miembro de la campaña empresarial XDM tal como aparece en la interfaz de usuario](../../images/field-groups/b2b/business-campaign-member-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | El ID compuesto de la campaña que adquirió este miembro de la campaña. |
| `acquiredByCampaignID` | [!UICONTROL Cadena] | Un identificador de cadena para la campaña que adquirió este miembro de la campaña. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Marca de tiempo ISO 8601 del momento en que la persona respondió por primera vez a la campaña. |
| `hasReachedSuccess` | [!UICONTROL Booleana] | Indica si este miembro de la campaña ha resultado en una conversión correcta. |
| `hasResponded` | [!UICONTROL Booleana] | Indica si este miembro de la campaña ha respondido a la campaña. |
| `isDeleted` | [!UICONTROL Booleana] | Indica si este miembro de la campaña se ha eliminado en el Marketo Engage.<br><br>Al usar la variable [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Si configura `isDeleted` a `true`, puede utilizar el campo para filtrar qué registros se han eliminado de sus orígenes al consultar el lago de datos. |
| `isExhausted` | [!UICONTROL Booleana] | Indica si este miembro de la campaña ha agotado todas las interacciones de la campaña. |
| `lastStatus` | [!UICONTROL Cadena] | El último estado del miembro de la campaña. |
| `memberStatus` | [!UICONTROL Cadena] | Estado actual del miembro de la campaña. |
| `memberStatusReason` | [!UICONTROL Cadena] | Motivo detrás del estado actual del miembro de la campaña. |
| `membershipDate` | [!UICONTROL DateTime] | Motivo detrás del estado actual del miembro de la campaña. |
| `nurtureCadence` | [!UICONTROL Cadena] | El intervalo de tiempo para la información relacionada con la campaña que se presentará al miembro de la campaña. |
| `nurtureTrackName` | [!UICONTROL Cadena] | Nombre del programa de crianza al que está sujeto este miembro de la campaña. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Marca de fecha y hora ISO 8601 para el momento en que se realizó una conversión exitosa para el miembro de la campaña. |
| `webinarConfirmationUrl` | [!UICONTROL Cadena] | Dirección URL de confirmación del seminario web para el miembro de la campaña. |
| `webinarRegistrationID` | [!UICONTROL Cadena] | El ID de registro del seminario web para el miembro de la campaña. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
