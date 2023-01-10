---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;entorno;detalles de entorno;
solution: Experience Platform
title: Grupo de campos de esquema Detalles del entorno
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles del entorno de ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL Detalles del entorno] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles del entorno] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) se utiliza para capturar información sobre los detalles de entorno relacionados con un evento de experiencia, como detalles del dispositivo, información del explorador, hora local y otra información geográfica.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [Device](../../data-types/device.md) | Describe una instancia de dispositivo, aplicación o explorador de dispositivo identificada que se puede rastrear entre sesiones, normalmente mediante cookies. |
| `environment` | [Entorno](../../data-types/environment.md) | Describe información sobre el contexto de situación de la observación de eventos, detallando específicamente información transitoria como las versiones de red o software. |
| `placeContext` | [Contexto del lugar](../../data-types/place-context.md) | Describe las circunstancias transitorias relacionadas con la observación del evento. Algunos ejemplos son la información específica de la configuración regional, como el tiempo, la hora local, el tráfico, el día de la semana, la jornada laboral frente a las vacaciones y las horas de trabajo. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
