---
description: Obtenga información sobre cómo ver información detallada sobre conjuntos de datos y ejecuciones de trabajos individuales en Programaciones de trabajos.
solution: Experience Platform
title: Ver detalles de programación del trabajo
type: Tutorial
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 1%

---


# Ver detalles de programación del trabajo

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] están disponibles actualmente como una versión limitada y solo para los siguientes trabajos de Real-Time CDP:
>
> * Ingesta de lago de datos por lotes
> * Ingesta de perfil por lotes
> * Segmentación por lotes
> * Activación de destino del lote.

Al solucionar errores de trabajos o investigar problemas de rendimiento, necesita información detallada sobre conjuntos de datos específicos y sus ejecuciones de trabajos. La interfaz [Programaciones de trabajos](job-schedules.md) le permite explorar en profundidad desde la vista de cronología los conjuntos de datos y trabajos individuales para comprender el historial de ejecución, el tiempo y el estado.

Utilice esta vista detallada para:

* Investigue por qué un trabajo específico falló o tardó más de lo esperado
* Revisión del historial de ejecución de un conjunto de datos a lo largo del tiempo
* Comprenda los patrones de tiempo y duración de los trabajos por lotes
* Identificar qué lotes específicos están causando problemas de canalización
* Recopile la información necesaria para solucionar problemas con la asistencia de Adobe

## Requisitos previos {#prerequisites}

Antes de ver los detalles del trabajo, debe:

