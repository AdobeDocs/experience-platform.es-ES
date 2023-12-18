---
title: Grupo de campos de esquema de detalles de miembros de campaña empresarial de XDM
description: Obtenga información acerca del grupo de campos de esquema Detalles de miembros de XDM Business Campaign.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 4%

---

# [!UICONTROL Detalles del miembro de la campaña empresarial de XDM] grupo de campos de esquema

[!UICONTROL Detalles del miembro de la campaña empresarial de XDM] es un grupo de campos de esquema estándar para [[!UICONTROL Miembros de campaña empresarial de XDM] clase](../../classes/b2b/business-campaign-members.md), que captura información detallada acerca de una campaña empresarial.

![La estructura del grupo de campos Detalles del miembro de la campaña empresarial de XDM tal como aparece en la interfaz de usuario](../../images/field-groups/b2b/business-campaign-member-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | El ID compuesto de la campaña que adquirió este miembro de la campaña. |
| `acquiredByCampaignID` | [!UICONTROL Cadena] | Un identificador de cadena para la campaña que adquirió este miembro de la campaña. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Una marca de tiempo ISO 8601 del momento en el que la persona respondió a la campaña por primera vez. |
| `hasReachedSuccess` | [!UICONTROL Booleana] | Indica si este miembro de la campaña ha resultado en una conversión correcta. |
| `hasResponded` | [!UICONTROL Booleana] | Indica si este miembro de la campaña ha respondido a la campaña. |
| `isDeleted` | [!UICONTROL Booleana] | Indica si este miembro de la campaña se ha eliminado en el Marketo Engage.<br><br>Al usar el [Conector de origen de Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md)Sin embargo, cualquier registro que se elimine en Marketo se reflejará automáticamente en el perfil del cliente en tiempo real. Sin embargo, los registros relacionados con estos perfiles pueden persistir en el lago de datos. Por configuración `isDeleted` hasta `true`Sin embargo, puede utilizar el campo para filtrar qué registros se han eliminado de las fuentes al consultar el lago de datos. |
| `isExhausted` | [!UICONTROL Booleana] | Indica si este miembro de la campaña ha agotado todas las interacciones de la campaña. |
| `lastStatus` | [!UICONTROL Cadena] | El último estado del miembro de la campaña. |
| `memberStatus` | [!UICONTROL Cadena] | El estado actual del miembro de la campaña. |
| `memberStatusReason` | [!UICONTROL Cadena] | El motivo detrás del estado actual del miembro de la campaña. |
| `membershipDate` | [!UICONTROL DateTime] | El motivo detrás del estado actual del miembro de la campaña. |
| `nurtureCadence` | [!UICONTROL Cadena] | La cadencia temporal de la información relacionada con la campaña que se va a presentar al miembro de la campaña. |
| `nurtureTrackName` | [!UICONTROL Cadena] | El nombre del programa de nutrición al que está sujeto este miembro de la campaña. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Una marca de tiempo ISO 8601 para el momento en el que se realizó una conversión correcta para el miembro de la campaña. |
| `webinarConfirmationUrl` | [!UICONTROL Cadena] | La URL de confirmación del seminario web del miembro de la campaña. |
| `webinarRegistrationID` | [!UICONTROL Cadena] | El ID de registro del seminario web del miembro de la campaña. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
