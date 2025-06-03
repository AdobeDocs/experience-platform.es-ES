---
title: Tarjeta de modelo de puntuación de tendencia de Customer AI
description: Obtenga información acerca del modelo de IA utilizado para la inteligencia artificial aplicada al cliente.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: dddd699f231d54ee44b33f86a5c9e59c0aedc30c
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Tarjeta de modelo de puntuación de tendencia de Customer AI

## Información general del modelo {#model-overview}

* El modelo de puntuación de tendencia de inteligencia artificial aplicada al cliente está diseñado para proporcionar a los especialistas en marketing y a los equipos de participación del cliente perspectivas procesables mediante la predicción de la probabilidad de que un cliente realice una acción determinada, como realizar una compra, registrarse para una suscripción o participar en una campaña de correo electrónico. Los resultados permiten a las empresas optimizar la segmentación de audiencia y personalizar las interacciones con los clientes en función de los comportamientos predichos.
* Los usuarios principales de este modelo son profesionales de marketing, analistas de datos y equipos de participación de clientes que aprovechan [Real-Time CDP](../../../rtcdp/home.md) para impulsar estrategias de marketing basadas en datos.
* Este modelo se utiliza principalmente para la segmentación de clientes, el marketing dirigido y la predicción de pérdidas. Las empresas aprovechan este modelo para predecir la intención de compra de los clientes, optimizar las campañas de marketing y mejorar los esfuerzos de personalización. Por ejemplo, una empresa de comercio electrónico podría utilizar el modelo para identificar a los compradores con intenciones altas y ofrecerles promociones exclusivas.
* Los especialistas en marketing a menudo tienen dificultades para identificar a los clientes adecuados a los que dirigirse y optimizar los esfuerzos de participación. Este modelo reduce las conjeturas al proporcionar un enfoque basado en datos para la segmentación de clientes, lo que garantiza que los recursos de marketing se asignen de forma eficaz.
* El modelo no debe utilizarse para la toma de decisiones de alto riesgo, como la puntuación del crédito financiero, diagnósticos médicos o evaluaciones legales. Además, no está pensado para utilizarse en la predicción de comportamientos sensibles a nivel personal (p. ej., condiciones de salud, preferencias políticas) debido a posibles problemas éticos.

## Detalles del modelo {#model-details}

