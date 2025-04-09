---
title: Tarjeta de modelo de puntuación de tendencia de Customer AI
description: Obtenga información acerca del modelo de IA utilizado para la inteligencia artificial aplicada al cliente.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Tarjeta de modelo de puntuación de tendencia de Customer AI

Como parte de [Servicios inteligentes en Adobe Experience Platform](../../../intelligent-services/home.md), puede usar [inteligencia artificial aplicada al cliente](../../../intelligent-services/customer-ai/overview.md) para generar predicciones y explicaciones de clientes a nivel individual.

Con la ayuda de factores influyentes, puede utilizar la inteligencia artificial aplicada al cliente para indicarle qué es lo más probable que haga un cliente y por qué. Además, puede beneficiarse de las predicciones y perspectivas de la inteligencia artificial aplicada al cliente para personalizar las experiencias de los clientes y ofrecerles las ofertas y los mensajes más adecuados.

Lea esta tarjeta de modelo para obtener información sobre el modelo de IA utilizado para impulsar la inteligencia artificial aplicada al cliente.

## Información general del modelo {#model-overview}

* La inteligencia artificial aplicada al cliente es un modelo impulsado por IA diseñado para generar puntuaciones de tendencia para los usuarios en función de sus comportamientos pasados y las interacciones con una empresa. Utilice la inteligencia artificial aplicada al cliente para predecir la probabilidad de que un cliente realice acciones específicas, como realizar una compra, interactuar con el contenido o producir errores. Este modelo se implementa en Experience Platform y se integra con varios flujos de trabajo de marketing y análisis de clientes.
* El modelo está diseñado para proporcionar a los especialistas en marketing y a los equipos de participación de los clientes información procesable mediante la predicción de la probabilidad de que un cliente realice una acción determinada, como realizar una compra, registrarse para obtener una suscripción o participar en una campaña de correo electrónico. Los resultados permiten a las empresas optimizar la segmentación de audiencia y personalizar las interacciones con los clientes en función de los comportamientos predichos.
* Este es un **modelo de clasificación de aprendizaje supervisado** que predice la probabilidad de que se produzca un evento (compra, pérdida, participación) según los datos históricos del cliente. Se entrenó utilizando árboles de decisión con potenciación de gradiente (GBDT) con regresión logística para modelar puntuaciones de tendencia.
* Los usuarios principales de este modelo son los profesionales de marketing, los analistas de datos y los equipos de participación del cliente que aprovechan Experience Platform para impulsar estrategias de marketing basadas en datos.
* La inteligencia artificial aplicada al cliente se integra directamente en los servicios de IA de Experience Platform, lo que permite a los usuarios acceder a las salidas de los modelos a través de API y paneles creados previamente. Las puntuaciones de tendencia generadas por el modelo se pueden usar en [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) y [Real-Time CDP](../../../rtcdp/home.md) para refinar la segmentación de audiencia y adaptar las estrategias de marketing.

## Uso previsto {#intended-use}

* Este modelo se usa principalmente para la **segmentación de clientes, marketing dirigido y predicción de pérdida**. Las empresas aprovechan este modelo para **predecir la intención de compra de los clientes, optimizar las campañas de marketing y mejorar los esfuerzos de personalización**. Por ejemplo, una empresa de comercio electrónico podría utilizar el modelo para identificar a los compradores con intenciones altas y ofrecerles promociones exclusivas.
* Los especialistas en marketing a menudo tienen dificultades para **identificar a los clientes adecuados para segmentar** y **optimizar los esfuerzos de participación**. Este modelo **reduce las conjeturas** al proporcionar un enfoque basado en datos para la segmentación de clientes, lo que garantiza que los recursos de marketing se asignen de forma eficaz.
* El modelo es aplicable en múltiples industrias, incluyendo el comercio electrónico, el comercio minorista, los servicios financieros, las telecomunicaciones y los medios. Cualquier empresa que dependa de la participación del cliente y del marketing personalizado puede beneficiarse de este modelo.
* El modelo **no debe usarse para la toma de decisiones de alto riesgo**, como la puntuación de crédito financiero, los diagnósticos médicos o las evaluaciones legales. Además, no está pensado para su uso en la predicción de comportamientos personales sensibles (condiciones de salud, preferencias políticas) debido a posibles preocupaciones éticas.

## Entradas y salidas de modelo {#model-inputs-and-outputs}

* El modelo procesa los datos de comportamiento del cliente, los atributos demográficos y las interacciones históricas. Esto incluye datos como la frecuencia de visita al sitio web, el historial de compras anterior, la participación con correos electrónicos de marketing y la información demográfica.
* Los datos de entrada deben estructurarse como objetos JSON que contengan atributos del cliente y señales de comportamiento. Para el procesamiento por lotes, el modelo acepta archivos CSV con el formato de los estándares de ingesta de datos de Experience Platform.
* El modelo genera una puntuación de tendencia entre 0 y 1, donde los valores más altos indican una mayor probabilidad de que se produzca el evento predicho. Además, proporciona puntuaciones de importancia de características, lo que permite a los usuarios comprender qué factores influyeron en la predicción.

