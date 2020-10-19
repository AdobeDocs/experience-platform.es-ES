---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: Mezcla de detalles del entorno de ExperienceEvent
topic: overview
description: Este documento proporciona una visión general de la combinación de Detalles del Entorno de ExperienceEvent.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# [!UICONTROL Mezcla de detalles] del entorno de ExperienceEvent

[!UICONTROL Los detalles] del entorno de ExperienceEvent son una combinación estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/individual-profile.md) que se utiliza para capturar información relativa a los detalles del entorno relacionados con un Evento de experiencias, como detalles del dispositivo, información del explorador, hora local y otra información geográfica.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [Device](../../data-types/device.md) | Describe una instancia de dispositivo, aplicación o navegador de dispositivo identificada que se puede rastrear en varias sesiones, normalmente mediante cookies. |
| `environment` | [Entorno](../../data-types/environment.md) | Describe información sobre el contexto situacional de la observación de evento, detallando específicamente información transitoria como las versiones de red o software. |
| `placeContext` | [Colocar contexto](../../data-types/place-context.md) | Describe las circunstancias transitorias relacionadas con la observación de evento. Algunos ejemplos son la información específica de la configuración regional, como el tiempo, la hora local, el tráfico, el día de la semana, el día laboral o el día festivo, y las horas de trabajo. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
