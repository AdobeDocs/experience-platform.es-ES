---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;iab;tcf;consentimiento;
solution: Experience Platform
title: Grupo de campos de consentimiento de IAB TCF 2.0 para esquemas de eventos
description: Obtenga información acerca del grupo de campos Esquema de consentimiento TCF 2.0 de IAB para la clase XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL Grupo de campos de consentimiento TCF de IAB 2.0] para esquemas de eventos

>[!IMPORTANT]
>
>Este documento cubre el grupo de campos de esquema [!UICONTROL Consentimiento TCF 2.0 de IAB] para la clase XDM ExperienceEvent. Este grupo de campos solo debe utilizarse si se desea rastrear los eventos de cambio de consentimiento a lo largo del tiempo.
>
>Tenga en cuenta que los valores de consentimiento registrados en los datos de evento no se respetan en los flujos de trabajo de aplicación automática. Para que se aplique automáticamente, los valores de consentimiento deben introducirse en la clase de perfil individual de XDM y habilitarse para el perfil del cliente en tiempo real.
>
>Para el grupo de campos destinado a la clase Perfil individual XDM, consulte el siguiente [documento](../profile/iab.md) en su lugar.

El consentimiento [!UICONTROL IAB TCF 2.0] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) que se usa para capturar una serie con marca de tiempo de cadenas de consentimiento IAB, con el fin de rastrear patrones de cambio de consentimiento a lo largo del tiempo.

![](../../images/field-groups/iab-event.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `consentStrings` | Matriz de [cadenas de consentimiento](../../data-types/consent-string.md) | Una matriz de valores de cadena de consentimiento asociados al evento. |

{style="table-layout:auto"}

Consulte la guía sobre la compatibilidad con [IAB TCF 2.0 en Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información sobre el caso de uso de este grupo de campos. Para obtener más información sobre el propio grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
