---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;iab;tcf;consentimiento;
solution: Experience Platform
title: Grupo de campos de esquema de consentimiento TCF 2.0 de IAB
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema de consentimiento TCF 2.0 de IAB para la clase ExperienceEvent XDM.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# [!UICONTROL Grupo de campos de esquema de ] consentimiento TCF 2.0 de IAB

>[!IMPORTANT]
>
>Este documento cubre el grupo de campos de esquema [!UICONTROL IAB TCF 2.0 Consent] para la clase XDM ExperienceEvent. Este grupo de campos solo debe utilizarse si tiene intención de rastrear eventos de cambio de consentimiento a lo largo del tiempo.
>
>Tenga en cuenta que los valores de consentimiento registrados en los datos de evento no se respetan en los flujos de trabajo de aplicación automática. Para que se realice la aplicación automática, los valores de consentimiento deben ingerirse en la clase de Perfil individual XDM y habilitarse para Perfil del cliente en tiempo real.
>
>Para el grupo de campos destinado a la clase de perfil individual XDM, consulte el siguiente [documento](../profile/iab.md) en su lugar.

[!UICONTROL IAB TCF 2.0 ] Confirma un grupo de campos de esquema estándar para los  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) clientes para capturar una serie con marca de tiempo de cadenas de consentimiento IAB, con el fin de rastrear patrones de cambio de consentimiento a lo largo del tiempo.

![](../../images/field-groups/iab-event.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `consentStrings` | Matriz de [cadenas de consentimiento](../../data-types/consent-string.md) | Matriz de valores de cadena de consentimiento asociados al evento. |

{style=&quot;table-layout:auto&quot;}

Consulte la guía sobre la compatibilidad con [IAB TCF 2.0 en Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información sobre el caso de uso de este grupo de campos. Para obtener más información sobre el propio grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
