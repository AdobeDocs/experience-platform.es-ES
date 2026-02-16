---
description: Obtenga información sobre cómo identificar y resolver los antipatrones comunes de configuración de programación de trabajos en Adobe Experience Platform.
solution: Experience Platform
title: Identificar antipatrones de programación de trabajo
type: Tutorial
hide: true
source-git-commit: 9d170fec9b80f0f2e17fc39e8f573cbad515f823
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---


# Identificación de antipatrones de programación de trabajo

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] están disponibles actualmente como una versión limitada y solo para los siguientes trabajos de Real-Time CDP:
>
> * Ingesta de lago de datos por lotes
> * Ingesta de perfil por lotes
> * Segmentación por lotes
> * Activación de destino del lote.

La vista de la cronología de [Programaciones de trabajos](job-schedules.md) le ayuda a identificar problemas comunes de configuración que pueden afectar negativamente el rendimiento y la confiabilidad de su canalización de datos. Estos antipatrones suelen provocar errores en los trabajos, incoherencias en los datos o un rendimiento del sistema degradado. Si detecta estos patrones antes de tiempo, puede reconfigurar sus trabajos para evitar problemas antes de que afecten a sus operaciones comerciales.

## Requisitos previos {#prerequisites}

Antes de identificar los antipatrones, debe:

