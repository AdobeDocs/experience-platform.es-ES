---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;ExperienceEvent;campos;esquemas;esquemas;diseño de esquema;mezcla;mezcla;entorno;detalles del entorno;
solution: Experience Platform
title: Mezcla de detalles de entorno
topic-legacy: overview
description: Este documento proporciona una descripción general de la combinación de Detalles del entorno de ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---

# [!UICONTROL Environment Details] mixto

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../name-updates.md) para obtener más información.

[!UICONTROL Environment Details] es una combinación estándar para el  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) cliente que captura información relacionada con los detalles del entorno relacionados con un evento de experiencia, como detalles del dispositivo, información del explorador, hora local y otra información geográfica.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Describe una instancia de dispositivo, aplicación o explorador de dispositivo identificada que se puede rastrear entre sesiones, normalmente mediante cookies. |
| `environment` | [Entorno](../../data-types/environment.md) | Describe información sobre el contexto de situación de la observación de eventos, detallando específicamente información transitoria como las versiones de red o software. |
| `placeContext` | [Contexto del lugar](../../data-types/place-context.md) | Describe las circunstancias transitorias relacionadas con la observación del evento. Algunos ejemplos son la información específica de la configuración regional, como el tiempo, la hora local, el tráfico, el día de la semana, la jornada laboral frente a las vacaciones y las horas de trabajo. |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
