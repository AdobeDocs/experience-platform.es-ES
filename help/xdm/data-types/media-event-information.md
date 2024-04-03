---
title: Tipo de datos de información de evento de medios
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de información de eventos de medios.
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL Información de evento de medios] tipo de datos

[!UICONTROL Información de evento de medios] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe información de detalles de medios relacionada con el evento de experiencia.

![Diagrama del tipo de datos Información de evento de medios.](../images/data-types/media-event-information.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Información detallada de los medios relacionada con el evento de experiencia. Este tipo de datos se utiliza tanto para [recopilación de datos de medios](./media-collection-details.md) y [informes de datos de medios](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL Cadena] | Hora a la que se produjo un evento multimedia. |
| `mediaEventType` | [!UICONTROL Cadena] | El tipo de evento de medios. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
