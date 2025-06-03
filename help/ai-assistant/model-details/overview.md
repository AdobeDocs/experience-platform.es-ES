---
title: Detalles Del Modelo Para La Transparencia Del Modelo De IA En Adobe Experience Platform
description: Obtenga información acerca de los detalles del modelo en Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 74a8ef82-cff9-4a7e-95c8-f915eb664eda
source-git-commit: 6623c7dad0fc4ddb7cb79e8f474b824915f130fc
workflow-type: tm+mt
source-wordcount: '3171'
ht-degree: 0%

---

# Detalles del modelo para la transparencia del modelo de IA en Adobe Experience Platform

Un detalle del modelo de IA es el formato estándar mediante el cual se comunica la transparencia del modelo de IA. Los detalles del modelo proporcionan información completa sobre el modelo subyacente en el que se basa una herramienta de IA determinada. Los detalles del modelo incluyen información como el propósito de una herramienta de IA, datos de formación, métricas de rendimiento, limitaciones y consideraciones éticas. Puede utilizar la transparencia que proporcionan los detalles del modelo para comprender mejor las capacidades y limitaciones del modelo, así como para promover un uso responsable y justo de la IA.

Los detalles del modelo son públicos y están pensados para mejorar la comprensión, tanto del cliente existente como del potencial, de los modelos de IA que utiliza Adobe. Los detalles del modelo suelen ser estáticos. Sin embargo, hay varios aspectos de los modelos de IA que pueden cambiar con el tiempo, incluidos el linaje, el sesgo y otros atributos de transparencia.

Lea este documento para obtener más información sobre los detalles del modelo en Adobe Experience Platform.

## Secciones de detalles del modelo {#model-detail-sections}

Un detalle de modelo se compone de una variedad de secciones diferentes, cada una centrada en un aspecto particular del modelo de IA.

Lea lo siguiente para obtener una guía sobre las diferentes secciones de los detalles de un modelo, incluida la información sobre las preguntas que abordan.

### Información general del modelo {#model-overview}

La descripción general del modelo contiene información general sobre un modelo de IA. Utilice esta sección para proporcionar información como el nombre, el propósito y el tipo de su modelo de IA. Además, puede utilizar esta sección para identificar a los usuarios previstos y explicar cómo el modelo se integra con Experience Platform.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Cuál es el nombre del modelo? | El nombre y la versión oficiales del modelo de IA. | **CustomerAI Propensity Scoring Model v2.0** <br>CustomerAI es un modelo con tecnología de IA diseñado para generar puntuaciones de tendencia para los usuarios en función de sus comportamientos pasados e interacciones con una empresa. Ayuda a predecir la probabilidad de que un cliente realice acciones específicas, como realizar una compra, interactuar con contenido o producir pérdidas. Este modelo se implementa en Adobe Experience Platform y se integra con varios flujos de trabajo de análisis de clientes y marketing.</br> |
| ¿Cuál es el propósito del modelo? | Una breve descripción de para qué está diseñado el modelo. | El modelo está diseñado para proporcionar a los especialistas en marketing y a los equipos de participación de los clientes información procesable mediante la predicción de la probabilidad de que un cliente realice una acción determinada, como realizar una compra, registrarse para obtener una suscripción o participar en una campaña de correo electrónico. Los resultados permiten a las empresas optimizar la segmentación de audiencia y personalizar las interacciones con los clientes en función de los comportamientos predichos. |
| ¿Qué tipo de modelo es? | El tipo de modelo, como clasificación, regresión, generativo, etc. | Este es un modelo de clasificación de aprendizaje supervisado de s **s** que predice la probabilidad de que se produzca un evento (por ejemplo, compra, pérdida, participación) según los datos históricos del cliente. Se entrenó utilizando árboles de decisión con potenciación de gradiente (GBDT) con regresión logística para modelar puntuaciones de tendencia. |
| ¿Quiénes son los usuarios previstos? | Los grupos de usuarios internos y externos a los que está destinado el modelo. | Los usuarios principales de este modelo son los profesionales de marketing, los analistas de datos y los equipos de participación del cliente que aprovechan Adobe Experience Platform para impulsar estrategias de marketing basadas en datos. |
| ¿Cómo se integra este modelo con Adobe Experience Platform? | Los detalles de integración y las API utilizadas, así como cómo se ajustan a los flujos de trabajo. | CustomerAI se integra directamente en los servicios de IA de **Adobe Experience Platform**, lo que permite a los usuarios acceder a los resultados de los modelos a través de las API y los paneles creados previamente. Las puntuaciones de tendencia generadas por el modelo se pueden usar en **Adobe Journey Optimizer**, **y Adobe Real-Time CDP** para refinar la segmentación de audiencia y adaptar las estrategias de marketing. |

