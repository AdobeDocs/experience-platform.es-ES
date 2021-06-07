---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;entorno;detalles de entorno;
solution: Experience Platform
title: Grupo de campos de esquema Detalles del entorno
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del entorno de ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos Environment ] Detailsschema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL Environment ] Detail es un grupo de campos de esquema estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) clasificado que captura información relacionada con los detalles de entorno relacionados con un Evento de experiencia, como detalles del dispositivo, información del explorador, hora local y otra información geográfica.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Describe una instancia de dispositivo, aplicación o explorador de dispositivo identificada que se puede rastrear entre sesiones, normalmente mediante cookies. |
| `environment` | [Entorno](../../data-types/environment.md) | Describe información sobre el contexto de situación de la observación de eventos, detallando específicamente información transitoria como las versiones de red o software. |
| `placeContext` | [Contexto del lugar](../../data-types/place-context.md) | Describe las circunstancias transitorias relacionadas con la observación del evento. Algunos ejemplos son la información específica de la configuración regional, como el tiempo, la hora local, el tráfico, el día de la semana, la jornada laboral frente a las vacaciones y las horas de trabajo. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
