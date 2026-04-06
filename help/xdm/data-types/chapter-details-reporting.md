---
title: Detalles del capítulo Tipo de datos de informes
description: Obtenga información sobre los detalles del capítulo Creación de informes sobre el tipo de datos del Modelo de datos de experiencia (XDM).
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# [!UICONTROL Chapter Details] tipo de datos de informe

La creación de informes [!UICONTROL Chapter Details] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe varios atributos relacionados con capítulos o segmentos dentro del contenido multimedia. Utilice el tipo de datos de creación de informes [!UICONTROL Chapter Details] para capturar detalles como el nombre del capítulo, la duración, la posición, el ID, el estado de reproducción (iniciada/finalizada) y el tiempo empleado en cada capítulo. Los servicios de Adobe utilizan los campos de creación de informes de contenidos para analizar los campos de recopilación de contenidos que envían los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican.

![Un diagrama del tipo de datos del informe de detalles del capítulo.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Cada nombre para mostrar contiene un vínculo a información adicional sobre sus parámetros de audio y vídeo. Las páginas vinculadas contienen detalles sobre el vídeo y los datos recopilados por Adobe, los valores de implementación, los parámetros de red, los informes y otros aspectos importantes.

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Chapter Completed]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | Booleano | Si el capítulo se ha completado o no. |
| [[!UICONTROL Chapter ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | cadena | El ID del capítulo generado automáticamente. |
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | entero | La duración del capítulo en segundos. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | cadena | El nombre del capítulo y/o segmento. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | entero | El desplazamiento del capítulo dentro del contenido (en segundos) desde el inicio. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | entero | La posición (índice, entero) del capítulo dentro del contenido. |
| [[!UICONTROL Chapter Started]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | Booleano | Si el capítulo ha comenzado o no. |
| [[!UICONTROL Chapter Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | entero | El tiempo empleado en el capítulo, en segundos. |
