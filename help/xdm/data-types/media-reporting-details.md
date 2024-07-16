---
title: Tipo de datos de detalles de Media Reporting
description: Obtenga información sobre el tipo de datos del modelo de datos de experiencia (XDM) de Detalles de creación de informes de medios.
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# [!UICONTROL Detalles de informes de medios] tipo de datos

>[!NOTE]
>
>Los campos de recopilación de medios capturan datos y los envían a otros servicios de Adobe para un procesamiento posterior. Los servicios de Adobe utilizan los campos de creación de informes de contenidos para analizar los campos de recopilación de contenidos que envían los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican.

[!UICONTROL Detalles de informes de medios] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles esenciales acerca de los eventos de reproducción de medios. Utilice el tipo de datos [!UICONTROL Detalles de informes de medios] para capturar detalles como la posición del cabezal de reproducción dentro del contenido, identificadores de sesión únicos y varias propiedades anidadas relacionadas con la sesión, entre otras. Este tipo de datos proporciona una visión general completa de la experiencia de reproducción que permite realizar un seguimiento y análisis de los patrones de consumo de medios y los eventos asociados durante las sesiones de reproducción.

>[!NOTE]
>
>Los campos que se mencionan a continuación no se utilizan directamente para crear solicitudes. En su lugar, la recopilación de campos enviados a Adobe Experience Platform o Adobe Analytics se monta a partir de los datos de solicitud y las métricas se incorporan o procesan en la infraestructura del servidor. Aunque Platform recopila varios tipos de eventos de usuario, los informes devueltos se centran en eventos específicos, como `media.sessionStart`, `media.adStart` y `media.sessionComplete`. Esto significa que, aunque transmite 12 tipos de eventos durante la recopilación, los informes solo presentan desgloses basados en los cinco eventos enumerados a continuación.

+++Seleccione esta opción para mostrar un diagrama del tipo de datos de [!UICONTROL Detalles de informes de medios].
![Un diagrama del tipo de datos de [!UICONTROL Detalles de creación de informes de medios].](../images/data-types/media-reporting-details.png)
+++

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Detalles de Advertising] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Los detalles de Advertising hacen referencia a información específica relacionada con las actividades publicitarias durante el evento de experiencia. Esto incluye metadatos de publicidad, datos específicos de segmentación y métricas de rendimiento. |
| [!UICONTROL Detalles de Advertising Pod] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Los detalles del pod de Advertising contienen información sobre pods de publicidad dentro del evento de experiencia. Proporciona información sobre la secuencia de anuncios, el contenido y las métricas de participación. |
| [!UICONTROL Detalles del capítulo] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Detalles del capítulo captura datos relacionados con los capítulos o las partes segmentadas del contenido. Proporciona información sobre marcadores de capítulo, escalas de tiempo y metadatos asociados. |
| [!UICONTROL Lista De Estados] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | La propiedad States es una matriz que captura varios estados a lo largo del evento de experiencia. Esta propiedad proporciona datos secuenciales sobre la reproducción, las acciones del usuario o los cambios de contenido. |
| [!UICONTROL Detalles De Datos Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | Los detalles de datos de QoE (calidad de experiencia) capturan métricas relacionadas con el rendimiento y datos de experiencia del usuario. Proporciona perspectivas sobre la calidad, la capacidad de respuesta y las interacciones del usuario. |
| [!UICONTROL Detalles de la sesión] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Los detalles de la sesión incluyen información completa asociada con el evento de experiencia, que ofrece perspectivas sobre las interacciones del usuario, la duración y los datos contextuales relevantes para la sesión de reproducción. |
| [!UICONTROL Metadatos personalizados] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Los metadatos personalizados contienen metadatos adicionales o definidos por el usuario asociados al evento de experiencia. Estos metadatos permiten incluir datos personalizados o específicos en el contexto de evento. |
| [!UICONTROL Cabezal de reproducción] | `playhead` | entero | El cabezal de reproducción representa la posición de reproducción actual dentro del contenido multimedia. Para el contenido en directo, indica el segundo del día actual (0 &lt;= cabezal de reproducción &lt; 86400). Para el contenido grabado, refleja el segundo actual de la duración del contenido (0 &lt;= cabezal de reproducción &lt; longitud del contenido). |

{style="table-layout:auto"}