{style="table-layout:auto"}

+++

### Uso previsto {#intended-use}

La sección de uso previsto contiene información sobre los casos de uso principales del modelo de IA. Puede utilizar esta sección para ampliar los problemas que su modelo pretende resolver, las industrias o dominios para los que su modelo es relevante y los casos de uso incorrecto que deben evitarse al utilizar su modelo de IA.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Cuáles son los casos de uso principales? | Los escenarios donde se espera utilizar el modelo. | Este modelo se usa principalmente para la **segmentación de clientes, marketing dirigido y predicción de pérdida**. Las empresas aprovechan este modelo para **predecir la intención de compra de los clientes, optimizar las campañas de marketing y mejorar los esfuerzos de personalización**. Por ejemplo, una empresa de comercio electrónico podría utilizar el modelo para identificar a los compradores con intenciones altas y ofrecerles promociones exclusivas. |
| ¿Qué problemas resuelve este modelo? | Los principales puntos problemáticos abordados por el modelo. | Los especialistas en marketing a menudo tienen dificultades para **identificar a los clientes adecuados para segmentar** y **optimizar los esfuerzos de participación**. Este modelo **reduce las conjeturas** al proporcionar un **enfoque basado en datos** para la segmentación de clientes, lo que garantiza que los recursos de marketing se asignen de manera eficiente. |
| ¿Para qué industrias o dominios es relevante este modelo? | Una lista de las industrias aplicables. | El modelo es aplicable en múltiples industrias, entre ellas **comercio electrónico, venta minorista, servicios financieros, telecomunicaciones y medios**. Cualquier empresa que dependa de la participación del cliente y del marketing personalizado puede beneficiarse de este modelo. |
| ¿Cómo no se debe utilizar este modelo? | Cualquier caso de uso indebido que deba evitarse. | El modelo **no debe usarse para la toma de decisiones de alto riesgo**, como **puntuación de crédito financiero, diagnósticos médicos o evaluaciones legales**. Además, no está pensada para su uso en **predicción de comportamientos personales sensibles** (como problemas de salud, preferencias políticas) debido a posibles problemas éticos. |

{style="table-layout:auto"}

+++

### Entradas y salidas de modelo {#model-inputs-and-outputs}

La sección de entradas y salidas del modelo contiene información sobre los tipos de datos admitidos que el modelo toma como entrada y devuelve como salida. Puede utilizar esta sección para proporcionar ejemplos de las entradas y salidas de datos que son relevantes para su modelo de IA.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Qué tipos de datos toma el modelo como entrada? | Los tipos de datos que el modelo toma como entrada, entre los que se incluyen: funciones de datos, formatos y fuentes. | El modelo procesa **datos de comportamiento del cliente, atributos demográficos e interacciones históricas**. Esto incluye datos como la frecuencia de visita al sitio web, el historial de compras anterior, la participación con correos electrónicos de marketing y la información demográfica. |
| ¿En qué formato deben estar las entradas? | Los formatos de entrada aceptados. | Los datos de entrada deben estar estructurados como **objetos JSON** que contengan atributos del cliente y señales de comportamiento. Para el procesamiento por lotes, el modelo acepta **archivos CSV** con un formato acorde con los estándares de ingesta de datos de Adobe Experience Platform. |
| ¿Qué genera la salida del modelo? | El tipo de salida generada por el modelo. | El modelo genera una puntuación de tendencia entre 0 y 1, donde los valores más altos indican una mayor probabilidad de que se produzca el evento predicho. Además, proporciona puntuaciones de importancia de características, lo que permite a los usuarios comprender qué factores influyeron en la predicción. |
| ¿Cuáles son algunas entradas y salidas de ejemplo? | Una entrada de muestra y la salida correspondiente. | <ul><li>**Entrada de ejemplo:** json { &quot;customer_id&quot;: 12345, &quot;last_purchases&quot;: 3, &quot;last_visit_days&quot;: 7, &quot;email_click_rate&quot;: 0.4 }</li><li>**Ejemplo de salida:** json { &quot;customer_id&quot;: 12345, &quot;propensity_score&quot;: 0.82 }</li></ul> |

