---
description: Descubra cómo puede monitorizar los flujos de datos durante la segmentación mediante la interfaz de usuario del Experience Platform.
title: Monitorización de flujos de datos para audiencias en la IU
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: 716c14f29be24d084111864053e3e4ae884003f0
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 4%

---

# Monitorización de flujos de datos para audiencias en la IU

El servicio de segmentación le permite crear audiencias mediante definiciones de segmentos u otras fuentes a partir de los datos de [!DNL Real-Time Customer Profile]. Platform proporciona flujos de datos para rastrear de forma transparente este flujo de datos de fuentes a destinos.

Utilice el panel de monitorización para ver una representación visual de la actividad de los datos dentro de una audiencia, incluido el estado de la segmentación de los datos. Lea el tutorial para obtener instrucciones sobre cómo puede utilizar el panel de monitorización para monitorizar la segmentación de los datos mediante la interfaz de usuario del Experience Platform, lo que le permite rastrear el estado de los trabajos de activación, evaluación y exportación de audiencias.

## Introducción {#getting-started}

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Flujos de datos](../home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   - [Ejecuciones de flujo de datos](../../sources/notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes en función de la configuración de frecuencia de los flujos de datos seleccionados.
- [Segmentación](../../segmentation/home.md): la segmentación le permite crear audiencias a partir de los datos del perfil del cliente en tiempo real.
   - [Trabajos de activación](../../destinations/ui/activation-overview.md): se usa un trabajo de activación para activar la audiencia en un destino especificado.
   - [Trabajos de evaluación](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Un trabajo de evaluación es un proceso asincrónico que evalúa la audiencia.
   - [Trabajos de exportación](../../segmentation/api/export-jobs.md): un trabajo de exportación es un proceso asincrónico que se usa para mantener miembros de audiencia en conjuntos de datos.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Panel de monitorización de públicos {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Públicos"
>abstract="La vista de públicos contiene información sobre todos los públicos de su organización, con más detalles acerca de sus trabajos de activación y evaluación."

Para acceder al panel **[!UICONTROL Audiencias]**, seleccione **[!UICONTROL Supervisión]** en el panel de navegación izquierdo. Una vez en la página **[!UICONTROL Supervisión]**, seleccione la tarjeta **[!UICONTROL Audiencias]**.

![La tarjeta Audiencias. Se muestra información sobre el último trabajo de evaluación y el último trabajo de exportación.](../assets/ui/monitor-audiences/audience-card.png)

En el panel principal **[!UICONTROL Audiencias]**, la tarjeta **[!UICONTROL Audiencias]** muestra el estado y la fecha del último trabajo de evaluación y del último trabajo de exportación.

El propio panel contiene métricas tanto para audiencias como para trabajos de segmentación. De forma predeterminada, el tablero muestra las métricas de audiencia de las últimas 24 horas. Para obtener más información acerca de la vista de trabajos de segmentación, lea la sección [supervisión de trabajos de segmentación](#monitoring-segmentation-jobs-dashboard).

>[!IMPORTANT]
>
>Actualmente, solo se admiten las audiencias activadas en [destinos por lotes (basados en archivos)](../../destinations/destination-types.md#file-based) para el panel de monitorización de audiencias.

![Panel de audiencias. Se muestra información sobre las distintas audiencias de su organización y de la zona protegida.](../assets/ui/monitor-audiences/audience-dashboard.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Nombre de audiencia]** | Nombre de la audiencia. |
| **[!UICONTROL Tipo de datos]** | El tipo de datos de la audiencia. Los valores posibles incluyen **[!UICONTROL Customer]**, **[!UICONTROL Account]** y **[!UICONTROL Prospect]**. Puede ver para audiencias de un tipo de datos especificado usando el filtro [!UICONTROL Tipo de datos] sobre la banda de tarjetas. |
| **[!UICONTROL Última marca de tiempo de evaluación]** | La fecha y la hora en que se ejecutó el último trabajo de evaluación de la audiencia. |
| **[!UICONTROL Último estado de evaluación]** | El estado del último trabajo de evaluación de la audiencia. Los valores posibles incluyen **[!UICONTROL Éxito]**, **[!UICONTROL Sin ejecuciones]** y **[!UICONTROL Error]**. |
| **[!UICONTROL Último método de evaluación]** | El método de evaluación de la audiencia. Dado que solo se admite la segmentación por lotes, el único valor posible es **[!UICONTROL Batch]**. |
| **[!UICONTROL Últimos perfiles de evaluación]** | El número de perfiles que se evaluaron en el último trabajo de evaluación de la audiencia. |
| **[!UICONTROL Marca de tiempo de la última activación]** | La fecha y la hora en que se ejecutó el último trabajo de activación de la audiencia. |
| **[!UICONTROL Último estado de activación]** | El estado del último trabajo de activación de la audiencia. Los valores posibles incluyen **[!UICONTROL Éxito]**, **[!UICONTROL Sin ejecuciones]** y **[!UICONTROL Error]**. |
| **[!UICONTROL Identidades de la última activación]** | El número de identidades que se activaron en el último trabajo de activación de la audiencia. |
| **[!UICONTROL Destino de la última activación]** | El nombre del destino al que se activó el último trabajo de activación de la audiencia. |

Puede filtrar los resultados a una audiencia específica y ver sus trabajos de segmentación seleccionando el icono de filtro (![El icono de filtro.](../assets/ui/monitor-audiences/filter-icon.png)). Los trabajos de segmentación se ordenan en orden cronológico y aparecen primero los trabajos de segmentación más recientes.

![El icono de filtro está resaltado. Si selecciona esta opción, podrá ver los trabajos de segmentación de la audiencia especificada.](../assets/ui/monitor-audiences/filter-audience.png)

Aparecerá el tablero de audiencias filtradas. La tarjeta **[!UICONTROL Audiencias]** muestra el estado y la fecha del último trabajo de evaluación y del último trabajo de activación.

![La tarjeta Audiencias. Se muestra información sobre el último trabajo de evaluación y el último trabajo de activación.](../assets/ui/monitor-audiences/specified-audience-card.png)

El propio panel muestra la hora y el estado de los últimos trabajos de evaluación y activación, un gráfico que muestra el recuento de perfiles de la evaluación de audiencia y las métricas de los trabajos de segmentación que se ejecutaron. De forma predeterminada, el panel muestra las métricas de trabajo de segmentación de las últimas 24 horas.

![Panel de audiencia filtrado. Se muestra información sobre los diversos trabajos de segmentación que se han ejecutado para esta audiencia.](../assets/ui/monitor-audiences/filter-audience.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Inicio del trabajo]** | La fecha y la hora en que se inició el trabajo de segmentación. |
| **[!UICONTROL Tipo]** | Indica el tipo de trabajo de segmentación. Los dos tipos de trabajos admitidos son **activation** y **evaluation**. |
| **[!UICONTROL Trabajo completado]** | La fecha y la hora en que se completó el trabajo de segmentación. |
| **[!UICONTROL Tiempo de procesamiento]** | Cantidad de tiempo que tardó el trabajo de segmentación en completarse. |
| **[!UICONTROL Estado del trabajo]** | El estado del trabajo de segmentación. Los valores admitidos son **[!UICONTROL Success]**, **[!UICONTROL In Progress]** y **[!UICONTROL Failed]**. |
| **[!UICONTROL Recuento de perfiles]** | El número de perfiles que está evaluando el trabajo de segmentación. Cada usuario debe tener un perfil único. |
| **[!UICONTROL Identidad activada]** | El número de identidades que está activando el trabajo de segmentación. Cada perfil puede tener varias identidades. Por ejemplo, un perfil puede tener un correo electrónico, un número de teléfono y un número de fidelidad como identidades. |
| **[!UICONTROL Nombre de destino]** | El nombre del destino al que se está activando el trabajo de segmentación. |

Puede filtrar a un trabajo de segmentación específico y ver sus detalles seleccionando el icono de filtro (![El icono de filtro.](../assets/ui/monitor-audiences/filter-icon.png)). Existen dos tipos diferentes de trabajos de segmentación que se pueden filtrar: trabajos de activación y trabajos de evaluación.

### Detalles del trabajo de activación {#activation-job-details}

La página de detalles de ejecución del flujo de datos del trabajo de activación muestra información sobre las métricas de la ejecución, los errores de ejecución del flujo de datos y las audiencias relacionadas con el trabajo de segmentación. Se utiliza un trabajo de activación para activar la audiencia en un destino especificado.

![Panel de tareas de activación. Se muestra información sobre los diversos trabajos de segmentación que se han ejecutado para esta audiencia.](../assets/ui/monitor-audiences/activation-job-dashboard.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Perfiles recibidos]** | Número total de perfiles recibidos en el flujo de activación. |
| **[!UICONTROL Identidades activadas]** | Número total de identidades que se activaron correctamente en el destino, según los perfiles recibidos. |
| **[!UICONTROL Identidades excluidas]** | Número total de identidades que se excluyeron de la activación en el destino, según los perfiles recibidos. Estas identidades podrían excluirse debido a la falta de atributos o violaciones del consentimiento. |
| **[!UICONTROL Tamaño de los datos]** | El tamaño del flujo de datos que se está activando. |
| **[!UICONTROL Total de archivos]** | Número total de archivos que se activan en el flujo de datos. |
| **[!UICONTROL Estado]** | El estado actual del trabajo de activación. |
| **[!UICONTROL Inicio de ejecución de flujo de datos]** | La fecha y la hora en que se inició el trabajo de activación. |
| **[!UICONTROL Fin de ejecución de flujo de datos]** | La fecha y la hora en que finalizó el trabajo de activación. |
| **[!UICONTROL ID de ejecución de flujo de datos]** | El ID del trabajo de activación actual. |
| **[!UICONTROL ID de organización de IMS]** | El ID de la organización a la que pertenece el trabajo de activación. |
| **[!UICONTROL Nombre de destino]** | El nombre del destino al que se activan los datos. |

En la sección audiencias puede ver una lista de audiencias que se activaron como parte del trabajo de activación.

![Panel de tareas de activación. Se resaltará la información sobre las identidades que fallaron o que se excluyeron.](../assets/ui/monitor-audiences/activation-job-audiences.png)

Para la sección de audiencias, están disponibles las siguientes métricas:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Nombre]** | Nombre de la audiencia que se activó. |
| **[!UICONTROL Identidades activadas]** | Número total de identidades que se activaron correctamente en el destino, según los perfiles recibidos. |
| **[!UICONTROL Identidades excluidas]** | Número total de identidades que se excluyeron de la activación en el destino, según los perfiles recibidos. Estas identidades podrían excluirse debido a la falta de atributos o a una infracción de consentimiento. |
| **[!UICONTROL Último estado de ejecución del flujo de datos]** | El estado del último trabajo de activación que se ejecutó para esa audiencia. |
| **[!UICONTROL Última fecha de ejecución del flujo de datos]** | La fecha y la hora del último trabajo de activación que se ejecutó para esa audiencia. |

Además, puede ver detalles sobre los errores de ejecución del flujo de datos. En la sección de errores de ejecución del flujo de datos, puede ver las identidades que fallaron o las identidades excluidas. La sección de errores incluye detalles sobre el código de error y el número de identidades fallidas o excluidas.

![Panel de tareas de activación. Se resaltará la información sobre las identidades que fallaron o que se excluyeron.](../assets/ui/monitor-audiences/activation-job-errors.png)

### Detalles del trabajo de evaluación {#evaluation-job-details}

La página de detalles de ejecución del flujo de datos del trabajo de evaluación muestra información sobre las métricas de la ejecución y las audiencias relacionadas con el trabajo de segmentación.

![El tablero del trabajo de evaluación. Se muestra información sobre el trabajo de evaluación de la audiencia.](../assets/ui/monitor-audiences/evaluation-job-details.png)

Las siguientes métricas están disponibles para esta vista de panel:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Perfiles totales]** | Número total de perfiles que se están evaluando. |
| **[!UICONTROL Estado]** | El estado del trabajo de evaluación. Los estados posibles para el trabajo de evaluación incluyen **[!UICONTROL Éxito]** y **[!UICONTROL Error]**. |
| **[!UICONTROL Inicio del trabajo]** | La fecha y la hora en que se inició el trabajo de evaluación. |
| **[!UICONTROL Fin del trabajo]** | La fecha y la hora en que finalizó el trabajo de evaluación. |
| **[!UICONTROL Tipo de trabajo]** | El tipo de trabajo de segmentación. En este caso, siempre será un trabajo de **[!UICONTROL evaluación de segmentos]**. |
| **[!UICONTROL Tipo de evaluación]** | El tipo de evaluación que se está realizando. Puede ser **[!UICONTROL Batch]** o **[!UICONTROL Streaming]**. |
| **[!UICONTROL Id. de trabajo]** | El ID del trabajo de evaluación. |
| **[!UICONTROL ID de organización de IMS]** | El ID de la organización a la que pertenece el trabajo de evaluación. |
| **[!UICONTROL Nombre de audiencia]** | Nombre de la audiencia que se está evaluando. |
| **[!UICONTROL ID de audiencia]** | El ID de la audiencia que se está evaluando. |

En la sección [!UICONTROL Audiencias], puede ver una lista de audiencias que se están evaluando como parte del trabajo de evaluación. Puede filtrar la lista de audiencias por nombre mediante la barra de búsqueda.

>[!IMPORTANT]
>
>Actualmente, esta vista de panel admite hasta 800 métricas de audiencia.

Para la sección [!UICONTROL Audiencias], están disponibles las siguientes métricas:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Nombre]** | Nombre de la audiencia que se está evaluando. |
| **[!UICONTROL Recuento de perfiles]** | El número de perfiles que se están evaluando. |

## Panel de monitorización de trabajos de segmentación {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Trabajos de segmentación"
>abstract="La vista de trabajos de segmentación contiene información sobre los trabajos de evaluación y exportación de todos los públicos."

Para acceder al panel **[!UICONTROL Trabajos de segmentación]**, seleccione **[!UICONTROL Trabajos de segmentación]** en el panel [!UICONTROL Audiencias]. El panel [!UICONTROL Supervisión] contiene métricas e información sobre los trabajos de evaluación y exportación.

>[!NOTE]
>
>Solo se admiten **trabajos de evaluación de segmentación** para la monitorización por audiencia. Los trabajos de exportación de segmentación solo admiten la monitorización en el nivel de organización.

![Se muestra el panel de monitorización de trabajos de segmentación. Se resaltó el conmutador para cambiar entre Audiencias y Trabajos de segmentación.](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

Utilice el panel [!UICONTROL Trabajos de segmentación] para saber si la evaluación y exportación de perfiles se realiza a tiempo y sin excepciones, de modo que los servicios descendentes para la activación de destino puedan tener los datos de perfil evaluados más recientes.

Las siguientes métricas están disponibles para los trabajos de segmentación:

| Métrica | Descripción |
| ------ | ----------- |
| **[!UICONTROL Trabajo de segmentación]** | Indica el nombre del trabajo de segmentación. |
| **[!UICONTROL Tipo]** | Indica el tipo de trabajo de segmentación: exportación o evaluación. Tenga en cuenta que en ambos casos, el trabajo de segmentación evalúa o exporta **todas** las audiencias que pertenecen a una organización. Para obtener más información acerca de los trabajos de exportación, lea la guía del [extremo de trabajos de exportación](../../segmentation/api/export-jobs.md). Para obtener más información acerca de los trabajos de evaluación, lea el tutorial sobre [evaluación de una definición de segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Inicio del trabajo]** | La fecha y la hora en que se inició el trabajo de segmentación. |
| **[!UICONTROL Fin del trabajo]** | La fecha y la hora en que se completó el trabajo de segmentación. |
| **[!UICONTROL Estado]** | El estado del trabajo completado. Los estados posibles para el trabajo de segmentación incluyen éxito o error. |
