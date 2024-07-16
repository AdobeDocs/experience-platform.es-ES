---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;entorno;detalles de entorno;
solution: Experience Platform
title: Grupo de campos de esquema de detalles del entorno
description: Obtenga información sobre el grupo de campos de esquema Detalles del entorno de ExperienceEvent.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 2%

---


# [!UICONTROL Detalles del entorno] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles del entorno] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md) que se usa para capturar información con respecto a los detalles del entorno relacionados con un evento de experiencia, como detalles del dispositivo, información del explorador, hora local y otra información geográfica.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Describe un dispositivo, aplicación o instancia de explorador de dispositivo identificado que se puede rastrear a través de sesiones (normalmente, mediante cookies). |
| `environment` | [Entorno](../../data-types/environment.md) | Describe información acerca del contexto situacional de la observación de eventos, detallando específicamente información transitoria como la red o las versiones de software. |
| `placeContext` | [Contexto del lugar](../../data-types/place-context.md) | Describe las circunstancias transitorias relacionadas con la observación de eventos. Algunos ejemplos son información específica de la configuración regional, como el tiempo, la hora local, el tráfico, el día de la semana, los días laborales frente a los festivos y el horario laboral. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
