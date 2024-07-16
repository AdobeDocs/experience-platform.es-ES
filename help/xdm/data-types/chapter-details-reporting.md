---
title: Detalles del capítulo Tipo de datos de informes
description: Obtenga información sobre los detalles del capítulo Creación de informes sobre el tipo de datos del Modelo de datos de experiencia (XDM).
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# [!UICONTROL Detalles del capítulo] Tipo de datos de informe

[!UICONTROL Detalles del capítulo] La creación de informes es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe varios atributos relacionados con capítulos o segmentos dentro del contenido multimedia. Utilice el tipo de datos de informe [!UICONTROL Detalles del capítulo] para capturar detalles como el nombre del capítulo, la duración, la posición, el ID, el estado de reproducción (iniciada/finalizada) y el tiempo empleado en cada capítulo. Los servicios de Adobe utilizan los campos de creación de informes de contenidos para analizar los campos de recopilación de contenidos que envían los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican.

![Un diagrama del tipo de datos del informe de detalles del capítulo.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por el Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Capítulo completado]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | Booleano | Si el capítulo se ha completado o no. |
| [[!UICONTROL Id. de capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | cadena | El ID del capítulo generado automáticamente. |
| [[!UICONTROL Duración O Longitud Del Capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | entero | La duración del capítulo en segundos. |
| [[!UICONTROL Nombre de capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | cadena | El nombre del capítulo y/o segmento. |
| [[!UICONTROL Desplazamiento de capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | entero | El desplazamiento del capítulo dentro del contenido (en segundos) desde el inicio. |
| [[!UICONTROL Posición del capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | entero | La posición (índice, entero) del capítulo dentro del contenido. |
| [[!UICONTROL Capítulo Iniciado]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | Booleano | Si el capítulo ha comenzado o no. |
| [[!UICONTROL Tiempo de reproducción del capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | entero | El tiempo empleado en el capítulo, en segundos. |
