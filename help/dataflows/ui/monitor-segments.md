---
keywords: Experience Platform;inicio;temas populares;monitorizar segmentos;monitorizar flujos de datos;flujos de datos;segmentación
description: La segmentación le permite crear segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos durante la segmentación mediante la interfaz de usuario del Experience Platform.
title: Monitorizar flujos de datos para segmentos en la interfaz de usuario
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1923'
ht-degree: 2%

---

# Monitorización de flujos de datos para segmentos en la interfaz de usuario

El servicio de segmentación le permite crear segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real en Adobe Experience Platform. Platform proporciona flujos de datos para rastrear de forma transparente este flujo de datos de fuentes a destinos.

El panel de monitorización proporciona una representación visual de la actividad de los datos dentro de un segmento, incluido el estado de la segmentación de los datos. Este tutorial proporciona instrucciones sobre cómo utilizar el panel de monitorización para monitorizar la segmentación de los datos mediante la interfaz de usuario del Experience Platform, lo que le permite realizar un seguimiento del estado de los trabajos de activación, evaluación y exportación de segmentos.

## Primeros pasos {#getting-started}

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [Flujos de datos](../home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile]y [!DNL Destinations].
   - [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes basados en la configuración de frecuencia de los flujos de datos seleccionados.
- [Segmentación](../../segmentation/home.md): La segmentación le permite crear segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real.
   - [Trabajos de activación](../../destinations/ui/activation-overview.md): Se utiliza un trabajo de activación para activar el segmento en un destino especificado.
   - [Trabajos de evaluación](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Un trabajo de evaluación es un proceso asincrónico que se ejecuta y crea un segmento de audiencia basado en el segmento especificado.
   - [Exportar trabajos](../../segmentation/api/export-jobs.md): Un trabajo de exportación es un proceso asíncrono que se utiliza para mantener a los miembros del segmento de audiencia en los conjuntos de datos.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Monitorización del tablero de segmentos {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Segmentos"
>abstract="La vista de segmentos contiene información sobre todos los segmentos de la organización de IMS, con más información sobre sus trabajos de activación y evaluación."

Para acceder a la **[!UICONTROL Segmentos]** tablero, seleccione **[!UICONTROL Monitorización]** en el panel de navegación izquierdo. Una vez en el **[!UICONTROL Monitorización]** seleccione **[!UICONTROL Segmentos]** tarjeta.

![La tarjeta Segmentos . Se muestra información sobre el último trabajo de evaluación y el último trabajo de exportación.](../assets/ui/monitor-segments/segment-card-monitoring.png)

En el **[!UICONTROL Segmentos]** tablero, **[!UICONTROL Segmentos]** La tarjeta muestra el estado y la fecha del último trabajo de evaluación y del último trabajo de exportación.

El tablero mismo contiene métricas tanto para segmentos como para trabajos de segmentos. De forma predeterminada, el tablero mostrará las métricas de segmentos de las últimas 24 horas. Para obtener más información sobre la vista de trabajos de segmentos, lea la [monitorización de trabajos de segmentos](#monitoring-segment-jobs-dashboard) para obtener más información.

>[!IMPORTANT]
>
>Actualmente, solo los segmentos activados en [destinos por lotes (basados en archivos)](../../destinations/destination-types.md#file-based) son compatibles con el panel de segmentos de monitorización.

![El tablero de segmentos. Se muestra información sobre los distintos segmentos de la organización de IMS y el simulador de pruebas.](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

Las siguientes métricas están disponibles para esta vista de tablero:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Nombre del segmento]** | Nombre del segmento. |
| **[!UICONTROL Última marca de tiempo de evaluación]** | La fecha y hora de ejecución del último trabajo de evaluación del segmento. |
| **[!UICONTROL Último estado de evaluación]** | Estado del último trabajo de evaluación del segmento. Los valores posibles incluyen **[!UICONTROL Correcto]**, **[!UICONTROL Sin ejecuciones]** y **[!UICONTROL Error]**. |
| **[!UICONTROL Últimos perfiles de evaluación]** | Número de perfiles que se evaluaron en el último trabajo de evaluación del segmento. |
| **[!UICONTROL Última marca de tiempo de activación]** | La fecha y hora en que se ejecutó el último trabajo de activación del segmento. |
| **[!UICONTROL Último estado de activación]** | Estado del último trabajo de activación del segmento. Los valores posibles incluyen **[!UICONTROL Correcto]**, **[!UICONTROL Sin ejecuciones]** y **[!UICONTROL Error]**. |
| **[!UICONTROL Identidades de la última activación]** | Número de identidades activadas en el último trabajo de activación del segmento. |
| **[!UICONTROL Último destino de activación]** | Nombre del destino al que se activó el último trabajo de activación del segmento. |

Puede filtrar los resultados a un segmento específico y ver sus trabajos de segmento seleccionando el icono de filtro (![El icono de filtro.](../assets/ui/monitor-segments/filter-icon.png)). Los trabajos de los segmentos se ordenan en orden cronológico, y los trabajos de los segmentos más recientes aparecen primero.

![El icono de filtro se resalta. Si selecciona esta opción, podrá ver los trabajos del segmento correspondientes al segmento especificado.](../assets/ui/monitor-segments/filter-segment.png)

Aparecerá el tablero de segmentos filtrado. La variable **[!UICONTROL Segmentos]** La tarjeta muestra el estado y la fecha del último trabajo de evaluación y del último trabajo de activación.

![La tarjeta Segmentos . Se muestra información sobre el último trabajo de evaluación y el último trabajo de activación.](../assets/ui/monitor-segments/specified-segment-card.png)

El propio panel muestra la hora y el estado de los últimos trabajos de evaluación y activación, un gráfico que muestra el recuento de perfiles de la evaluación de segmentos y las métricas de los trabajos de segmentos que se ejecutaron. De forma predeterminada, el tablero muestra las métricas de trabajo del segmento correspondientes a las últimas 24 horas.

![El tablero de segmentos filtrado. Se muestra información sobre los distintos trabajos de segmentos que se han ejecutado para este segmento.](../assets/ui/monitor-segments/filter-specified-segment.png)

Las siguientes métricas están disponibles para esta vista de tablero:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Inicio del trabajo]** | La fecha y hora en que se inició el trabajo del segmento. |
| **[!UICONTROL Tipo]** | Indica el tipo del trabajo del segmento. Los dos tipos de trabajo admitidos son **activación** y **evaluación** trabajos. |
| **[!UICONTROL Finalización del trabajo]** | La fecha y hora en que se completó el trabajo del segmento. |
| **[!UICONTROL Tiempo de procesamiento]** | Cantidad de tiempo que tardó el trabajo del segmento en completarse. |
| **[!UICONTROL Estado del trabajo]** | Estado del trabajo del segmento. Los valores admitidos son **[!UICONTROL Correcto]**, **[!UICONTROL En curso]** y **[!UICONTROL Error]**. |
| **[!UICONTROL Recuento de perfiles]** | Número de perfiles que está evaluando el trabajo del segmento. Cada usuario debe tener un perfil único. |
| **[!UICONTROL Recuento de identidad]** | Número de identidades que se están activando en el trabajo del segmento. Cada perfil puede tener varias identidades. Por ejemplo, un perfil puede tener un correo electrónico, un número de teléfono y un número de fidelidad como identidades. |
| **[!UICONTROL Nombre de destino]** | Nombre del destino al que se está activando el trabajo del segmento. |

Puede filtrar aún más a un trabajo de segmento específico y ver sus detalles seleccionando el icono de filtro (![El icono de filtro.](../assets/ui/monitor-segments/filter-icon.png)). Existen dos tipos diferentes de trabajos de segmentos que se pueden filtrar: trabajos de activación y trabajos de evaluación.

### Detalles del trabajo de activación {#activation-job-details}

La página de detalles de ejecución del flujo de datos del trabajo de activación muestra información sobre las métricas de ejecución, los errores de ejecución del flujo de datos y los segmentos relacionados con el trabajo del segmento. Se utiliza un trabajo de activación para activar el segmento para un destino especificado. De forma predeterminada, la página de detalles muestra los errores de ejecución del flujo de datos.

![El tablero de segmentos filtrado. Se muestra información sobre los distintos trabajos de segmentos que se han ejecutado para este segmento.](../assets/ui/monitor-segments/activation-job-details.png)

Las siguientes métricas están disponibles para esta vista de tablero:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Perfiles recibidos]** | Número total de perfiles recibidos en el flujo de activación. |
| **[!UICONTROL Identidades activadas]** | Número total de identidades que se activaron correctamente en el destino, según los perfiles recibidos. |
| **[!UICONTROL Identidades excluidas]** | Número total de identidades que se excluyeron de la activación en el destino, según los perfiles recibidos. Estas identidades podrían excluirse debido a la falta de atributos o violaciones del consentimiento. |
| **[!UICONTROL Tamaño de los datos]** | El tamaño del flujo de datos que se está activando. |
| **[!UICONTROL Archivos totales]** | Número total de archivos que se activan en el flujo de datos. |
| **[!UICONTROL Estado]** | Estado actual del trabajo de activación. |
| **[!UICONTROL Inicio de la ejecución del flujo de datos]** | La fecha y hora en que se inició el trabajo de activación. |
| **[!UICONTROL Fin de la ejecución del flujo de datos]** | La fecha y hora en que finalizó el trabajo de activación. |
| **[!UICONTROL ID de ejecución de flujo de datos]** | El ID del trabajo de activación actual. |
| **[!UICONTROL ID de organización de IMS]** | ID de la organización IMS a la que pertenece el trabajo de activación. |
| **[!UICONTROL Nombre de destino]** | Nombre del destino al que se activan los datos. |

Debajo de las métricas, se muestra un interruptor para seleccionar entre los errores de ejecución del flujo de datos y los segmentos.

![El tablero de segmentos filtrado. Se resalta el interruptor utilizado para cambiar entre los errores de ejecución del flujo de datos y la visualización de segmentos.](../assets/ui/monitor-segments/activation-job-details-toggle.png)

En la sección errores de ejecución del flujo de datos , seleccione la opción para ver las identidades fallidas o los campos excluidos. La sección de errores incluye detalles sobre el código de error y el número de identidades fallidas o excluidas.

![El tablero de segmentos filtrado. Se resalta la información sobre las identidades que fallaron o se excluyeron.](../assets/ui/monitor-segments/activation-job-details.png)

En la sección de segmentos, puede ver una lista de segmentos que se activaron como parte del trabajo de activación. Utilice la barra de búsqueda para filtrar la lista de segmentos por nombre.

![El tablero de segmentos filtrado. Se resalta la información sobre las identidades que fallaron o se excluyeron.](../assets/ui/monitor-segments/activation-job-details-segments.png)

Para la sección de segmentos, están disponibles las siguientes métricas:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Nombre]** | Nombre del segmento que se activó. |
| **[!UICONTROL Identidades activadas]** | Número total de identidades que se activaron correctamente en el destino, según los perfiles recibidos. |
| **[!UICONTROL Identidades excluidas]** | Número total de identidades que se excluyeron de la activación en el destino, según los perfiles recibidos. Estas identidades podrían excluirse debido a la falta de atributos o a la violación del consentimiento. |
| **[!UICONTROL Último estado de ejecución de flujo de datos]** | El estado del último trabajo de activación que se ejecutó para ese segmento. |
| **[!UICONTROL Última fecha de ejecución del flujo de datos]** | La fecha y hora del último trabajo de activación que se ejecutó para ese segmento. |

### Detalles del trabajo de evaluación {#evaluation-job-details}

La página de detalles de ejecución del flujo de datos del trabajo de evaluación muestra información sobre las métricas y segmentos de ejecución relacionados con el trabajo del segmento. Un trabajo de evaluación es un proceso asincrónico que crea un segmento de audiencia basado en el segmento especificado. Para obtener más información sobre los trabajos de evaluación, lea el tutorial en [evaluación de un segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment).

![El panel de tareas de evaluación. Se muestra información sobre el trabajo de evaluación de segmentos.](../assets/ui/monitor-segments/evaluation-job-details.png)

Las siguientes métricas están disponibles para esta vista de tablero:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Perfiles totales]** | Número total de perfiles que se están evaluando. |
| **[!UICONTROL Estado]** | Estado del trabajo de evaluación. Los estados posibles del trabajo de evaluación incluyen **[!UICONTROL Correcto]** y **[!UICONTROL Error]**. |
| **[!UICONTROL Inicio del trabajo]** | La fecha y hora en que se inició el trabajo de evaluación. |
| **[!UICONTROL Fin del trabajo]** | La fecha y hora en que finalizó el trabajo de evaluación. |
| **[!UICONTROL Tipo de trabajo]** | Tipo de trabajo del segmento. En este caso, siempre será un trabajo de evaluación de segmentos. |
| **[!UICONTROL Tipo de evaluación]** | Tipo de evaluación que se está realizando. Esto puede ser **[!UICONTROL Lote]** o **[!UICONTROL Transmisión]**. |
| **[!UICONTROL ID de trabajo]** | El ID del trabajo de evaluación. |
| **[!UICONTROL ID de organización de IMS]** | ID de la organización IMS a la que pertenece el trabajo de evaluación. |
| **[!UICONTROL Nombre del segmento]** | Nombre del segmento que se está evaluando. |
| **[!UICONTROL ID de segmento]** | ID del segmento que se está evaluando. |

En la sección de segmentos, puede ver una lista de segmentos que se están evaluando como parte del trabajo de evaluación. Puede filtrar la lista de segmentos por su nombre utilizando la barra de búsqueda.

>[!IMPORTANT]
>
>Actualmente, esta vista de panel admite hasta 800 métricas de segmento.

Para la sección de segmentos, están disponibles las siguientes métricas:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Nombre]** | Nombre del segmento que se está evaluando. |
| **[!UICONTROL Recuento de perfiles]** | Número de perfiles que se están evaluando. |