{style="table-layout:auto"}

+++

### Datos de formación {#training-data}

La sección de datos de formación contiene información sobre los conjuntos de datos que se utilizaron para entrenar un modelo de IA determinado. Puede utilizar esta sección para obtener más información sobre el tamaño y el origen de los datos de formación, los sesgos identificados en el conjunto de datos y cómo se han preprocesado los datos.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Qué conjuntos de datos se utilizaron para entrenar el modelo? | Descripción de las fuentes de datos. | El modelo se formó en datos de interacción de clientes anónimos de origen recopilados mediante Adobe Experience Platform. Incluye datos de comportamiento del cliente históricos, registros de transacciones, interacciones por correo electrónico y métricas de participación en varios sectores. |
| ¿Cuál es el tamaño y la fuente de los datos? | El volumen y el origen del conjunto de datos de formación. | El conjunto de datos de formación consta de 10 millones de registros de clientes procedentes de un conjunto diverso de clientes de Adobe Experience Platform. Estos registros incluyen interacciones históricas de clientes, datos transaccionales, registros de participación de comportamiento e información demográfica de varias industrias, como venta minorista, comercio electrónico, telecomunicaciones y finanzas. Los datos se recopilaron en un período de 24 meses, lo que garantiza una representación suficiente de las tendencias estacionales y los patrones de participación a largo plazo. |
| ¿Hay algún sesgo conocido en el conjunto de datos? | Consideraciones parciales y esfuerzos de mitigación. | El conjunto de datos proviene principalmente de usuarios de alta participación, lo que puede introducir un sesgo de selección. Para mitigar esto, el modelo aplica muestreo estratificado, técnicas de auditoría de sesgos y estrategias de aumento de datos. |
| ¿Cómo se preprocesan los datos? | Pasos necesarios para limpiar y preparar los datos. | El conjunto de datos se somete a un amplio preprocesamiento para garantizar la coherencia, calidad y facilidad de uso de los datos. <ol><li>**Gestión de valores que faltan**: los valores que faltan se solucionan usando una combinación de imputación media (para campos numéricos), imputación de modo (para campos categóricos) y modelado predictivo (para casos que faltan complejos).</li><li>**Codificación categórica:** Las variables categóricas, como los segmentos de clientes y las categorías de compra, se convierten en representaciones numéricas mediante técnicas de codificación de un solo host y de codificación de destino.</li><li>**Escala y normalización de características:** La escala mínima-máxima se aplica a variables delimitadas (por ejemplo, edad, ingresos), mientras que la estandarización de puntuación z se usa para características distribuidas normalmente.</li><li>**Procesamiento previo adicional:** La canalización incluye detección y eliminación de periféricos, filtrado de duplicados, estandarización de marcas de tiempo e ingeniería de características para mejorar la predicción.</li></ol> |

{style="table-layout:auto"}

+++

### Arquitectura de modelo y formación {#model-architecture-and-training}

La sección de arquitectura y formación del modelo describe el modelo del modelo de IA. Esta sección hace referencia a la estructura y el diseño del modelo de IA, incluidos detalles sobre el tipo de algoritmo y los métodos de evaluación utilizados. También puede utilizar esta sección para proporcionar información sobre los marcos de formación utilizados, así como los recursos de cálculo utilizados en la formación.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Qué arquitectura utiliza el modelo? | El tipo de red neuronal, método de ensamblado, etc. | El modelo aprovecha Gradient Boosting Decision Trees (GBDT) utilizando XGBoost, optimizado para datos estructurados. Se le enseña sobre las secuencias de eventos de clientes históricas para identificar patrones de comportamiento predictivos. |
| ¿Qué algoritmos se aplicaron? | Las técnicas de aprendizaje automático utilizadas. | El modelo se construye utilizando un enfoque de aprendizaje supervisado, aprovechando Gradient Boosting Decision Trees (GBDT) con XGBoost como algoritmo de aprendizaje principal. Adicionalmente, se incorpora la regresión logística como un modelo de referencia para la evaluación de la precisión predictiva. |
| ¿Qué marcos de formación se han utilizado? | Las bibliotecas o plataformas utilizadas para la formación. | El modelo fue desarrollado utilizando TensorFlow, XGBoost y scikit-learn. La formación se ejecuta en la infraestructura en la nube de Adobe AI utilizando GPU NVIDIA V100, compatibles con conjuntos de datos a gran escala. |
| ¿Qué recursos informáticos se utilizaron para la formación? | El hardware y los recursos de la nube utilizados para la formación. | GPU NVIDIA V100, formadas en la infraestructura de Google Cloud. |
| ¿Qué métodos de evaluación se utilizaron? | Las métricas y los procedimientos de prueba utilizados para la evaluación. | AUC-ROC, recuperación de precisión y validación cruzada. |