* Tener acceso a [!UICONTROL Job Schedules] con los **[!UICONTROL View Job Schedules]** y **[!UICONTROL View Profile Management]** [permisos de control de acceso](/help/access-control/home.md#permissions).
* Familiarícese con la [interfaz de horarios de trabajo](job-schedules.md#understanding-interface) y la vista de escala de tiempo.
* Comprenda los diferentes [tipos de trabajos](job-schedules.md#job-schedules-details) (ingesta de lago, ingesta de perfiles, segmentación, activación).

## Explicación de la jerarquía de detalles {#details-hierarchy}

Los horarios de trabajo proporcionan tres niveles de detalle, lo que le permite pasar de patrones amplios a problemas específicos:

| Ver nivel | Lo que muestra | Cuándo utilizarla |
|------------|---------------|----------------|
| **Vista de escala de tiempo** | Todos los conjuntos de datos y sus trabajos programados durante el período de tiempo seleccionado | Identificar patrones, identificar [antipatrones](job-schedules-anti-patterns.md) y obtener una descripción general de toda la canalización |
| **Detalles del conjunto de datos** | Métricas agregadas e historial de ejecución para un único conjunto de datos | Seguimiento del rendimiento general de un conjunto de datos, comprensión de los volúmenes de datos y revisión de la frecuencia de trabajo |
| **Detalles de ejecución del trabajo** | Información de ejecución específica para una ejecución de trabajo individual | Investigar por qué falló un trabajo en particular, comprobar el tiempo exacto y verificar los registros procesados |

**Flujo de navegación**: Comience con la vista de cronología para identificar problemas → Seleccione un conjunto de datos para ver sus detalles → Seleccione una ejecución de trabajo específica para investigar los detalles.

### Explicación de la vista de cronología {#timeline-visualization}

La vista de cronología utiliza un diseño horizontal y vertical para ayudarle a comprender los horarios de los trabajos y los tiempos de procesamiento críticos:

* **Eje horizontal (progresión de tiempo)**: los conjuntos de datos y sus ejecuciones de trabajos se muestran en la escala de tiempo de izquierda a derecha, mostrando cuándo se ejecutan los trabajos durante el período de tiempo seleccionado (hoy, ayer o los últimos 7 días). Cada barra de color representa una ejecución del trabajo, colocada horizontalmente según su hora de inicio y finalización.

* **Eje vertical (horas de inicio programadas)**: las horas de inicio programadas críticas se muestran como líneas verticales que se extienden a lo largo de todos los conjuntos de datos, lo que facilita ver la relación de tiempo entre los trabajos de flujo ascendente y el procesamiento descendente:
   * **Línea vertical azul**: Representa cuándo está programado que comience la segmentación
   * **Línea vertical negra**: Representa cuándo está programado que comience la activación de destino

Este diseño le permite identificar rápidamente las relaciones de tiempo entre los trabajos de la canalización de datos y el procesamiento descendente. Lo ideal es que los trabajos de subida (como el lago de datos y la ingesta de perfiles) se completen a la izquierda de estos marcadores verticales, lo que garantiza que los datos estén listos antes de que comiencen la segmentación y la activación. Los trabajos que se extienden más allá de estos marcadores indican posibles problemas de tiempo en los que los procesos descendentes pueden iniciarse antes de que los datos estén completamente preparados.

### ¿Qué vista debo usar? {#which-view}

Utilice la tabla siguiente para elegir la vista correcta para la tarea. Haga coincidir lo que necesita hacer con la vista recomendada para navegar de forma eficaz.

| Tengo que... | Usar esta vista |
|--------------|---------------|
| Ver todos mis conjuntos de datos con perfil habilitado y sus programaciones a la vez | [Vista de escala de tiempo](job-schedules.md) |
| Identificación de conflictos de programación o antipatrones | [Vista de escala de tiempo](job-schedules.md) |
| Seguimiento del rendimiento general de un conjunto de datos | [Detalles del conjunto de datos](#view-dataset-details) |
| Ver cuántos registros totales ha procesado un conjunto de datos | [Detalles del conjunto de datos](#view-dataset-details) |
| Comparar el rendimiento del trabajo con el tiempo para un conjunto de datos | [Detalles del conjunto de datos](#view-dataset-details) |
| Investigar por qué ha fallado un trabajo específico | [Detalles de ejecución del trabajo](#view-job-details) |
| Comprobar el tiempo exacto de una ejecución de trabajo en particular | [Detalles de ejecución del trabajo](#view-job-details) |
| Verificar registros procesados en una sola ejecución | [Detalles de ejecución del trabajo](#view-job-details) |
| Acceso a mensajes de error detallados | [Detalles de ejecución del trabajo](#view-job-details) → Seleccionar ID de ejecución de flujo de datos |

## Ver detalles del conjunto de datos {#view-dataset-details}

Para ver los detalles de un conjunto de datos específico:

1. En la vista de escala de tiempo **[!UICONTROL Job Schedules]**, busque el conjunto de datos que desee investigar.
2. Seleccione el nombre del conjunto de datos en la columna izquierda.

La vista de detalles del conjunto de datos se abre en un panel derecho, que muestra información sobre todos los trabajos asociados con este conjunto de datos.

![El panel de detalles del conjunto de datos muestra las métricas agregadas de ingesta de lago y perfil para un conjunto de datos seleccionado.](assets/job-schedules/view-dataset-details.png)

El panel de detalles del conjunto de datos muestra el nombre del conjunto de datos, el ID y las métricas específicas del trabajo organizadas por tipo de trabajo. En la parte superior del panel, la ID del conjunto de datos se muestra como un vínculo en el que se puede hacer clic. Seleccione este ID para navegar a la página de detalles completa del conjunto de datos.

Cada panel de detalles del conjunto de datos incluye las siguientes métricas:

### Métricas de ingesta de lago {#lake-ingestion-metrics}

Para conjuntos de datos con trabajos de ingesta de lago de datos, el panel muestra las siguientes métricas:

| Métrica | Descripción | Usar para |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Número total de trabajos de ingesta de lago de datos que se han completado para este conjunto de datos | Seguimiento de actividades |
| **[!UICONTROL Runs in progress]** | Cuántos trabajos de ingesta de lago se están ejecutando actualmente | Detección de cuello de botella |
| **[!UICONTROL Total records added]** | El número acumulado de registros nuevos agregados al lago de datos en todas las ejecuciones de trabajos | Monitorización del volumen |
| **[!UICONTROL Total ingestion time]** | La duración combinada de todos los trabajos de ingesta de lago de datos | Evaluación del tiempo de procesamiento |
| **[!UICONTROL Total records updated]** | El número acumulado de registros existentes que se actualizaron durante la ingesta | Actualizar análisis de patrones |
| **[!UICONTROL Avg. ingestion speed (records/second)]** | La tasa de rendimiento promedio para los trabajos de ingesta del lago de datos | Comparación del rendimiento |

### Métricas de ingesta de perfil {#profile-ingestion-metrics}

Para conjuntos de datos con trabajos de ingesta de perfiles, el panel muestra las siguientes métricas:

| Métrica | Descripción | Usar para |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Número total de trabajos de ingesta de perfiles que se han completado para este conjunto de datos | Seguimiento de actividades |
| **[!UICONTROL Runs in progress]** | Cuántos trabajos de ingesta de perfiles se están ejecutando actualmente | Detección de retardo |
| **[!UICONTROL Total profiles created]** | El número acumulado de perfiles nuevos creados a partir de este conjunto de datos en todas las ejecuciones de trabajos | Monitorización del crecimiento del perfil |
| **[!UICONTROL Total profile ingestion time]** | La duración combinada de todos los trabajos de ingesta de perfiles | Identificación del problema de sincronización |
| **[!UICONTROL Total profiles updated]** | El número acumulado de perfiles existentes que se actualizaron con los datos de este conjunto de datos | Actualizar seguimiento de frecuencia |
| **[!UICONTROL Avg. profile ingestion speed (profiles/second)]** | Tasa de rendimiento promedio para trabajos de ingesta de perfiles | Monitorización del rendimiento |

>[!NOTE]
>
> Estas métricas muestran totales acumulativos en todas las ejecuciones de trabajos para este conjunto de datos. Para ver los detalles de una ejecución específica, seleccione un trabajo directamente en la cronología.

## Filtrar conjuntos de datos en la cronología {#filter-datasets}

Cuando tiene muchos conjuntos de datos con trabajos programados, es posible que desee centrarse en conjuntos de datos específicos en lugar de ver todos a la vez. El filtro de conjuntos de datos le permite seleccionar qué conjuntos de datos aparecen en la vista de cronología.

![Panel de filtro de conjunto de datos que le permite seleccionar qué conjuntos de datos aparecen en la vista de escala de tiempo.](assets/job-schedules/view-datasets.gif)

Para filtrar los conjuntos de datos mostrados en la cronología:

1. Busque el contador del conjunto de datos en la parte superior izquierda de la vista de la cronología (por ejemplo, &quot;2 conjuntos de datos&quot;).
2. Seleccione el icono de filtro junto al contador del conjunto de datos.
3. Se abre el panel de selección de conjuntos de datos, que muestra todos los conjuntos de datos disponibles habilitados para perfiles con trabajos programados.
4. Seleccione o anule la selección de conjuntos de datos para mostrarlos u ocultarlos en la vista de cronología.
5. La cronología se actualiza inmediatamente para mostrar solo los conjuntos de datos seleccionados.

Use el filtrado para:

* **Céntrese en las fuentes de datos específicas**: al solucionar problemas de una canalización de datos en particular, filtre para mostrar solo los conjuntos de datos relevantes.
* **Reduzca el desorden visual**: si tiene muchos conjuntos de datos, el filtrado le ayuda a ver con mayor claridad los patrones de un subconjunto de datos.
* **Comparar conjuntos de datos relacionados**: seleccione solo conjuntos de datos relacionados para comprender su relación de programación.
* **Investigar antipatrones**: Cuando identifique un posible [problema de configuración](job-schedules-anti-patterns.md), filtre a los conjuntos de datos afectados para examinarlos más de cerca.

El filtro persiste durante la sesión, por lo que puede navegar entre períodos de tiempo (hoy, ayer, últimos 7 días) mientras mantiene la selección del conjunto de datos.

## Ver detalles de ejecución de trabajo individuales {#view-job-details}

Cuando necesite investigar una ejecución de trabajo específica, selecciónela en la cronología para ver información detallada de la ejecución de esa ejecución en particular.

### Acceder a detalles de ejecución del trabajo {#access-job-details}

Para ver los detalles de una ejecución de trabajo específica:

1. En la vista de escala de tiempo [!UICONTROL Job Schedules], busque la ejecución de trabajo específica que desee investigar.
2. Seleccione el indicador del trabajo en la cronología (la barra de color que representa el trabajo).

Se abre el panel **[!UICONTROL Dataflow run details]**, que muestra información sobre la ejecución de ese trabajo específico.

![El panel de detalles de ejecución del flujo de datos muestra información de ejecución para una ejecución de trabajo específica.](assets/job-schedules/job-details.png)

### Detalles de ejecución del flujo de datos {#dataflow-run-details}

El panel de detalles de ejecución del flujo de datos muestra información sobre la ejecución del trabajo específica, organizada por tipo de trabajo. Para los trabajos de ingesta, verá detalles para las etapas de ingesta de lago y de ingesta de perfil.

#### Detalles del trabajo de ingesta de lago {#lake-ingestion-job-details}

| Campo | Descripción |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | El identificador único de esta ejecución de trabajo de ingesta de lago específica. Seleccione el ID para ver los detalles completos de monitorización del flujo de datos. |
| **[!UICONTROL Run status]** | El resultado del trabajo (correcto, fallido, en curso, en cola). Un indicador verde muestra la finalización correcta. |
| **[!UICONTROL Started at]** | La fecha y la hora en que comenzó la ejecución del trabajo de ingesta del lago. |
| **[!UICONTROL Completed at]** | La fecha y la hora en que finalizó la ejecución del trabajo de ingesta del lago. |
| **[!UICONTROL Records added]** | Número de registros nuevos agregados al lago de datos durante la ejecución de este trabajo. |
| **[!UICONTROL Records updated]** | El número de registros existentes que se actualizaron en el lago de datos durante la ejecución de este trabajo. |

#### Detalles del trabajo de ingesta de perfil {#profile-ingestion-job-details}

| Campo | Descripción |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | El identificador único de esta ejecución de trabajo de ingesta de perfiles específica. Seleccione el ID para ver los detalles completos de monitorización del flujo de datos. |
| **[!UICONTROL Run status]** | El resultado del trabajo (correcto, fallido, en curso, en cola). Un indicador verde muestra la finalización correcta. |
| **[!UICONTROL Started at]** | La fecha y la hora en que comenzó la ejecución del trabajo de ingesta de perfiles. |
| **[!UICONTROL Completed at]** | La fecha y la hora en que finalizó la ejecución del trabajo de ingesta de perfiles. |
| **[!UICONTROL Records added]** | El número de perfiles nuevos creados durante la ejecución de este trabajo. |
| **[!UICONTROL Records updated]** | El número de perfiles existentes que se actualizaron durante la ejecución de este trabajo. |

### Explicación del flujo de ejecución del trabajo {#job-execution-flow}

Al ver una ejecución de trabajo específica, puede ver la relación entre la ingesta del lago y la ingesta de perfiles:

* **La ingesta de lago se ejecuta primero**: Los datos se cargan en el lago de datos y se validan.
* **La ingesta de perfiles sigue**: Una vez completada la ingesta de lago, los registros aptos se procesan en el almacén de perfiles.
* **El tiempo importa**: tenga en cuenta la diferencia horaria entre el momento en que se completa la ingesta del lago y el momento en que comienza la ingesta de perfiles. Las lagunas aquí pueden afectar a los procesos descendentes como la segmentación.

**Usar detalles de ejecución del trabajo para**:

* Verificar que un trabajo específico se haya completado correctamente
* Calcular la duración real de una ejecución de trabajo (tiempo completado menos tiempo de inicio)
* Comprender cuántos registros se procesaron en una ejecución específica
* Comparar el rendimiento en diferentes ejecuciones de trabajos
* Acceso a la monitorización detallada del flujo de datos para solucionar errores
* Identificar problemas de tiempo entre las etapas de ingesta de lago y perfil

## Solución de problemas con detalles del trabajo {#troubleshooting}

Utilice los detalles del trabajo para investigar problemas y determinar los pasos siguientes:

**Trabajos con errores**: seleccione el ID de ejecución del flujo de datos para ver los detalles del error en el panel de supervisión. Comprueba [detalles del conjunto de datos](#view-dataset-details) para patrones recurrentes, revisa la [cronología](job-schedules.md) para la contención de recursos e identifica [antipatrones](job-schedules-anti-patterns.md) en tu configuración.

**Trabajos lentos**: compare la duración con los promedios históricos en [métricas del conjunto de datos](#view-dataset-details). Las causas comunes incluyen [superposición de programación](job-schedules-anti-patterns.md#schedule-overlap-pattern), [apilamiento por lotes denso](job-schedules-anti-patterns.md#scheduled-density) o aumento del volumen de datos.

**Discrepancias de registros**: compare los registros de ingesta de lago con los registros de ingesta de perfil en los detalles de ejecución del trabajo. La ingesta de perfiles suele mostrar menos registros debido a los requisitos de identidad y las reglas de calidad de datos.

Para obtener información detallada del estado del flujo de datos, consulte [Monitorizar la ingesta del lago de datos](../dataflows/ui/monitor-sources.md), [Monitorizar flujos de datos para perfiles](../dataflows/ui/monitor-profiles.md), [Monitorizar flujos de datos para audiencias](../dataflows/ui/monitor-audiences.md) y [Monitorizar flujos de datos para destinos](../dataflows/ui/monitor-destinations.md).

## Próximos pasos {#next-steps}

Después de aprender a ver los detalles del trabajo:

* Revise la [descripción general de los horarios de trabajo](job-schedules.md) para comprender la vista de la cronología y la interfaz.
* Obtenga información acerca de [antipatrones](job-schedules-anti-patterns.md) para evitar problemas comunes de configuración.
* Sepa [la ingesta por lotes](../ingestion/batch-ingestion/overview.md) para optimizar los horarios de carga de datos.
* Explore [monitorización de flujos de datos de destino](../dataflows/ui/monitor-destinations.md) para ver la canalización de extremo a extremo.