## Monitorización del panel de trabajos de segmentos {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Trabajos de segmentos"
>abstract="La vista de trabajos del segmento contiene información sobre los trabajos de evaluación y exportación de todos los segmentos."

Para acceder a la **[!UICONTROL Trabajos de segmentos]** tablero, seleccione **[!UICONTROL Monitorización]** (![icono de monitorización](../assets/ui/monitor-destinations/monitoring-icon.png)) en el panel de navegación izquierdo. Una vez en el [!UICONTROL Monitorización] página, seleccione **[!UICONTROL Trabajos de segmentos]**. La variable [!UICONTROL Monitorización] tablero contiene métricas e información sobre los trabajos de evaluación y exportación de segmentos.

>[!NOTE]
>
>Solo **trabajos de evaluación de segmentos** son compatibles con la monitorización por segmento. Los trabajos de exportación de segmentos solo admiten la supervisión a nivel de organización.

![Panel de monitorización de trabajos de segmentos](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

Utilice la variable [!UICONTROL Trabajos de segmentos] tablero para comprender si la evaluación y exportación de perfiles se produce a tiempo y sin excepciones, de modo que los servicios descendentes para la activación de destinos puedan tener los datos de perfil evaluados más recientes.

Las siguientes métricas están disponibles para trabajos de segmentos:

| Métrica | Descripción |
---------|----------|
| **[!UICONTROL Trabajo de segmentos]** | Indica el nombre del trabajo del segmento. |
| **[!UICONTROL Tipo]** | Indica el tipo de trabajo del segmento: exportación o evaluación. Tenga en cuenta que en ambos casos, el trabajo del segmento se evalúa o exporta **all** segmentos que pertenecen a una organización. Para obtener más información sobre los trabajos de exportación, consulte la guía de [exportar extremo de trabajos](../../segmentation/api/export-jobs.md). Para obtener más información sobre los trabajos de evaluación, lea el tutorial en [evaluación de un segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Inicio del trabajo]** | La fecha y hora en que se inició el trabajo del segmento. |
| **[!UICONTROL Fin del trabajo]** | La fecha y hora en que se completó el trabajo del segmento. |
| **[!UICONTROL Estado]** | El estado del trabajo completado. Los estados posibles del trabajo del segmento incluyen éxito o error. |