{style="table-layout:auto"}

+++

### Rendimiento y evaluación {#performance-and-evaluation}

La sección de rendimiento y evaluación contiene información sobre las métricas y los métodos utilizados para evaluar el rendimiento del modelo para las tareas previstas. Puede utilizar esta sección para proporcionar información sobre las métricas de evaluación que se utilizaron, así como sobre las debilidades o los casos de error identificados.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Cómo se probó el modelo? | Métodos utilizados para validar el rendimiento. | El modelo se probó con un enfoque de validación holdout, donde el 80% de los datos se utilizó para entrenamiento y el 20% se reservó para evaluación. |
| ¿Qué métricas de evaluación se utilizaron? | Los indicadores clave de rendimiento. | La efectividad del modelo se mide usando **AUC-ROC (0,85)**, **precision-reminder (0,78)** y **F1-score (0,80)**. Estas métricas ayudan a evaluar el poder predictivo del modelo en distintos segmentos. |
| ¿Cómo varía el rendimiento en los distintos escenarios? | Las variaciones de rendimiento específicas del contexto. | Menor precisión para los nuevos segmentos de clientes con datos históricos limitados. |
| ¿Existen debilidades o casos de error conocidos? | Limitaciones o puntos de error. | El modelo puede ofrecer un rendimiento inferior al esperado para los clientes con datos históricos limitados (problema de inicio en frío). Además, los efectos de estacionalidad, como las tendencias de compras en días festivos, pueden requerir un reciclaje frecuente para mantener la precisión. |

{style="table-layout:auto"}

+++

### Equidad y parcialidad {#fairness-and-bias}

La sección de equidad y sesgo contiene información sobre el rendimiento del modelo de IA con respecto a las métricas de imparcialidad y sesgo. La equidad se refiere a la capacidad del modelo para proporcionar resultados equitativos entre diferentes grupos demográficos y casos de uso, mientras que el sesgo se refiere a errores sistemáticos que resultan en resultados injustos. Utilice esta sección para obtener más información sobre las comprobaciones de equidad que se realizaron y para analizar cómo el modelo mitiga el sesgo.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Qué controles de equidad se realizaron? | Los procesos de análisis y mitigación de sesgos que se realizaron. | El modelo se sometió a pruebas de paridad demográfica y evaluaciones de equidad contradictoria para detectar disparidades de desempeño entre los distintos segmentos de usuarios. |
| ¿Afecta el modelo de forma desproporcionada a determinados grupos? | Cualquier disparidad en el rendimiento que se haya identificado. | El análisis reveló una caída del rendimiento del 5 % para los usuarios con datos de interacción históricos bajos. Para resolver esto, el modelo incorpora técnicas de reponderación durante el entrenamiento. |
| ¿Cómo mitiga el modelo el sesgo? | Las técnicas utilizadas para abordar el sesgo. | El conjunto de datos está estratificado para garantizar una representación proporcional de los distintos datos demográficos de los clientes, y se introducen restricciones de equidad durante la formación para evitar que el modelo favorezca a ningún grupo en particular. Las auditorías periódicas de los sesgos se llevan a cabo mediante el análisis de la paridad demográfica, lo que permite realizar ajustes si se detectan disparidades en el rendimiento. |

{style="table-layout:auto"}

+++

### Explicación e interpretabilidad {#explainability-and-interpretability}

