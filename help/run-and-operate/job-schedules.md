---
description: Obtenga información sobre cómo inspeccionar y solucionar problemas de trabajos de procesamiento por lotes programados mediante la herramienta Programaciones de trabajos en Adobe Experience Platform.
solution: Experience Platform
title: Inspeccionar horarios de trabajo
type: Tutorial
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---


# Inspeccionar horarios de trabajos

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] están disponibles actualmente como una versión limitada y solo para los siguientes trabajos de Real-Time CDP:
>
> * Ingesta de lago de datos por lotes
> * Ingesta de perfil por lotes
> * Segmentación por lotes
> * Activación de destino del lote.

[!UICONTROL Job Schedules] proporciona una vista unificada de todos los trabajos de procesamiento por lotes programados en toda la canalización de datos, desde la ingesta hasta la activación de destino. Inspeccione el estado de ejecución, identifique los conflictos de programación y diagnostique los problemas de configuración antes de que afecten a las operaciones empresariales.

Utilice los horarios de trabajo para investigar errores, optimizar el tiempo de los trabajos y comprender las dependencias entre la ingesta del lago de datos, el procesamiento de perfiles, la segmentación y la activación de destino. Para obtener instrucciones sobre cómo resolver problemas comunes de configuración, consulte la documentación de [identificación de patrones antihorario de trabajo](job-schedules-anti-patterns.md).

## Requisitos previos {#prerequisites}

Para tener acceso a [!UICONTROL Job Schedules], necesita los **[!UICONTROL View Job Schedules]** y **[!UICONTROL View Profile Management]** [permisos de control de acceso](/help/access-control/home.md#permissions).

Póngase en contacto con el administrador del sistema para asegurarse de que tiene los permisos adecuados.

## Introducción {#getting-started}

Antes de usar [!UICONTROL Job Schedules], debe estar familiarizado con los siguientes conceptos de Experience Platform:

* **[Ingesta por lotes](../ingestion/batch-ingestion/overview.md)**: Cómo se cargan los datos en el repositorio de datos y el almacén de perfiles en intervalos programados.
* **[Segmentación](../segmentation/home.md)**: Cómo se evalúan y actualizan las audiencias en función de los datos de perfil y las definiciones de segmento.
* **[Perfil del cliente en tiempo real](../profile/home.md)**: Cómo se unifican los datos de perfil y cómo están disponibles para la segmentación y activación.
* **[Destinos](../destinations/home.md)**: Dónde y cómo se activan los datos en los sistemas descendentes y las plataformas de marketing.

La comprensión de estos componentes le ayuda a interpretar los patrones de ejecución del trabajo y a diagnosticar problemas cuando se producen.

## Explicación de la interfaz de programación de trabajos {#understanding-interface}

Para acceder a [!UICONTROL Job Schedules]:

1. En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Run and Operate]** en el panel de navegación izquierdo.
2. Seleccione **[!UICONTROL Job Schedules]**.

La página [!UICONTROL Job Schedules] proporciona una descripción general de todos sus trabajos de procesamiento por lotes programados.

![Ejecutar y operar la navegación izquierda](assets/job-schedules/run-and-operate-left-nav.png)

### Tarjetas de resumen {#summary-cards}

En la parte superior de la página, puede ver tarjetas de resumen que proporcionan información rápida sobre los trabajos de procesamiento por lotes.

![Tarjetas de resumen de horarios de trabajo que muestran información sobre los trabajos de procesamiento por lotes](assets/job-schedules/job-schedules-cards.png)

* **Ejecuciones de ingesta de lago de datos**: El número de trabajos de ingesta de lago de datos que se han ejecutado.
* **Ejecuciones de ingesta de perfiles**: Número de trabajos de ingesta de perfiles que se han ejecutado.
* **Siguiente segmentación**: Cuando se ejecutará el siguiente trabajo de segmentación programado.
* **Siguiente activación de destino**: Cuando se ejecutará el siguiente trabajo de activación de destino programado.

Estas tarjetas le ayudan a comprender la actividad y las próximas programaciones en toda la canalización de datos. Los valores de **Ejecuciones de ingesta de lago** y **Ejecuciones de ingesta de perfil** cambian según el intervalo de tiempo seleccionado (Hoy, Ayer o Últimos 7 días); las tarjetas de próxima ejecución (**Siguiente segmentación** y **Siguiente activación de destino**) no se ven afectadas por el selector de tiempo.

