---
title: Grupo de campos de esquema de detalles de interacción de Media Analytics
description: Obtenga información acerca del grupo de campos de esquema Detalles de interacción de Media Analytics.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---

# [!UICONTROL Detalles de interacción de MediaAnalytics] grupo de campos de esquema

[!UICONTROL Detalles de interacción de MediaAnalytics] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md). Utilice este grupo de campos para capturar campos de datos enriquecidos que supervisan y analizan exhaustivamente las interacciones con contenido de medios en varias plataformas o canales.

![Un diagrama de esquema del grupo de campos de esquema [!UICONTROL Detalles de interacción de MediaAnalytics].](../../images/field-groups/mediaanalytics-interaction.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|---| --- | --- | --- |
| [!UICONTROL Detalles de recopilación de medios] | `mediaCollection` | [[!UICONTROL Detalles de recopilación de medios]](../../data-types/media-collection-details.md) | Atributos relacionados con una colección de elementos de medios. Utilice los campos de recopilación de medios para capturar datos y enviarlos a otros servicios de Adobe para un procesamiento posterior. |
| [!UICONTROL Detalles de informes de medios] | `mediaReporting` | [[!UICONTROL Detalles de informes de medios]](../../data-types/media-reporting-details.md) | Detalles de creación de informes y métricas asociadas con el contenido de medios. * Los servicios de Adobe utilizan los campos de Media Reporting para analizar los campos de Media Collection enviados por los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican. |
| [!UICONTROL Lista De Eventos De Contenido Descargado De La Colección De Medios] | `mediaDownloadedEvents` | [!UICONTROL Matriz] de [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Eventos que rastrean la descarga de contenido dentro de la colección de medios. |

{style="table-layout:auto"}

>[!TIP]
>
>Puede ocultar campos que no utilice la API de Media Edge. Al ocultar estos campos, el esquema es más fácil de leer y comprender, pero no es obligatorio. Estos campos solo hacen referencia a los del grupo de campos [!UICONTROL Detalles de interacción de MediaAnalytics]. Para mejorar la legibilidad en la interfaz de usuario de Experience Platform, siga las instrucciones de la [documentación de Media Analytics sobre cómo ocultar campos sin usar](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
