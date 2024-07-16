---
title: Tipo de datos de colección de detalles del capítulo
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de recopilación de detalles del capítulo.
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL Detalles del capítulo] Tipo de datos de colección

La colección [!UICONTROL Detalles del capítulo] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe varios atributos relacionados con capítulos o segmentos dentro del contenido multimedia. Utilice el tipo de datos de colección [!UICONTROL Detalles del capítulo] para capturar detalles como el nombre del capítulo, el desplazamiento, la duración y el índice del capítulo. Los campos de recopilación de medios capturan datos y los envían a otros servicios de Adobe para un procesamiento posterior.

![Un diagrama del tipo de datos de la colección de detalles del capítulo.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Requerido | Descripción |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Duración O Longitud Del Capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | entero | Sí | La duración del capítulo en segundos. |
| [[!UICONTROL Nombre de capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | cadena | No | El nombre del capítulo y/o segmento. |
| [[!UICONTROL Desplazamiento de capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | entero | Sí | El desplazamiento del capítulo dentro del contenido (en segundos) desde el inicio. |
| [[!UICONTROL Posición del capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | entero | Sí | La posición (índice, entero) del capítulo dentro del contenido. |

{style="table-layout:auto"}