* Tener acceso a [!UICONTROL Job Schedules] con el **[!UICONTROL View Job Schedules]** [permiso de control de acceso](/help/access-control/home.md#permissions).
* Familiarícese con la [interfaz de horarios de trabajo](job-schedules.md#understanding-interface) y cómo leer la vista de cronología.
* Comprenda los conceptos básicos de [ingesta por lotes](../ingestion/batch-ingestion/overview.md), [segmentación](../segmentation/home.md) y [procesamiento de perfiles](../profile/home.md).

## Referencia rápida {#anti-pattern-quick-reference}

| Antipatrón | Lo que verá en la cronología | Impacto principal | Gravedad |
|--------------|----------------------------------|----------------|----------|
| [Superposición de programación](#schedule-overlap-pattern) | Varios trabajos ejecutándose simultáneamente | Contención de recursos y errores de trabajos | Alto |
| [Densidad de trabajo programada](#scheduled-density) | Muchos conjuntos de datos con lotes agrupados en la misma hora | Cuellos de botella de canalización y segmentación incompleta | Alto |
| [Lotes excesivos por conjunto de datos](#excessive-batches-per-dataset) | Conjunto de datos único con decenas de lotes diarios | Complejidad operativa y de procesamiento ineficiente | Medio |

## Superposición de programación {#schedule-overlap-pattern}

**Gravedad de impacto**: Alto | **Problema principal**: contención de recursos

**Qué buscar**: hay varios trabajos programados para ejecutarse al mismo tiempo o en sucesión, especialmente cuando se superponen trabajos que requieren muchos recursos.

En este ejemplo, puede ver los trabajos de ingesta por lotes que se ejecutan al mismo tiempo que un trabajo de segmentación programado. Esto crea contención de recursos porque ambas operaciones requieren una potencia de procesamiento y una memoria significativas.

**Por qué esto es problemático**:

* **Contención de recursos**: cuando se ejecutan simultáneamente varios trabajos que requieren muchos recursos, compiten por los recursos del sistema (CPU, memoria, E/S), lo que hace que todos los trabajos se ejecuten más lentamente.
* **Rendimiento impredecible**: La duración del trabajo se vuelve incoherente, lo que dificulta la planificación de programaciones confiables.
* **Retrasos en cascada**: Si los trabajos tardan más de lo esperado, pueden retrasar los trabajos dependientes posteriores, lo que crea un efecto de propagación en toda la canalización.
* **Mayor riesgo de error**: el agotamiento de los recursos puede provocar que los trabajos agoten el tiempo de espera o fallen por completo.

**Cómo solucionarlo**:

* **Escalonar programaciones de trabajos**: Asegúrese de que las operaciones de uso intensivo de recursos se ejecuten secuencialmente en lugar de simultáneamente.
* **Agregar tiempo de búfer**: deje un espacio adecuado entre los trabajos para tener en cuenta las variaciones de procesamiento.
* **Revisar dependencias**: identifique qué trabajos deben completarse para que otros puedan iniciarse de forma segura.

## Densidad de trabajos programados {#scheduled-density}

**Gravedad de impacto**: Alto | **Problema principal**: Cuellos de botella en la canalización

**Qué buscar**: Demasiados conjuntos de datos con varios lotes programados dentro de la misma hora, especialmente cuando estos lotes se apilan y se programan cerca de ventanas de procesamiento críticas, como las horas de inicio de la segmentación.

En este patrón, verá lo siguiente:

* Varios conjuntos de datos, cada uno con varios lotes al día
* Trabajos de ETL (ingesta de lago de datos e ingesta de perfiles) agrupados dentro de la misma hora
* Ingesta por lotes programada inmediatamente antes o durante las ventanas de segmentación programadas

**Por qué esto es problemático**:

* **Cuello de botella de canalización**: cuando se apilan numerosos lotes de diferentes conjuntos de datos en un corto período de tiempo, se crea un cuello de botella de procesamiento que puede saturar la canalización de ingesta.
* **Disponibilidad de perfiles retrasada**: Es posible que los trabajos de ingesta de perfiles que se ejecutan demasiado cerca de los tiempos de inicio de la segmentación no se completen a tiempo, lo que da como resultado evaluaciones de audiencia incompletas o antiguas.
* **Segmentación impredecible**: Si los trabajos de ingesta ascendente siguen ejecutándose cuando comienza la segmentación, se arriesga a evaluar las audiencias con datos incompletos, lo que provoca la pertenencia a audiencias incorrectas.
* **Errores en cascada**: Un solo lote retrasado en una programación apilada densamente puede causar un efecto dominó, retrasando todos los lotes subsiguientes y los procesos descendentes.
* **Extracción de recursos**: Es posible que el sistema tenga problemas para asignar recursos suficientes al procesar demasiados trabajos de ingesta simultánea, lo que ralentiza los tiempos de procesamiento o produce errores.

**Cómo solucionarlo**:

* **Consolidar lotes**: Reduzca la frecuencia de los lotes combinando varios lotes pequeños en menos lotes más grandes por conjunto de datos.
* **Distribuir de forma uniforme**: Difunda los trabajos de ingesta durante todo el día en lugar de agruparlos en horarios específicos.
* **Agregar tiempo de búfer**: Asegure un búfer mínimo de 1 a 2 horas entre la finalización de la ingesta de perfiles y el inicio de la segmentación.
* **Requisitos de revisión**: evalúe si todos los conjuntos de datos realmente necesitan varios lotes diarios; muchos casos de uso funcionan con actualizaciones menos frecuentes.

## Lotes excesivos por conjunto de datos {#excessive-batches-per-dataset}

**Gravedad de impacto**: Medium | **Problema principal**: Procesamiento ineficiente

**Qué buscar**: Un solo conjunto de datos con un número excesivo de trabajos por lotes individuales programados a lo largo del día, que crea una larga pila vertical de trabajos en la cronología.

En este patrón, verá una fila del conjunto de datos con muchos trabajos de ingesta por lotes individuales programados a intervalos frecuentes, a veces decenas de lotes por día para un único conjunto de datos.

**Por qué esto es problemático**:

* **Procesamiento ineficiente**: Cada trabajo por lotes tiene costos generales (inicialización, validación, actualizaciones de metadatos). Procesar muchos lotes pequeños es significativamente menos eficiente que procesar menos lotes más grandes.
* **Mayor superficie de error**: más trabajos significan más oportunidades de error. Cada lote que falla requiere investigación y posible reprocesamiento.
* **Carga innecesaria del sistema**: los lotes pequeños y frecuentes mantienen al sistema constantemente ocupado con tareas de sobrecarga en lugar del procesamiento de datos real, lo que reduce el rendimiento general.
* **Disponibilidad de datos retrasada**: Paradójicamente, la ejecución de muchos lotes pequeños puede retrasarse cuando los datos están disponibles para procesos descendentes en comparación con los lotes consolidados.
* **Inspección difícil**: el seguimiento del éxito y el rendimiento de docenas de trabajos por lotes individuales por conjunto de datos se vuelve complejo desde el punto de vista operativo y lleva mucho tiempo.
* **Intervalo de procesamiento de perfil**: Cada lote de ingesta de perfil déclencheur el procesamiento de perfiles. Los pequeños lotes frecuentes pueden hacer que el procesamiento de perfiles se ejecute casi continuamente, lo que impide una optimización eficiente de los lotes.

**Cómo solucionarlo**:

* **Reducir la frecuencia de lotes**: consolide a menos lotes por día por conjunto de datos para la mayoría de los casos de uso.
* **Aumentar tamaño del lote**: acumule más datos antes de activar la ingesta en lugar de ingerirlos inmediatamente.
* **Alinear con las necesidades de la empresa**: compruebe si las actualizaciones por hora son realmente necesarias o si son suficientes las actualizaciones diarias o bidiarias.
* **Usar streaming para tiempo real**: cambia a la ingesta de streaming para los requisitos en tiempo real originales en lugar de simularla con lotes frecuentes.

## Próximos pasos {#next-steps}

Después de identificar los antipatrones en sus horarios de trabajo:

* Vea [detalles del trabajo](job-schedules-details.md) para investigar conjuntos de datos específicos y ejecuciones de trabajos que puedan estar causando problemas.
* Revise la [descripción general de los horarios de trabajo](job-schedules.md) para comprender las capacidades de la interfaz y de la inspección.
* Obtenga información acerca de la [ingesta por lotes](../ingestion/batch-ingestion/overview.md) para optimizar los horarios de carga de datos.
* Comprenda las [programaciones de segmentación](../segmentation/home.md) para garantizar que las evaluaciones de audiencia se realicen a tiempo correctamente.
* Explore [monitorización de flujos de datos de destino](../dataflows/ui/monitor-destinations.md) para ver la canalización de extremo a extremo.
