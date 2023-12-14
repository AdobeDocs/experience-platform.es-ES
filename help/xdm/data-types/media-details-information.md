---
title: Tipo de datos de información de detalles de medios
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de información de detalles de medios.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# [!UICONTROL Información de detalles de medios] tipo de datos

[!UICONTROL Información de detalles de medios] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles esenciales sobre los eventos de reproducción de medios. Utilice el [!UICONTROL Información de detalles de medios] tipo de datos para capturar detalles como la posición del cursor de reproducción dentro del contenido, identificadores de sesión únicos y varias propiedades anidadas relacionadas con la sesión, entre otras. Este tipo de datos proporciona una visión general completa de la experiencia de reproducción, que permite realizar un seguimiento y análisis de los patrones de consumo de medios y los eventos asociados durante las sesiones de reproducción.

+++Seleccione para mostrar un diagrama de la [!UICONTROL Información de detalles de medios] tipo de datos.
![Un diagrama de la [!UICONTROL Información de detalles de medios] tipo de datos.](../images/data-types/media-details-information.png)
+++

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Cabezal De Reproducción] | `playhead` | entero | El cabezal de reproducción representa la posición de reproducción actual dentro del contenido multimedia. Para el contenido en directo, indica el segundo del día actual (0 &lt;= cabezal de reproducción &lt; 86400). Para el contenido grabado, refleja el segundo actual de la duración del contenido (0 &lt;= cabezal de reproducción &lt; longitud del contenido). |
| [!UICONTROL ID de sesión de contenido] | `sessionID` | string | El ID de sesión de contenido identifica de forma exclusiva una instancia de un flujo de contenido durante una sesión de reproducción individual. Sirve como identificador distintivo para rastrear y administrar la experiencia de reproducción específica asociada a un usuario o visualizador. |
| [!UICONTROL Detalles de sesión] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | Los detalles de la sesión incluyen información completa asociada con el evento de experiencia, que ofrece perspectivas sobre las interacciones del usuario, la duración y los datos contextuales relevantes para la sesión de reproducción. |
| [!UICONTROL Detalles de publicidad] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | Los detalles publicitarios hacen referencia a información específica relacionada con las actividades publicitarias durante el evento de experiencia. Esto incluye metadatos de publicidad, datos específicos de segmentación y métricas de rendimiento. |
| [!UICONTROL Detalles de Advertising Pod] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | Los detalles del pod de publicidad contienen información sobre los pods de publicidad dentro del evento de experiencia. Proporciona información sobre la secuencia de anuncios, el contenido y las métricas de participación. |
| [!UICONTROL Detalles del capítulo] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | Detalles del capítulo captura datos relacionados con los capítulos o las partes segmentadas del contenido. Proporciona información sobre marcadores de capítulo, escalas de tiempo y metadatos asociados. |
| [!UICONTROL Detalles del error] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | Los detalles del error contienen información relativa a los errores encontrados durante el evento de experiencia. Esto incluye códigos de error, descripciones, marcas de tiempo y datos contextuales relevantes. |
| [!UICONTROL Detalles de datos de Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | Los detalles de datos de QoE (calidad de experiencia) capturan métricas relacionadas con el rendimiento y datos de experiencia del usuario. Proporciona perspectivas sobre la calidad, la capacidad de respuesta y las interacciones del usuario. |
| [!UICONTROL Inicio de lista de estados] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Inicio de estados proporciona una matriz para enumerar los estados al principio del evento de experiencia. Incluye datos relacionados con la reproducción, las acciones del usuario o aspectos específicos del contenido. |
| [!UICONTROL Fin de lista de estados] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | El final de estados proporciona una matriz para enumerar los estados al final del evento de experiencia. Contiene detalles sobre los estados de reproducción finales o el estado del contenido. |
| [!UICONTROL Lista De Estados] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | La propiedad States es una matriz que captura varios estados a lo largo del evento de experiencia. Esta propiedad proporciona datos secuenciales sobre la reproducción, las acciones del usuario o los cambios de contenido. |
| [!UICONTROL Los metadatos personalizados] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | Los metadatos personalizados contienen metadatos adicionales o definidos por el usuario asociados al evento de experiencia. Estos metadatos permiten incluir datos personalizados o específicos en el contexto de evento. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