**Entrada de ejemplo**

```json
{
  "customer_id": 12345,
  "past_purchases": 3,
  "last_visit_days": 7,
  "email_click_rate": 0.4
}
```

**Ejemplo de salida**

```json
{
  "customer_id": 12345,
  "propensity_score": 0.82
}
```

## Datos de formación

* El modelo fue entrenado en **datos de interacción de clientes anónimos de origen** recopilados a través de Experience Platform. Incluye **datos de comportamiento, registros de transacciones, interacciones por correo electrónico y métricas de participación** del cliente históricos en varias industrias.
* El conjunto de datos de formación consta de **10 millones de registros de clientes** procedentes de un conjunto diverso de clientes de Experience Platform. Estos registros incluyen **interacciones históricas de clientes, datos transaccionales, registros de participación de comportamiento e información demográfica** de varias industrias, como venta minorista, comercio electrónico, telecomunicaciones y finanzas. Los datos se recopilaron en un período de 24 meses, lo que garantiza una representación suficiente de las tendencias estacionales y los patrones de participación a largo plazo.
* El conjunto de datos proviene principalmente de usuarios de alta participación, lo que puede introducir un sesgo de selección. Para mitigar esto, el modelo aplica muestreo estratificado, técnicas de auditoría de sesgos y estrategias de aumento de datos.
* El conjunto de datos se somete a un amplio preprocesamiento para garantizar la coherencia, calidad y facilidad de uso de los datos.
   * **Gestión de valores que faltan**: los valores que faltan se solucionan usando una combinación de imputación media (para campos numéricos), imputación de modo (para campos categóricos) y modelado predictivo (para casos que faltan complejos).
   * **Codificación categórica**: Las variables categóricas, como los segmentos de clientes y las categorías de compra, se convierten en representaciones numéricas mediante técnicas de codificación de un solo host y de codificación de destino.
   * **Escala y normalización de características**: la escala mínima-máxima se aplica a las variables delimitadas (edad, ingresos), mientras que la estandarización del valor z se utiliza para las características distribuidas normalmente.
   * **Procesamiento previo adicional**: la canalización incluye la detección y eliminación de periféricos, el filtrado de duplicados, la estandarización de marcas de tiempo y la ingeniería de características para mejorar el modelado predictivo.

## Arquitectura de modelo y formación

* El modelo aprovecha **[!DNL Gradient Boosting Decision Trees](GBDT) usando[!DNL XGBoost]**, optimizado para datos estructurados. Se le enseña sobre las secuencias de eventos de clientes históricas para identificar patrones de comportamiento predictivos.
* El modelo se ha creado utilizando un enfoque de aprendizaje supervisado, aprovechando GBDT con [!DNL XGBoost] como algoritmo de aprendizaje principal. Adicionalmente, se incorpora la regresión logística como un modelo de referencia para la evaluación de la precisión predictiva.
* El modelo se desarrolló con **[!DNL TensorFlow]**, **[!DNL XGBoost]** y **[!DNL scikit-learn]**. La formación se ejecuta en la infraestructura de nube de Adobe AI mediante **[!DNL NVIDIA V100]GPU**, que admiten conjuntos de datos a gran escala.
* [!DNL NVIDIA V100 GPUs], con formación sobre la infraestructura de Google Cloud.
* [!DNL AUC-ROC], recuperación de precisión y validación cruzada.

## Rendimiento y evaluación

* El modelo se probó con un enfoque de validación holdout, donde el 80% de los datos se utilizó para entrenamiento y el 20% se reservó para evaluación.
* La eficacia del modelo se mide usando [!DNL AUC-ROC] (0,85), recuperación de precisión (0,78) y puntuación F1 (0,80). Estas métricas ayudan a evaluar el poder predictivo del modelo en distintos segmentos.
* Menor precisión para los nuevos segmentos de clientes con datos históricos limitados.
* El modelo puede ofrecer un rendimiento inferior al esperado para los clientes con datos históricos limitados (problema de inicio en frío). Además, los efectos de estacionalidad (tendencias de compras en días festivos) pueden requerir un reciclaje frecuente para mantener la precisión.

## Equidad y parcialidad

* El modelo se sometió a **pruebas de paridad demográfica** y a **evaluaciones de equidad contradictoria** para detectar disparidades de rendimiento en los distintos segmentos de usuarios.
* El análisis reveló una caída de rendimiento del **5% para los usuarios con datos de interacción históricos bajos**. Para solucionarlo, el modelo incorpora técnicas de reponderación durante el entrenamiento.
* El conjunto de datos está estratificado para garantizar una representación proporcional de los distintos datos demográficos de los clientes, y se introducen restricciones de equidad durante la formación para evitar que el modelo favorezca a ningún grupo en particular. Las auditorías periódicas de los sesgos se llevan a cabo mediante el análisis de la paridad demográfica, lo que permite realizar ajustes si se detectan disparidades en el rendimiento.

## Explicación e interpretabilidad

