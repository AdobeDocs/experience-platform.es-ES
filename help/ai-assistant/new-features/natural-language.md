---
title: Estimación del lenguaje natural con el asistente de IA
description: Aprenda a utilizar las capacidades de estimación de lenguaje natural de AI Assistant.
badge: Alpha
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Estimación de lenguaje natural con AI Assistant

>[!AVAILABILITY]
>
>Esta función está en Alpha y es posible que no esté disponible para su organización. Para participar en el programa de Alpha y acceder a esta función, póngase en contacto con el equipo de cuenta de Adobe.

Puede utilizar las capacidades de Estimación de lenguaje natural de AI Assistant para Adobe Experience Platform para estimar los tamaños de audiencia y predecir las tendencias de audiencia en función de preguntas simples y conversacionales. Con esta función, puede hacer que las perspectivas de audiencia sean más accesibles e intuitivas. Esto puede resultar especialmente útil en los casos de uso de operaciones de marketing y empresariales, especialmente si gestiona las audiencias diariamente y depende de estas perspectivas para configurar estrategias de marketing eficaces.

Con las capacidades de procesamiento de lenguaje natural de AI Assistant, puede hacer preguntas como: &quot;¿Cuántos perfiles tengo en California entre 25 y 35 años&quot; o &quot;¿Cuántos clientes de alto valor tenemos?&quot; o incluso &quot;¿Qué porcentaje de mi audiencia tendrá probabilidad de comprar dentro del próximo mes?&quot; A continuación, el asistente de IA interpreta estas preguntas y devuelve estimaciones o puntuaciones de tendencia que puede utilizar para tomar decisiones basadas en datos.

Lea este documento para aprender a utilizar las capacidades de estimación de lenguaje natural de AI Assistant.

## Terminología y definiciones clave {#key-terminology-and-definitions}

Consulte la siguiente tabla para obtener una lista de la terminología importante y sus definiciones correspondientes.

| Terminología | Definición |
| --- | --- |
| Estimación del tamaño de audiencia | Proceso de calcular el número de miembros dentro de una audiencia específica en función de criterios definidos. Puede basar las estimaciones de tamaño en los datos de perfil, incluidos los perfiles que no están en una audiencia. Además, puede recuperar las estimaciones de tamaño de audiencia sin tener que crear primero una audiencia. Utilice esta perspectiva para comprender la escala del alcance de las campañas segmentadas. |
| Estimación de tendencia | Una predicción de la probabilidad de que los miembros de una audiencia muestren comportamientos específicos (como realizar una compra o producir una pérdida) en un lapso de tiempo determinado. La estimación de tendencia es específica para audiencias dentro de Real-time Customer Data Platform, pero puede incluir datos de perfil, incluidos perfiles en en cualquier audiencia. Puede hacer referencia a esta perspectiva al optimizar sus campañas y administrar las estrategias de retención de audiencia. |
| Procesamiento de lenguaje natural | La capacidad del asistente de IA para interpretar y responder a las preguntas que se formulan en el lenguaje cotidiano, lo que le permite interactuar de manera conversacional y recibir perspectivas relevantes sin utilizar consultas técnicas. |
| Lapsos de tiempo predefinidos | Intervalos de tiempo estándar ( &quot;mes pasado&quot;, &quot;30 días siguientes&quot;) admitidos por el asistente de IA para estimar el tamaño y las tendencias de la audiencia. **Nota**: Es posible que los lapsos de tiempo personalizados no sean totalmente compatibles durante la fase de Alpha. |
| Datos de instantánea | Conjunto de datos utilizado por el asistente de IA para proporcionar estimaciones. Estos datos se actualizan desde Real-time Customer Data Platform cada 24 a 48 horas y, por lo tanto, las perspectivas pueden no reflejar cambios en la audiencia en tiempo real. |

{style="table-layout:auto"}

## Ejemplos de casos de uso {#use-case-examples}

Las capacidades de estimación de lenguaje natural del asistente de IA pueden ser especialmente útiles para los siguientes casos de uso:

### Operaciones de marketing

Como profesional de operaciones de marketing, sus responsabilidades pueden incluir la administración y la monitorización de datos de audiencias para garantizar que se ajusten a sus objetivos comerciales. Con la función de estimación de lenguaje natural del asistente de IA, puede recopilar rápidamente perspectivas sobre los tamaños de audiencia y las tendencias sin tener que crear una audiencia primero o tener amplios conocimientos de análisis de datos.

ayudándoles a mantener un enfoque coherente y basado en datos en sus flujos de trabajo.

### Usuarios y especialistas en marketing empresariales

Como usuario empresarial y experto en marketing, el acceso rápido a los datos de audiencia puede ser crucial para el éxito de la planificación, la segmentación y la evaluación de campañas. Con la función de estimación de lenguaje natural de AI Assistant, puede simplificar el acceso a la información de la audiencia, hacer preguntas directas y recibir perspectivas procesables que ayuden en la creación de audiencias y la optimización de campañas.

## Funciones principales

>[!IMPORTANT]
>
>Las siguientes características son en Alpha y se centran en las capacidades fundacionales de estimación de lenguaje natural. Como esta función está en Alpha, debe asegurarse de volver a comprobar la precisión de las respuestas que reciba del asistente de IA.

### Estimación del tamaño de audiencia

Puede utilizar consultas en lenguaje natural para solicitar al Asistente de IA que calcule el tamaño de audiencias específicas. Esta función puede resultar especialmente útil para medir el alcance y el impacto de las audiencias de destino. Por ejemplo, como estratega de marketing, puede hacer preguntas como:

