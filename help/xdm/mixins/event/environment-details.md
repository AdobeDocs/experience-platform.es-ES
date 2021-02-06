---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;diseño de Esquema;mezcla;combinación;entorno;detalles de entorno;
solution: Experience Platform
title: Mezcla de detalles de entorno
topic: overview
description: Este documento proporciona una visión general de la combinación de Detalles del Entorno de ExperienceEvent.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---


# [!UICONTROL Entorno ] Detailsmixin

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento en [actualizaciones de nombres de mezcla](../name-updates.md) para obtener más información.

[!UICONTROL Entorno ] Detalla una combinación estándar para los  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) alumnos para capturar información relacionada con los detalles de entorno relacionados con un Evento de experiencias, como detalles del dispositivo, información del explorador, hora local y otra información geográfica.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Describe una instancia de dispositivo, aplicación o navegador de dispositivo identificada que se puede rastrear en varias sesiones, normalmente mediante cookies. |
| `environment` | [Entorno](../../data-types/environment.md) | Describe información sobre el contexto situacional de la observación de evento, detallando específicamente información transitoria como las versiones de red o software. |
| `placeContext` | [Colocar contexto](../../data-types/place-context.md) | Describe las circunstancias transitorias relacionadas con la observación de evento. Algunos ejemplos son la información específica de la configuración regional, como el tiempo, la hora local, el tráfico, el día de la semana, el día laboral o el día festivo, y las horas de trabajo. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