La sección de explicabilidad e interpretabilidad contiene información sobre la capacidad de un modelo de IA para proporcionar explicaciones claras y comprensibles, y la facilidad con la que un usuario humano puede comprender cómo las características de entrada afectan a las predicciones y respuestas. Utilice esta sección para explicar cómo los usuarios pueden comprender mejor por qué el modelo toma determinadas decisiones y qué herramientas o técnicas están disponibles para la interpretabilidad.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Pueden los usuarios comprender por qué el modelo toma determinadas decisiones? | Los métodos de interpretabilidad utilizados por el modelo. | El modelo aprovecha **SHapley Additive Explanations (SHAP)** para cuantificar el impacto de cada característica de entrada en sus predicciones, proporcionando transparencia sobre cómo los atributos del cliente influyen en las puntuaciones de tendencia. Los valores SHAP permiten la interpretabilidad global, al identificar los factores más influyentes en todas las predicciones, y la interpretabilidad local, al explicar las predicciones individuales para clientes específicos. |
| ¿Qué herramientas o técnicas están disponibles para la interpretabilidad? | Las herramientas de explicación disponibles. | El modelo admite **Explicaciones interpretables locales no basadas en modelos (LIME)** y SHAP para proporcionar información sobre cómo las características de entrada influyen en las predicciones. LIME genera explicaciones locales mediante la creación de versiones perturbadas de los datos de entrada y la observación de cambios en las predicciones, mientras que SHAP asigna valores de contribución a cada característica, lo que ofrece interpretabilidad global y local de las decisiones del modelo. |

{style="table-layout:auto"}

+++

### Solidez y generalización {#robustness-and-generalization}

La sección de solidez y generalización contiene información sobre el rendimiento del modelo de IA en datos no vistos. Además, puede utilizar esta sección para explicar cómo el modelo mantiene su rendimiento y precisión a partir de entradas inesperadas o desafiantes.

>[!TIP]
>
>En IA, &quot;datos no vistos&quot; se refiere a datos que son diferentes de los datos en los que se formó un modelo determinado.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Qué rendimiento tiene el modelo en los datos no vistos? | Los resultados de las pruebas de rendimiento de la generalización. | El modelo mantiene un **80% AUC-ROC** cuando se prueba en conjuntos de datos no vistos, lo que demuestra una fuerte generalización a los nuevos registros de clientes. El rendimiento permanece estable en distintos segmentos de clientes, pero muestra una ligera degradación cuando el comportamiento del usuario se desvía significativamente de los patrones históricos. |
| ¿Se ha sometido el modelo a pruebas de resistencia para detectar datos contradictorios? | Los detalles de la evaluación de la solidez. | El modelo ha sido evaluado frente a datos perturbados y contradictorios, como la falta de datos, la inyección fuera de lo normal y el etiquetado incorrecto intencional. Si bien el rendimiento sigue siendo sólido en condiciones normales, se observó una menor degradación de la precisión (aproximadamente del 3 al 5 %) en condiciones de extrema confrontación. |

{style="table-layout:auto"}

+++

### Consideraciones de seguridad y privacidad {#security-and-privacy-considerations}

La sección Consideraciones de seguridad y privacidad contiene información sobre las medidas y prácticas implementadas para proteger los datos confidenciales y garantizar el uso seguro del modelo. Puede utilizar esta sección para responder a preguntas sobre cómo gestiona el modelo los datos confidenciales.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿El modelo gestiona datos confidenciales? | Cualquier información que cumpla con las leyes de privacidad. | El modelo no procesa ni conserva información de identificación personal (PII) y todos los datos utilizados para la formación se anonimizan y agregan. Se adhiere al estricto cumplimiento de las políticas de privacidad del RGPD, la CCPA y Adobe internas para garantizar un uso responsable de los datos. |
| ¿Qué técnicas de preservación de la privacidad se utilizaron? | Las técnicas utilizadas para garantizar las medidas de privacidad. | El modelo incorpora técnicas de privacidad diferenciales para añadir ruido controlado a los datos, lo que evita la reidentificación de las personas. Además, se utilizan métodos de hash, anonimización y tokenización para eliminar la PII antes del aprendizaje y la inferencia del modelo. |

{style="table-layout:auto"}

+++

### Monitorización y mantenimiento {#monitoring-and-maintenance}

