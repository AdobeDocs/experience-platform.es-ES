---
title: Monitorización de cambios significativos y previsión de audiencias con el asistente de IA
description: Aprenda a utilizar el Asistente de IA para monitorizar los cambios significativos y prever las audiencias en Adobe Experience Platform.
badge: Alpha
source-git-commit: 37d2886cc5d7b3a019d23f76973d79547865298b
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Monitorice los cambios significativos y prevea el crecimiento de la audiencia con el asistente de IA

>[!AVAILABILITY]
>
>Esta función está en Alpha y es posible que no esté disponible para su organización. Para participar en el programa de Alpha y acceder a esta función, póngase en contacto con el equipo de cuenta de Adobe.

En el panorama actual del marketing basado en datos, es esencial disponer de perspectivas oportunas y precisas. Tanto si es un usuario empresarial como si participa en operaciones de marketing, necesita la capacidad de interactuar de forma coherente con su audiencia y realizar ajustes rápidos e impactantes basados en perspectivas claras. Para mantener la alineación o lograr sus objetivos comerciales, debe tener la información procesable necesaria para impulsar campañas eficaces y optimizar los recursos.

Puede utilizar el Asistente de IA para Adobe Experience Platform para monitorizar los cambios significativos y proporcionar previsiones de crecimiento para los tamaños de audiencia y de conjuntos de datos. A continuación, puede utilizar esta información para garantizar la integridad de los datos de audiencia y ofrecer proyecciones prospectivas para apoyar la toma de decisiones basada en datos.

Lea este documento para obtener información sobre cómo monitorizar los cambios significativos y pronosticar el crecimiento y las fluctuaciones de la audiencia mediante el asistente de IA.

## Terminología y definiciones clave {#key-terminology-and-definitions}

Consulte la siguiente tabla para obtener una lista de la terminología importante y sus definiciones correspondientes.

| Terminología | Definición |
| --- | --- |
| Cambio significativo | Un cambio significativo es un cambio grande basado en porcentajes en el tamaño de la audiencia o del conjunto de datos, definido por umbrales específicos (por ejemplo, 10 % para audiencias grandes). Los cambios significativos ayudan a identificar anomalías que afectan a la estabilidad de los datos. |
| Anomalías | Las anomalías son variaciones de datos inesperadas, como un crecimiento repentino del 20 % en una audiencia de **compradores de alto valor**. Una anomalía puede deberse a un posible problema de ingesta de datos o a un cambio en la definición de la audiencia. |
| Datos históricos | Los datos históricos se refieren a datos a largo plazo, por lo general de uno a tres años. Puede utilizar datos históricos para rastrear patrones. **Nota**: durante la fase de Alpha, el Asistente de IA proporciona datos históricos de hasta 13 meses. |
| Datos emergentes/recientes | Los datos emergentes o recientes se refieren a puntos de datos observados durante un corto periodo, generalmente durante una semana o hasta 30 días. Puede utilizar datos emergentes o recientes para resaltar tendencias inmediatas y realizar ajustes rápidos. |
| Pronóstico | Las previsiones de A son predicciones de tamaños futuros de audiencias o conjuntos de datos basadas en tendencias pasadas. Puede utilizar los datos de previsión para apoyar la planificación a largo plazo. |
| Tamaño de público | El tamaño de la audiencia se refiere al número total de perfiles dentro de una audiencia. El tamaño de la audiencia se actualiza con cada iteración de la ingesta de datos. |
| Plazo de comparación | El asistente de IA utiliza lapsos de tiempo de comparación predefinidos. Las anomalías recientes tienen de forma predeterminada una retrospectiva de siete días, mientras que las anomalías anteriores cubren 30 días. Las tendencias históricas abarcan hasta 13 meses. |

{style="table-layout:auto"}

## Ejemplos de casos de uso {#use-case-examples}

La capacidad del asistente de IA para monitorizar cambios significativos y prever audiencias puede ser especialmente útil para los siguientes casos de uso:

