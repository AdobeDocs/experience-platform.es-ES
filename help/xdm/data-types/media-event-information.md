---
title: Tipo de datos de información de evento de medios
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de información de eventos de medios.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL Información de evento de medios] tipo de datos

[!UICONTROL Información de evento de medios] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe información de detalles de medios relacionada con el evento de experiencia.

![Diagrama del tipo de datos Información de evento de medios.](../images/data-types/media-event-information.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | Información detallada de los medios relacionada con el evento de experiencia. |
| `mediaEventTimestamp` | [!UICONTROL Cadena] | Hora a la que se produjo un evento multimedia. |
| `mediaEventType` | [!UICONTROL Cadena] | El tipo de evento de medios. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
