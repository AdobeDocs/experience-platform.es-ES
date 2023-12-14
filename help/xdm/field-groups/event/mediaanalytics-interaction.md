---
title: Grupo de campos de esquema de detalles de interacción de Media Analytics
description: Obtenga información acerca del grupo de campos de esquema Detalles de interacción de Media Analytics.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL Detalles de interacción de Media Analytics] grupo de campos de esquema

[!UICONTROL Detalles de interacción de Media Analytics] es un grupo de campos de esquema estándar para [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). Utilice este grupo de campos para capturar campos de datos enriquecidos que supervisan y analizan exhaustivamente las interacciones con contenido de medios en varias plataformas o canales.

![Un diagrama de esquema del [!UICONTROL Detalles de interacción de Media Analytics] grupo de campos de esquema.](../../images/field-groups/mediaanalytics-interaction.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---| --- | --- | --- |
| [!UICONTROL Detalles de recopilación de medios] | `mediaCollection` | [[!UICONTROL Información de detalles de medios]](../../data-types/media-details-information.md) | Atributos relacionados con una colección de elementos de medios. |
| [!UICONTROL Detalles de informes de medios] | `mediaReporting` | [[!UICONTROL Información de detalles de medios]](../../data-types/media-details-information.md) | Detalles de creación de informes y métricas asociadas con el contenido de medios. |
| [!UICONTROL Lista De Eventos De Contenido Descargado De Colecciones De Medios] | `mediaDownloadedEvents` | [!UICONTROL Matriz] de [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Eventos que rastrean la descarga de contenido dentro de la colección de medios. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