### Operaciones de marketing

Los profesionales de las operaciones de marketing (operaciones de marketing) son responsables de garantizar la integridad y la coherencia de los datos de audiencia. Como miembro de un equipo de operaciones de marketing, sus responsabilidades pueden incluir la monitorización de la calidad de los datos, la respuesta a cambios inesperados y el mantenimiento de una base estable para todos los esfuerzos de marketing. Puede utilizar la detección de anomalías del Asistente de IA para detectar y abordar cambios significativos de audiencias o conjuntos de datos, lo que evita interrupciones que podrían afectar al rendimiento de la campaña.

### Usuarios y especialistas en marketing empresariales

Como usuario empresarial y experto en marketing, puede confiar en las perspectivas de audiencia precisas para tomar decisiones basadas en datos y garantizar que las campañas lleguen a las audiencias a las que están destinadas de forma eficaz. Con las capacidades de previsión del Asistente de IA, puede anticipar el crecimiento o la reducción de audiencias y habilitar ajustes estratégicos en los recursos y la segmentación a lo largo del tiempo.

## Funciones principales

>[!IMPORTANT]
>
>Las siguientes funciones se encuentran en Alpha y se centran en funcionalidades básicas de monitorización y previsión. Como esta función está en Alpha, debe asegurarse de volver a comprobar la precisión de las respuestas que reciba del asistente de IA.

### Monitorización de cambios significativos en audiencias y datos

Puede utilizar el Asistente de IA para identificar cambios significativos en los tamaños de audiencias y conjuntos de datos mediante el seguimiento de desviaciones de patrones típicos. Cada cambio significativo se basa en umbrales predefinidos adaptados a la escala de la audiencia.

| Tamaño de público | Número de perfiles | Descripción |
| --- | --- | --- |
| Audiencias pequeñas | De 1 a 100 000 perfiles | Indica un cambio del 30 % o más, a menos que se especifique un porcentaje específico. |
| Audiencias de Medium | De 100 000 a 500 000 perfiles | Indica un cambio del 25% o más, a menos que se especifique un porcentaje específico. |
| Audiencias grandes | De 500.000 a 1 millón de perfiles | Indica un cambio del 20 % o más, a menos que se especifique un porcentaje específico. |
| Audiencias muy grandes | Más de 1 millón de perfiles | Indica un cambio del 10 % o más, a menos que se especifique un porcentaje específico. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Ejemplo de escenario

Los cambios significativos indican anomalías que pueden afectar a la estabilidad de la audiencia o a la fiabilidad de los datos. Por ejemplo, si una audiencia de **compradores de alto valor** experimenta una caída repentina del 15 % en su tamaño, el Asistente de IA lo marcará como un cambio significativo. A continuación, puede utilizar esta información para investigar y resolver posibles problemas antes de que afecten a sus campañas.

>[!ENDSHADEBOX]

>[!TIP]
>
>El asistente de IA no le notifica automáticamente la ocurrencia de cambios significativos en los tamaños de audiencia. Debe iniciar una conversación con el asistente de IA y preguntar qué audiencias han cambiado significativamente o por un margen específico, en un período de tiempo específico.

### Prever el crecimiento de audiencias y conjuntos de datos

Puede utilizar el Asistente de IA para hacer referencia a tendencias de datos históricos y proyectar tamaños de audiencias y conjuntos de datos futuros. A continuación, puede utilizar estas perspectivas para apoyar la planificación de recursos y los ajustes de estrategia. Actualmente, puede utilizar el Asistente de IA para pronosticar el crecimiento de la audiencia y del conjunto de datos durante 30 días. Si comprende el crecimiento o la disminución de audiencia esperado, puede ajustar las estrategias de segmentación y asignar los recursos en consecuencia.

### Perspectivas sobre los tamaños históricos de audiencia

Además de detectar cambios significativos, puede utilizar el Asistente de IA para recuperar perspectivas históricas y comparar los tamaños actuales de audiencia o conjunto de datos con los datos anteriores. Esta función admite el seguimiento de tendencias a largo plazo y la evaluación del impacto de actividades de marketing anteriores.