* Es un modelo de clasificación de aprendizaje supervisado que predice la probabilidad de que se produzca un evento (compra, pérdida, participación) según los datos históricos del cliente. Se entrenó utilizando árboles de decisión con potenciación de gradiente (GBDT) con regresión logística para modelar puntuaciones de tendencia.
* El modelo procesa los datos de comportamiento del cliente, los atributos demográficos y las interacciones históricas. Esto incluye datos como la frecuencia de visita al sitio web, el historial de compras anterior, la participación con correos electrónicos de marketing y la información demográfica.
* El modelo genera una puntuación entre 0 y 100, donde los valores más altos indican una mayor probabilidad de que el evento predicho se produzca entre la cohorte de población calificada. Además, proporciona puntuaciones de importancia de características, lo que permite a los usuarios comprender qué factores influyeron en la predicción.

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
  "SCORE": 89 
}
```

## Formación de modelo {#model-training}

* El conjunto de datos de formación de cada cliente se obtiene directamente de sus propios datos en Experience Platform. Esto incluye las interacciones históricas del cliente, los registros transaccionales, los registros de participación de comportamiento y la información demográfica recopilada y almacenada en su instancia de Experience Platform. El conjunto de datos aprovecha los datos específicos del cliente en el periodo de tiempo que ha elegido, capturando las tendencias estacionales y los patrones de participación únicos. Antes de usar, el conjunto de datos de cada cliente se somete a un preprocesamiento personalizado según sus características de datos, incluida la administración de valores que faltan, la codificación categórica, la escala de características, la detección de periféricos y la ingeniería de características para garantizar una calidad y una facilidad de uso óptimas para su caso de uso específico.
* El modelo aprovecha [!DNL LightGBM] con [!DNL GBM], optimizado para datos estructurados. Se le enseña sobre las secuencias de eventos de clientes históricas para identificar patrones de comportamiento predictivos.
* El modelo se desarrolló con [!DNL LightGBM] y [!DNL scikit-learn], y está entrenado en la infraestructura en la nube de Adobe AI.
* Los recursos de equipo utilizados para la formación del modelo son [!DNL Databricks] clústeres.

## Evaluación de modelo {#model-evaluation}

* La efectividad del modelo se mide usando [!DNL AUC-ROC]. Dado que la inteligencia artificial aplicada al cliente se dirige a una amplia gama de casos de uso del cliente, no se puede saber el rango operativo. Por lo tanto, se utiliza la métrica [!DNL AUC] porque es independiente del alcance y el presupuesto.
* Los datos de evaluación incluyen registros de clientes en espera y se preprocesan de forma similar a los datos de formación con pasos de normalización, codificación y limpieza de funciones para que coincidan con las expectativas de formato de entrada. Una vez que haya pasado la ventana de resultados, se puede llevar a cabo la evaluación final del rendimiento.

## Implementación de modelo {#model-deployment}

* El modelo está alojado en los servicios de IA de Experience Platform e integrado con varias aplicaciones de Adobe. Está disponible a través de puntos finales de API, lo que permite un acceso fluido a predicciones en tiempo real y procesamiento por lotes en los flujos de trabajo de marketing y participación del cliente.
* El modelo se monitoriza continuamente a través de la monitorización del modelo para ver la desviación de la configuración del entrenamiento. Las retenciones periódicas (una vez cada 3 meses) se ejecutan automáticamente.
* El modelo se vuelve a entrenar una vez cada varios meses (máximo una vez cada 6 meses) utilizando datos actualizados de interacción del cliente para garantizar una relevancia continua. El reciclaje periódico ayuda a mitigar la deriva de datos y las fluctuaciones estacionales que podrían afectar a la precisión predictiva.

## Explicabilidad {#explainability}

El modelo aprovecha [!DNL SHapley Additive Explanations] (SHAP) para cuantificar el impacto de cada característica de entrada en sus predicciones, lo que proporciona transparencia sobre cómo los atributos del cliente influyen en las puntuaciones de tendencia. Los valores SHAP permiten la interpretabilidad global, al identificar los factores más influyentes en todas las predicciones, y la interpretabilidad local, al explicar las predicciones individuales para clientes específicos. El modelo también admite [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Equidad y parcialidad {#fairness-and-bias}

* Este modelo está entrenado en datos de comportamiento anónimos asociados con ID de cookies, sin acceso a atributos demográficos protegidos como edad, sexo o etnia. Como tal, la medición directa de la equidad entre grupos sensibles no es factible. Los esfuerzos de mitigación de sesgos incluyen la normalización de la frecuencia de actividad del usuario, la supresión de las características excesivamente dominantes y la realización de comprobaciones de calibración de puntuación entre cohortes.
* El modelo tiene en cuenta el sesgo de actualización y monitoriza el sesgo de exposición mediante la evaluación de predicciones de modelos sobre el tráfico aleatorio de exclusión. Se están realizando evaluaciones para detectar y reducir la amplificación de sesgos y los bucles de retroalimentación durante la implementación del modelo.
* El conjunto de datos proviene principalmente de usuarios de alta participación, lo que puede introducir un sesgo de selección. Para mitigar esto, el modelo aplica estrategias de muestreo.

## Solidez {#robustness}

El modelo mantiene una fuerte generalización de los nuevos registros de clientes. El rendimiento permanece estable en distintos segmentos de clientes, pero muestra una ligera degradación cuando el comportamiento del usuario se desvía significativamente de los patrones históricos.

## Consideraciones de privacidad y seguridad {#privacy-and-security-considerations}

* El modelo no procesa ni conserva información de identificación personal (PII) y todos los datos utilizados para la formación se anonimizan y agregan. Se adhiere al estricto cumplimiento de las políticas de privacidad del RGPD, la CCPA y Adobe internas. El modelo incorpora técnicas de privacidad diferenciales, hash, anonimización y tokenización para garantizar la privacidad.
* La inteligencia artificial aplicada al cliente respeta sus preferencias de consentimiento. Una vez que haya [configurado y habilitado su directiva de consentimiento](../../../data-governance/policies/user-guide.md#create-a-consent-policy), la inteligencia artificial aplicada al cliente aceptará los datos de consentimiento recopilados de usted. Solo se utilizan datos consentidos para puntuar el modelo en ejecuciones posteriores del modelo. Las nuevas puntuaciones reemplazarán las puntuaciones antiguas y se pueden utilizar en la segmentación. Actualmente, esta función solo está disponible para los clientes de HealthCare Shield y para los clientes de Privacy and Security shield.

## Consideraciones éticas {#ethical-considerations}

El modelo podría introducir un sesgo en la toma de decisiones. En un esfuerzo por evitarlo, Experience Platform sigue las directrices de IA responsable, lo que garantiza que los modelos se sometan a auditorías de sesgos, pruebas de equidad y supervisión humana antes de su implementación.