* &quot;¿Cuántos perfiles viven en Nueva York?&quot;
* &quot;¿Cuántos perfiles tengo con un correo electrónico y he aceptado?&quot;

Utilice esta función para simplificar el proceso de estimación del tamaño de la audiencia y obtener respuestas inmediatas sin necesidad de navegar por filtros de datos complejos o definiciones de segmentos.

### Estimación de tendencia de audiencia

>[!TIP]
>
>Su cuenta de Experience Platform debe estar aprovisionada con [inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/overview.md) para poder usar las capacidades de estimación de tendencia del Asistente para IA.

Puede utilizar la estimación de la tendencia de la audiencia para identificar la probabilidad de comportamientos o acciones específicos dentro de una audiencia. Por ejemplo, puede hacer preguntas como las siguientes:

* &quot;¿Qué porcentaje de mi audiencia actual tendrá probabilidad de comprar en el próximo mes?&quot;
* &quot;¿Cuántos perfiles tengo con una alta tendencia a la conversión?&quot;

Al hacer preguntas sobre lenguaje natural, puede recuperar puntuaciones de tendencia que indiquen el porcentaje o la probabilidad de que los miembros de la audiencia muestren determinados comportamientos, lo que le ayuda a realizar ajustes proactivos en sus campañas o estrategias de retención.

## Ejemplos de preguntas para estimación del tamaño y la tendencia de la audiencia

A continuación, encontrará preguntas de ejemplo que puede realizar al asistente de IA para comprender mejor el tamaño de la audiencia y las tendencias de comportamiento:

### Estimación del tamaño de audiencia

* &quot;¿Cuántos perfiles tengo con un número de correo electrónico o de teléfono móvil?&quot;
* &quot;¿Cuántos perfiles tengo en Nueva York?&quot;
* &quot;¿Cuáles son los cinco estados principales en los que viven mis clientes?&quot;

### Estimación de propensión de audiencia

* &quot;¿Qué porcentaje de mi audiencia tiene probabilidades de comprar dentro del próximo mes?&quot;
* &quot;¿Cuántos clientes se espera que realicen la conversión en el próximo trimestre?&quot;

Puede utilizar la flexibilidad que ofrecen las consultas en lenguaje natural para obtener información rápida sobre la dinámica de audiencias sin necesidad de conocimientos técnicos.

## Preguntas más frecuentes

Lea esta sección para obtener respuestas a las preguntas más frecuentes sobre la estimación del lenguaje natural con el Asistente de IA.

### ¿Con qué frecuencia actualiza el asistente de IA los datos de audiencia?

Los datos del asistente de IA se actualizan cada 24 a 48 horas. Por lo tanto, las estimaciones pueden reflejar ligeros retrasos. Esto significa que, cuando pregunta por los datos &quot;actuales&quot;, la respuesta refleja la instantánea más reciente, que puede tener hasta 48 horas de antigüedad.

### ¿Puedo solicitar tamaños de audiencia o tendencias con intervalos de fechas personalizados?

Actualmente, el Asistente de IA admite intervalos de fechas predefinidos, como &quot;mes pasado&quot; o &quot;30 días siguientes&quot;. Los intervalos de fechas personalizados que exceden estas opciones predefinidas no son totalmente compatibles en la fase de Alpha. Si se solicita un lapso de tiempo personalizado, el Asistente de inteligencia artificial proporcionará perspectivas en función del lapso de tiempo disponible más cercano.

### ¿Cómo calcula el asistente de IA las puntuaciones de tendencia?

Las puntuaciones de tendencia se calculan usando [Customer AI](../../intelligent-services/customer-ai/overview.md). El asistente de IA utiliza modelos de aprendizaje automático para predecir la probabilidad de comportamientos de audiencia específicos, como compras y pérdidas, dentro del lapso de tiempo solicitado. Durante la fase de Alpha, el cálculo de la puntuación de tendencia en el asistente de IA no utiliza eventos de experiencia ni datos de comportamiento.

### ¿AI Assistant estimará los tamaños de audiencia o las tendencias en función de los datos en tiempo real?

No, los datos en tiempo real no están disponibles en este momento. Las estimaciones se basan en instantáneas de datos recientes, actualizadas cada 24 a 48 horas. Las actualizaciones en tiempo real están fuera del ámbito durante la fase de Alpha.

### ¿Cómo se calculan las tendencias?

El asistente de IA se basa en los modelos de inteligencia artificial aplicada al cliente para responder a cualquier puntuación de probabilidad o tendencia.

## Funciones fuera de ámbito

Actualmente no se admiten las siguientes capacidades:

### Estimaciones del tamaño de la audiencia basadas en datos de eventos de comportamiento

Actualmente, el Asistente de IA no puede responder preguntas basadas en datos de comportamiento como **&quot;Cuántos usuarios han agregado un producto al carro de compras en los últimos 30 días&quot;**. Sin embargo, puede crear un atributo calculado en Real-Time CDP que precalcule dichos valores. Estos atributos calculados están disponibles en el asistente de IA. Para obtener más información, lea la documentación sobre [atributos calculados](../../profile/computed-attributes/overview.md).

### Actualizaciones de datos en tiempo real

Las estimaciones proporcionadas por AI Assistant se basan en instantáneas de datos recientes, pero no en tiempo real. Los datos se actualizan cada 24 a 48 horas, por lo que las perspectivas reflejan este retraso. Esta limitación significa que los usuarios no pueden recibir actualizaciones instantáneas si un segmento o conjunto de datos cambia significativamente en un corto periodo de tiempo.