Puede hacer preguntas al asistente de IA como: &quot;¿Cuál fue el tamaño de mi audiencia de &quot;Clientes fieles&quot; el mes pasado? para ver datos históricos sobre el crecimiento o la disminución de esta audiencia específica.

## Ejemplos de preguntas para la monitorización de cambios significativos

Puede plantear sus preguntas sobre el asistente de IA de varias formas.

* Si su pregunta incluye un porcentaje, como **&quot;¿Qué audiencias cambiaron en un 30% o más?&quot;**, el Asistente de IA usará el porcentaje como punto de referencia.
* Si su pregunta no especifica un porcentaje, el Asistente de IA interpretará los cambios significativos en función de la configuración predeterminada.

Consulte las siguientes tablas para ver ejemplos de consultas que ilustran cómo el Asistente de IA interpreta los cambios significativos en función del tamaño de la audiencia:

| Información de audiencia o cambio de audiencia | Ejemplo |
| --- | --- |
| <ul><li>¿Cuál es el tamaño actual de {AUDIENCE_NAME}?</li><li>Mostrar las audiencias que mostraron un cambio de {PERCENT} sobre {DATE_DURATION}.</li></ul> | <ul><li>¿Cuál es el tamaño actual de la audiencia de compradores de alto valor?</li><li>Muestre las audiencias que han mostrado un cambio del 20 % durante la última semana.</li></ul> |

{style="table-layout:auto"}

| Consultas específicas de la audiencia | Ejemplo |
| --- | --- |
| <ul><li>¿Qué audiencias cambiaron más de {PERCENT} en {DATE_OR_DURATION}?</li><li>Mostrarme audiencias con un cambio significativo sobre {DATE_OR_DURATION}.</li><li>Mostrar la distribución de audiencias con los cambios más grandes en {DATE_OR_DURATION}.</li><li>Mostrar las audiencias que han disminuido más de {PERCENT} en {DATE_OR_DURATION}.</li></ul> | <ul><li>¿Qué audiencias cambiaron más del 20 % en la última semana?</li><li>Muéstreme audiencias con un cambio significativo en los últimos seis meses.</li><li>Muéstreme la distribución de audiencias con los cambios más grandes del 1 al 31 de octubre.</li><li> Muéstreme las audiencias que han disminuido en más de un 20 % desde el 31 de agosto. |

{style="table-layout:auto"}

## Más información

### Explicación del umbral de &quot;cambio significativo&quot;

Puede especificar un porcentaje específico al consultar el Asistente de IA para obtener información sobre los cambios significativos. Si no proporciona un porcentaje específico, el Asistente de IA hará referencia a un conjunto predefinido de umbrales para determinar qué califica como un cambio significativo. Los umbrales predeterminados se basan en el tamaño de una audiencia determinada. Consulte la siguiente tabla para obtener información sobre qué constituye un cambio significativo en función del tamaño de la audiencia:

| Tamaño de público | ¿Qué es importante? |
| --- | --- |
| 1 millón o más | 10% o más |
| De 500 k a 1 millón | 20% o más |
| 100k a 500k | 25% o más |
| Menos de 100 k | 30 % o más |

### Cronología genérica y fechas específicas

El Asistente de IA admite comparaciones basadas en el tiempo específicas y genéricas para tamaños de audiencia, interpretándolas en función del contexto proporcionado en la consulta.

>[!BEGINTABS]

>[!TAB Escalas de tiempo genéricas]

Las escalas de tiempo genéricas hacen referencia a consultas que utilizan un lenguaje como &quot;esta semana&quot; o &quot;la semana pasada&quot;. Si hace al Asistente de IA una pregunta como &quot;¿Qué audiencias cambiaron en más del 20 % en la última semana?&quot;, calculará y comparará el tamaño promedio de la **audiencia promedio** durante el período especificado.