La sección de supervisión y mantenimiento contiene información sobre cómo se supervisa el rendimiento del modelo a lo largo del tiempo y con qué frecuencia se vuelve a entrenar el modelo. Puede utilizar esta sección para proporcionar información sobre cómo se realiza el seguimiento de métricas como precisión, precisión, recuperación y latencia.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Cómo se supervisa el rendimiento del modelo a lo largo del tiempo? | Detalles sobre los mecanismos de seguimiento utilizados para el modelo. | El modelo se monitoriza continuamente a través de WatsonX, rastreando indicadores clave de rendimiento como la desviación de precisión, los cambios de importancia de las características y la estabilidad de predicción. Los mecanismos de detección de anomalías y alertas notifican al equipo cuando se producen desviaciones significativas del comportamiento esperado. |
| ¿Con qué frecuencia se vuelve a entrenar el modelo? | La frecuencia de las actualizaciones del modelo. | El modelo se vuelve a entrenar mensualmente utilizando datos actualizados de interacción del cliente para garantizar una relevancia continua. El reciclaje periódico ayuda a mitigar la deriva de datos y las fluctuaciones estacionales que podrían afectar a la precisión predictiva. |

{style="table-layout:auto"}

+++

### Consideraciones éticas e IA responsable {#ethical-considerations-and-responsible-ai}

La sección Consideraciones éticas y IA responsable contiene información sobre cualquier preocupación ética asociada con su modelo de IA. Esta sección también contiene la eficacia con la que el modelo se alinea con los principios de IA responsables. Utilice esta sección para proporcionar información sobre los posibles impactos éticos del uso de su modelo, incluido el reconocimiento de sesgos, la garantía de equidad y la prevención de daños a personas o grupos.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Qué preocupaciones éticas se asocian con este modelo? | Los riesgos potenciales que se han identificado. | El modelo podría introducir un sesgo en la toma de decisiones si no se monitorea correctamente. Por ejemplo, si ciertas características demográficas están sobrerrepresentadas en los datos de formación, el modelo podría favorecer injustamente a grupos de clientes específicos. |
| ¿Cómo se alinea el modelo con los principios de IA responsable? | Información sobre cómo el modelo cumple con las directrices éticas de IA. | Adobe Experience Platform sigue las directrices de IA responsable, lo que garantiza que los modelos se sometan a auditorías de sesgos, pruebas de equidad y supervisión humana antes de la implementación. |

{style="table-layout:auto"}

+++

### Limitaciones conocidas {#known-limitations}

La sección Limitaciones conocidas contiene información sobre las limitaciones existentes identificadas para su modelo de IA. Utilice esta sección para subrayar las condiciones en las que el modelo de IA puede tener un mal rendimiento y para esbozar las limitaciones que los usuarios deben tener en cuenta.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Cuáles son las limitaciones conocidas del modelo? | Cualquier restricción de rendimiento o de caso de uso identificada. | Es posible que el modelo tenga dificultades para predecir con precisión los resultados de los productos recién lanzados o de los segmentos de clientes en los que no hay datos históricos suficientes. Además, las variaciones estacionales en el comportamiento de los clientes pueden causar fluctuaciones en la precisión predictiva si no se contabilizan durante el reciclaje. |
| ¿En qué condiciones el modelo funciona mal? | Cualquier debilidad identificada con respecto al modelo. | El rendimiento disminuye cuando el historial del cliente es escaso, como cuando se trata de nuevos compradores o usuarios con datos de participación mínimos. Además, si el comportamiento de los clientes cambia debido a factores externos como las desaceleraciones económicas o las tendencias del sector, el modelo puede requerir una rápida adaptación para mantener la precisión. |

{style="table-layout:auto"}

+++

### Mejoras futuras {#future-improvements}

La sección de futuras mejoras contiene información sobre las actualizaciones de funciones planificadas para su modelo de IA. Utilice esta sección para obtener más información sobre la hoja de ruta de mejoras.

+++Ver preguntas y ejemplos de respuestas

| Pregunta | Información necesaria | Respuesta de ejemplo |
| --- | --- | --- |
| ¿Qué mejoras se han planificado para futuras iteraciones? | Plan de trabajo para mejoras. | Las futuras iteraciones incluirán técnicas de aprendizaje de transferencia para mejorar el rendimiento de los usuarios de inicio en frío y mejorar la adaptabilidad a los comportamientos cambiantes de los clientes. Además, se introducirá la integración de datos en tiempo real para mejorar la capacidad de respuesta y precisión de los modelos en entornos de marketing dinámicos. |

{style="table-layout:auto"}

+++