### Selector de período de tiempo {#time-period}

Utilice los selectores de período de tiempo para elegir cuánto se retrocede para ver los trabajos programados.

![Ejemplo animado de la IU del selector de período de tiempo en Horarios de trabajo](assets/job-schedules/time-selector.gif)

* **Hoy**: vea los trabajos programados para hoy (vista predeterminada).
* **Ayer**: vea los trabajos que se ejecutaron ayer.
* **Últimos 7 días**: vea los trabajos de la semana pasada.

### Detalles de programaciones de trabajos por lotes {#job-schedules-details}

La vista principal muestra cuándo está programado que los trabajos por lotes se ejecuten a lo largo del día. Puede hacer lo siguiente:

* **Ver trabajos por conjunto de datos o entidad**: la columna izquierda muestra los nombres de los conjuntos de datos o los trabajos de procesamiento (por ejemplo, los conjuntos de datos de ingesta o los trabajos de segmentación).
* **Ver tiempo del trabajo**: la escala de tiempo muestra cuándo está programado que se ejecute cada trabajo, con indicadores visuales que marcan la hora programada.
* **Trabajos de filtro**: utilice el icono de filtro para reducir qué conjuntos de datos se incluirán en el informe.
* **Comprenda los tipos de trabajos**: la leyenda con códigos de color de la parte inferior le ayuda a identificar diferentes tipos de trabajos:
   * **Ingesta de lago** (verde): Ingesta de datos en el lago de datos
   * **Ingesta de perfiles** (rosa): Ingesta de datos en el almacén de perfiles
   * **Segmentación** (azul claro): trabajos de evaluación de audiencia
   * **Exportación de perfiles** (azul): exportación de datos de perfil
   * **Activation** (gris oscuro): trabajos de activación de destino
   * **En curso** (seccionado): trabajos en ejecución o en cola

Esta vista de cronología le ayuda a identificar conflictos de programación, comprender las dependencias entre trabajos y optimizar las programaciones de procesamiento por lotes.

## Identificación de problemas de configuración {#identifying-issues}

A medida que revise las programaciones de trabajos, puede observar patrones que indican problemas de configuración. Los problemas comunes incluyen:

* Trabajos programados para estar demasiado juntos, lo que provoca contención de recursos
* Demasiados lotes ejecutándose en la misma ventana de tiempo
* Conjuntos de datos individuales con trabajos por lotes diarios excesivos
* Tareas de ingesta programadas inmediatamente antes de que se ejecute la segmentación

Estos patrones pueden provocar errores en los trabajos, un procesamiento de datos incompleto y un rendimiento del sistema deficiente. Para aprender a identificar y resolver estos problemas, consulte la documentación sobre [identificación de antipatrones de programación de trabajos](job-schedules-anti-patterns.md).

Cuando necesite investigar conjuntos de datos específicos o ejecuciones de trabajos, puede explorar en profundidad las vistas detalladas para ver el historial de ejecución, los mensajes de error, las métricas de rendimiento y las dependencias. Para obtener información sobre cómo ver estos datos detallados, consulte la documentación sobre [ver detalles del trabajo](job-schedules-details.md).


## Próximos pasos {#next-steps}

Después de obtener información sobre los horarios de trabajo, es posible que desee explorar estos temas relacionados:

* [Ver detalles del trabajo](job-schedules-details.md): Aprenda a explorar en profundidad conjuntos de datos individuales y ejecuciones de trabajos para una investigación detallada.
* [Identificar antipatrones de programación de trabajo](job-schedules-anti-patterns.md): Aprenda a identificar y resolver problemas de configuración comunes que afectan el rendimiento de la canalización.
* [Ingesta por lotes](../ingestion/batch-ingestion/overview.md): Aprenda a ingerir datos en Experience Platform mediante el procesamiento por lotes.
* [Segmentación](../segmentation/home.md): Descubra cómo se evalúan y actualizan las audiencias en intervalos programados.
* [Supervisar flujos de datos para destinos](../dataflows/ui/monitor-destinations.md): Aprenda a supervisar los flujos de datos de activación de destino.
* [Programar exportaciones de audiencia](../destinations/ui/activate-batch-profile-destinations.md): Aprenda a configurar activaciones de destino de lote programadas.
