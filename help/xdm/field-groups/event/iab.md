---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;iab;tcf;consentimiento;
solution: Experience Platform
title: Grupo de campos de consentimiento TCF 2.0 de IAB para esquemas de eventos
description: Este documento proporciona una descripción general del grupo de campos de esquema de consentimiento TCF 2.0 de IAB para la clase ExperienceEvent XDM.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# [!UICONTROL Consentimiento TCF 2.0 de IAB] grupo de campos para esquemas de eventos

>[!IMPORTANT]
>
>Este documento cubre el [!UICONTROL Consentimiento TCF 2.0 de IAB] grupo de campos de esquema para la clase XDM ExperienceEvent . Este grupo de campos solo debe utilizarse si tiene intención de rastrear eventos de cambio de consentimiento a lo largo del tiempo.
>
>Tenga en cuenta que los valores de consentimiento registrados en los datos de evento no se respetan en los flujos de trabajo de aplicación automática. Para que se realice la aplicación automática, los valores de consentimiento deben ingerirse en la clase de Perfil individual XDM y habilitarse para Perfil del cliente en tiempo real.
>
>Para el grupo de campos diseñado para la clase XDM Individual Profile, consulte lo siguiente [documento](../profile/iab.md) en su lugar.

[!UICONTROL Consentimiento TCF 2.0 de IAB] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) se utiliza para capturar una serie con marca de hora de cadenas de consentimiento IAB, con el fin de rastrear patrones de cambio de consentimiento a lo largo del tiempo.

![](../../images/field-groups/iab-event.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `consentStrings` | Matriz de [Cadenas de consentimiento](../../data-types/consent-string.md) | Matriz de valores de cadena de consentimiento asociados al evento. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía de [Compatibilidad con IAB TCF 2.0 en Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información sobre el caso de uso de este grupo de campos. Para obtener más información sobre el propio grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