* El modelo aprovecha **[!DNL SHapley Additive Explanations](SHAP)** para cuantificar el impacto de cada característica de entrada en sus predicciones, lo que proporciona transparencia sobre cómo los atributos del cliente influyen en las puntuaciones de tendencia. Los valores SHAP permiten la interpretabilidad global, al identificar los factores más influyentes en todas las predicciones, y la interpretabilidad local, al explicar las predicciones individuales para clientes específicos.
* El modelo admite **[!DNL Local Interpretable Model-Agnostic Explanations](LIME)** y SHAP para proporcionar información sobre cómo las características de entrada influyen en las predicciones. LIME genera explicaciones locales mediante la creación de versiones perturbadas de los datos de entrada y la observación de cambios en las predicciones, mientras que SHAP asigna valores de contribución a cada característica, lo que ofrece interpretabilidad global y local de las decisiones del modelo.

## Solidez y generalización

* El modelo mantiene un 80 % de [!DNL AUC-ROC] cuando se prueba en conjuntos de datos no vistos, lo que demuestra una fuerte generalización a los nuevos registros de clientes. El rendimiento permanece estable en distintos segmentos de clientes, pero muestra una ligera degradación cuando el comportamiento del usuario se desvía significativamente de los patrones históricos.
* El modelo ha sido evaluado frente a datos perturbados y contradictorios, como la falta de datos, la inyección fuera de lo normal y el etiquetado incorrecto intencional. Si bien el rendimiento sigue siendo sólido en condiciones normales, se observó una menor degradación de la precisión (aproximadamente del 3 al 5 %) en condiciones de extrema confrontación.

## Consideraciones de seguridad y privacidad

* El modelo **no procesa ni conserva información de identificación personal (PII)**, y todos los datos utilizados para la formación se han convertido en anónimos y se han agregado. Se adhiere al estricto cumplimiento de las políticas de privacidad del RGPD, la CCPA y Adobe internas para garantizar un uso responsable de los datos.
* El modelo incorpora técnicas de privacidad diferenciales para añadir ruido controlado a los datos, lo que evita la reidentificación de las personas. Además, se usan **métodos de hash, anonimización y tokenización para eliminar PII** antes del aprendizaje y la inferencia del modelo.

## Implementación e integración

* El modelo está alojado en los servicios de IA de Adobe Experience Platform e integrado con varias aplicaciones de Adobe. Está disponible a través de puntos finales de API, lo que permite un acceso fluido a predicciones en tiempo real y procesamiento por lotes en los flujos de trabajo de marketing y participación del cliente.
* El modelo se ejecuta en una implementación basada en **[!DNL Kubernetes]** con capacidades de escalado automático para manejar cargas de trabajo variables de manera eficiente. Los recursos de cómputo incluyen [!DNL NVIDIA V100] GPU para la formación y la inferencia optimizada basada en CPU para la escalabilidad en tiempo real.

## Monitorización y mantenimiento

* El modelo se monitoriza continuamente **a través de[!DNL WatsonX]**, y realiza un seguimiento de los indicadores de rendimiento clave como la desviación de precisión, los cambios de importancia de las características y la estabilidad de la predicción. Los mecanismos de detección de anomalías y alertas notifican al equipo cuando se producen desviaciones significativas del comportamiento esperado.
* El modelo se vuelve a entrenar mensualmente utilizando datos actualizados de interacción del cliente para garantizar una relevancia continua. El reciclaje periódico ayuda a mitigar la deriva de datos y las fluctuaciones estacionales que podrían afectar a la precisión predictiva

## Preocupaciones éticas e IA responsable

* El modelo podría introducir un sesgo en la toma de decisiones si no se monitorea correctamente. Por ejemplo, si ciertas características demográficas están sobrerrepresentadas en los datos de formación, el modelo podría favorecer injustamente a grupos de clientes específicos.
* Experience Platform sigue las directrices de IA responsables y se asegura de que los modelos se sometan a **auditorías de sesgos, pruebas de imparcialidad y supervisión humana** antes de su implementación.

## Limitaciones conocidas

* Es posible que el modelo tenga dificultades para predecir con precisión los resultados de los productos recién lanzados o de los segmentos de clientes en los que no hay datos históricos suficientes. Además, las variaciones estacionales en el comportamiento de los clientes pueden causar fluctuaciones en la precisión predictiva si no se contabilizan durante el reciclaje.
* El rendimiento disminuye cuando el historial del cliente es escaso, como cuando se trata de nuevos compradores o usuarios con datos de participación mínimos. Además, si el comportamiento de los clientes **cambia debido a factores externos como desaceleraciones económicas o tendencias del sector**, el modelo puede requerir una adaptación rápida para mantener la precisión.

## Mejoras futuras

* Las futuras iteraciones incluirán técnicas de aprendizaje de transferencia para mejorar el rendimiento de los usuarios de inicio en frío y mejorar la adaptabilidad a los comportamientos cambiantes de los clientes. Además, se introducirá la integración de datos en tiempo real para mejorar la capacidad de respuesta y precisión de los modelos en entornos de marketing dinámicos.
