---
title: Tipo de datos de detalles de recopilación de medios
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de detalles de recopilación de medios.
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# [!UICONTROL Detalles de recopilación de medios] tipo de datos

[!UICONTROL Detalles de recopilación de medios] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles esenciales sobre los eventos de reproducción de medios. Utilice el [!UICONTROL Detalles de recopilación de medios] tipo de datos para capturar detalles como la posición del cursor de reproducción dentro del contenido, identificadores de sesión únicos y varias propiedades anidadas relacionadas con la sesión, entre otras. Este tipo de datos proporciona una visión general completa de la experiencia de reproducción que permite realizar un seguimiento y análisis de los patrones de consumo de medios y los eventos asociados durante las sesiones de reproducción.

>[!NOTE]
>
>Los campos de recopilación de medios capturan datos y los envían a otros servicios de Adobe para un procesamiento posterior. Los servicios de Adobe utilizan los campos de creación de informes de contenidos para analizar los campos de recopilación de contenidos que envían los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican.

+++Seleccione para mostrar un diagrama de la [!UICONTROL Detalles de recopilación de medios] tipo de datos.
![Un diagrama de la [!UICONTROL Información de detalles de recopilación de medios] tipo de datos.](../images/data-types/media-collection-details.png)
+++

| Nombre para mostrar | Propiedad | Eventos necesarios para | Tipo de datos | Descripción |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Detalles de publicidad] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Colección](./advertising-details-collection.md) | Los detalles publicitarios hacen referencia a información específica relacionada con las actividades publicitarias durante el evento de experiencia. Esto incluye metadatos de publicidad, datos específicos de segmentación y métricas de rendimiento. |
| [!UICONTROL Detalles de Advertising Pod] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Colección](./advertising-pod-details-collection.md) | Los detalles del pod de publicidad contienen información sobre los pods de publicidad dentro del evento de experiencia. Proporciona información sobre la secuencia de anuncios, el contenido y las métricas de participación. |
| [!UICONTROL Detalles del capítulo] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Colección](./chapter-details-collection.md) | Detalles del capítulo captura datos relacionados con los capítulos o las partes segmentadas del contenido. Proporciona información sobre marcadores de capítulo, escalas de tiempo y metadatos asociados. |
| [!UICONTROL Detalles del error] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Colección](./error-details-collection.md) | Los detalles del error contienen información relativa a los errores encontrados durante el evento de experiencia. Esto incluye códigos de error, descripciones, marcas de tiempo y datos contextuales relevantes. |
| [!UICONTROL Fin de lista de estados] | `statesEnd` | Utilizado en `statesUpdate` | [[!UICONTROL statesEnd] - Colección](./list-of-states-end-collection.md) | El final de estados proporciona una matriz para enumerar los estados al final del evento de experiencia. Contiene detalles sobre los estados de reproducción finales o el estado del contenido. |
| [!UICONTROL Inicio de lista de estados] | `statesStart` | Utilizado en `statesUpdate` | [[!UICONTROL statesStart] - Colección](./list-of-states-start-collection.md) | Inicio de estados proporciona una matriz para enumerar los estados al principio del evento de experiencia. Incluye datos relacionados con la reproducción, las acciones del usuario o aspectos específicos del contenido. |
| [!UICONTROL Detalles de datos de Qoe] | `qoeDataDetails` | Opcional para todos | [[!UICONTROL qoeDataDetails] - Colección](./qoe-data-details-collection.md) | Los detalles de datos de QoE (calidad de experiencia) capturan métricas relacionadas con el rendimiento y datos de experiencia del usuario. Proporciona perspectivas sobre la calidad, la capacidad de respuesta y las interacciones del usuario. |
| [!UICONTROL Detalles de sesión] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Colección](./session-details-collection.md) | Los detalles de la sesión incluyen información completa asociada con el evento de experiencia, que ofrece perspectivas sobre las interacciones del usuario, la duración y los datos contextuales relevantes para la sesión de reproducción. |
| [!UICONTROL Los metadatos personalizados] | `customMetadata` | Opcional para `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Colección](./custom-metadata-details-collection.md) | Los metadatos personalizados contienen metadatos adicionales o definidos por el usuario asociados al evento de experiencia. Estos metadatos permiten incluir datos personalizados o específicos en el contexto de evento. |
| [!UICONTROL ID de sesión de contenido] | `sessionID` | Todos los eventos **excepto** `sessionStart` y contenido descargado. | string | El ID de sesión de contenido identifica de forma exclusiva una instancia de un flujo de contenido durante una sesión de reproducción individual. Sirve como identificador distintivo para rastrear y administrar la experiencia de reproducción específica asociada a un usuario o visualizador.<br><em>Nota:<em>`sessionId` se envía en todos los eventos, excepto en `sessionStart` y para todos los eventos descargados. |
| [!UICONTROL Cabezal De Reproducción] | `playhead` | Todos los eventos | entero | El cabezal de reproducción representa la posición de reproducción actual dentro del contenido multimedia. Para el contenido en directo, indica el segundo del día actual (0 &lt;= cabezal de reproducción &lt; 86400). Para el contenido grabado, refleja el segundo actual de la duración del contenido (0 &lt;= cabezal de reproducción &lt; longitud del contenido). |

{style="table-layout:auto"}