Utilice este método para obtener una vista más amplia de los cambios de audiencia a lo largo del tiempo, lo que le permite comprender mejor las tendencias en intervalos semanales o mensuales.

>[!TAB Fechas específicas]

Si su pregunta hace referencia a una fecha específica, el Asistente de inteligencia artificial comparará los **tamaños de audiencia exactos** en cada una de las fechas proporcionadas.

Utilice esta comparación precisa para analizar los cambios entre puntos específicos en el tiempo y obtener información sobre cómo puede evolucionar el tamaño de la audiencia en días concretos.

>[!ENDTABS]

Puede aprovechar esta flexibilidad para comprender mejor la dinámica de audiencia en periodos de tiempo amplios y precisos. Tanto si realiza un seguimiento de las tendencias generales como si examina los turnos exactos entre fechas específicas, puede utilizar el mecanismo adaptable del asistente de IA para recuperar la comparación más relativa para la consulta.

## Preguntas frecuentes {#faq}

Lea esta sección para obtener respuestas a las preguntas más frecuentes sobre la monitorización de cambios significativos y la previsión de audiencias con el asistente de IA.

### ¿Cuántos datos históricos puedo ver para ver cómo aumenta o disminuye el tamaño de la audiencia?

El asistente de IA conserva 12 meses de datos históricos del tamaño de la audiencia. Puede hacer preguntas sobre los cambios de audiencia dentro de este periodo para comprender los patrones de crecimiento o caída durante el año pasado.

### ¿Hasta dónde en la historia puedo llegar para ver cambios en la audiencia?

El asistente de IA realiza un seguimiento de los cambios de audiencia desde el día en que se activa en la organización y se remonta hasta el último cambio en la definición de audiencia. Una vez activado, el asistente de IA supervisa y registra continuamente los cambios de definición durante un máximo de 12 meses, lo que permite realizar comparaciones y rastreos de datos en el futuro.

### ¿Cuántos datos históricos se necesitan para una previsión?

Se requieren al menos 30 días de datos para realizar previsiones fiables a partir del último cambio en la definición de audiencia. En algunos casos, como la previsión de [!DNL Black Friday], el Asistente de IA puede necesitar hasta 12 meses de datos históricos.

### ¿Cómo interpreta el asistente de IA &quot;recientemente&quot;?

El asistente de IA interpreta &quot;recientemente&quot; como los últimos siete días. Para las preguntas que hacen referencia a cambios recientes, el asistente de IA considera los datos de este período de tiempo para identificar tendencias o cambios.

### ¿Cómo compara el asistente de IA los tamaños de audiencia?

Cuando se mencionan fechas específicas, el asistente de IA compara el tamaño de la audiencia en esos días específicos. Para preguntas más generales, como las que hacen referencia a los &quot;últimos tres meses&quot; o a la &quot;última semana&quot;, AI Assistant compara el tamaño promedio de ese período con el promedio del día más reciente.

### ¿Cómo de actuales son los datos de audiencia del asistente de IA?

El asistente de IA puede tardar entre 24 y 48 horas en actualizar los datos de Real-time Customer Data Platform. Por lo tanto, para preguntas que hagan referencia al &quot;ayer&quot;, AI Assistant interpreta esto como un día antes de que los datos más recientes que tiene estén disponibles.

## Funciones fuera de ámbito

Actualmente no se admiten las siguientes capacidades:

### Análisis avanzado de la causa raíz

Aunque el Asistente de IA puede identificar cambios significativos, actualmente no puede proporcionar un análisis detallado de las causas básicas de estos cambios. Las futuras iteraciones del asistente de IA tienen como objetivo especificar qué conjuntos de datos o atributos contribuyen a cambios significativos en las audiencias.

### Tamaños completos de conjuntos de datos históricos

En este momento no se admite el seguimiento histórico completo de los tamaños de datos. Actualmente, el asistente de IA proporciona el historial de audiencias y conjuntos de datos durante un máximo de 13 meses.