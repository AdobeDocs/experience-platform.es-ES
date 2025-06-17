---
title: Detalles del modelo de puntuación de tendencia de Customer AI
description: Obtenga información acerca del modelo de IA utilizado para la inteligencia artificial aplicada al cliente.
source-git-commit: 6fe2041c0dc5f7f4b98dee00d3a793469b5f64db
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Detalles del modelo de puntuación de tendencia de Customer AI

## Información general del modelo {#model-overview}

* **Nombre y versión del modelo**: Modelo de puntuación de tendencia de inteligencia artificial aplicada al cliente
* **Propósito del modelo**: el modelo está diseñado para proporcionar a los especialistas en marketing y a los equipos de participación del cliente información procesable mediante la predicción de la probabilidad de que un consumidor realice una acción determinada, como realizar una compra, suscribirse a una suscripción o participar en una campaña de correo electrónico. Los resultados permiten a las empresas optimizar la segmentación de audiencia y personalizar las interacciones de los consumidores en función de los comportamientos predichos.
* **Usuarios previstos**: Los usuarios principales de este modelo son profesionales de marketing, analistas de datos y equipos de participación de clientes que aprovechan [Real-Time CDP](../../rtcdp/home.md) para impulsar estrategias de marketing basadas en datos.
* **Casos de uso**: Este modelo se usa principalmente para la segmentación de consumidores, el marketing segmentado y la predicción de pérdidas. Las empresas aprovechan este modelo para predecir la intención de compra de los consumidores, optimizar las campañas de marketing y mejorar los esfuerzos de personalización. Por ejemplo, una empresa de comercio electrónico podría utilizar el modelo para identificar a los compradores con intenciones altas y ofrecerles promociones exclusivas.
* **Puntos problemáticos**: Los especialistas en marketing a menudo tienen dificultades para identificar a los consumidores adecuados a quienes dirigirse y optimizar los esfuerzos de participación. Este modelo reduce las conjeturas al proporcionar un enfoque basado en datos para la segmentación de los consumidores, lo que garantiza que los recursos de marketing se asignen de forma eficaz.
* **Posible uso indebido**: el modelo no debe utilizarse en casos de uso de alto riesgo, como la puntuación de crédito financiero, diagnósticos médicos o evaluaciones legales. Además, el modelo no debe utilizarse para predecir comportamientos sensibles a nivel personal (como condiciones de salud, preferencias políticas).

## Detalles del modelo {#model-details}

* **Tipo de modelo**: Se trata de un modelo de clasificación de aprendizaje supervisado que predice la probabilidad de que se produzca un evento (como compra, pérdida o participación) según los datos de consumidor históricos. Se entrenó utilizando árboles de decisión con potenciación de gradiente (GBDT) con regresión logística para modelar puntuaciones de tendencia.
* **Entrada**: El modelo procesa datos de comportamiento del consumidor, atributos demográficos e interacciones históricas. Esto incluye datos como la frecuencia de visita al sitio web, el historial de compras anterior, la participación con correos electrónicos de marketing y la información demográfica.
* **Output**: el modelo genera una puntuación entre 0 y 100, donde los valores más altos indican una mayor probabilidad de que el evento predicho ocurra entre la cohorte de población calificada. Además, proporciona puntuaciones de importancia de características, lo que permite a los especialistas en marketing comprender qué factores influyeron en la predicción.

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

* **Datos de formación y preprocesamiento**: el conjunto de datos de formación de cada cliente se obtiene directamente de sus propios datos en Adobe Experience Platform. Esto incluye las interacciones históricas del cliente, los registros transaccionales, los registros de participación de comportamiento y la información demográfica recopilada y almacenada en su instancia de Adobe Experience Platform. El conjunto de datos aprovecha los datos específicos del cliente en el periodo de tiempo que ha elegido, capturando las tendencias estacionales y los patrones de participación únicos. Antes de usar, el conjunto de datos de cada cliente se somete a un preprocesamiento personalizado según sus características de datos, incluida la administración de valores que faltan, la codificación categórica, la escala de características, la detección de periféricos y la ingeniería de características para garantizar una calidad y una facilidad de uso óptimas para su caso de uso específico.
   * Los datos de consumidor utilizados para la formación no se utilizan entre clientes.
* **Especificaciones de formación**: El modelo aprovecha [!DNL LightGBM] con [!DNL GBM], optimizado para datos estructurados. Se le enseña sobre las secuencias de eventos de clientes históricas para identificar patrones de comportamiento predictivos.
* **Marcos de formación**: El modelo se desarrolló con [!DNL LightGBM] y [!DNL scikit-learn], y está alojado en la infraestructura en la nube de Adobe AI.
* **Infraestructura de formación**: [!DNL Databricks] clústeres.

## Evaluación de modelo {#model-evaluation}

* **Métricas y procedimientos de evaluación**: La efectividad del modelo se mide usando [!DNL AUC-ROC]. Dado que la inteligencia artificial aplicada al cliente se dirige a una amplia gama de casos de uso del cliente, no se puede saber el rango operativo. Por lo tanto, utilizamos una métrica [!DNL AUC] que es independiente del alcance y el presupuesto.
* **Datos de evaluación y preprocesamiento**: Los datos de evaluación incluyen registros de consumidores de exclusión y se preprocesan de manera similar a los datos de formación con los pasos de normalización, codificación y limpieza de las características para que coincidan con las expectativas del formato de entrada. Después de que la ventana de resultados haya pasado, podemos realizar una evaluación final del rendimiento.

## Implementación de modelo {#model-deployment}

* **Implementación de modelo**: el modelo está alojado en los servicios de IA de Adobe Experience Platform e integrado con varias aplicaciones de Adobe. Está disponible a través de puntos finales de API, lo que permite un acceso fluido a predicciones en tiempo real y procesamiento por lotes en los flujos de trabajo de marketing y participación del consumidor.
* **Supervisión del modelo**: El modelo se supervisa continuamente mediante la supervisión del modelo para ver la desviación de la configuración de formación. Las retenciones periódicas (una vez cada 3 meses) se ejecutan automáticamente.
* **Actualización del modelo**: El modelo se vuelve a entrenar una vez cada varios meses (máximo una vez cada 6 meses) utilizando datos actualizados de interacción del consumidor para garantizar una relevancia continua. El reciclaje periódico ayuda a mitigar la deriva de datos y las fluctuaciones estacionales que podrían afectar a la precisión predictiva.

## Explicabilidad {#explainability}

**Explicación del modelo**: el modelo aprovecha [!DNL SHapley Additive Explanations] (SHAP) para cuantificar el impacto de cada característica de entrada en sus predicciones, proporcionando transparencia sobre cómo los atributos de consumidor influyen en las puntuaciones de tendencia. Los valores SHAP permiten tanto la interpretabilidad global, al identificar los factores más influyentes en todas las predicciones, como la interpretabilidad local, lo que explica las predicciones individuales para consumidores específicos. El modelo también admite [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Equidad y parcialidad {#fairness-and-bias}

* **Modelo justo**: Este modelo está entrenado en datos de comportamiento anónimos asociados con ID de cookies, sin acceso a atributos demográficos protegidos como edad, sexo o etnia. Como tal, la medición directa de la equidad entre grupos sensibles no es factible. Los esfuerzos de mitigación de sesgos incluyen la normalización de la frecuencia de actividad del usuario, la supresión de las características excesivamente dominantes y la realización de comprobaciones de calibración de puntuación entre cohortes. Tenemos en cuenta el sesgo de actualización y monitorizamos el sesgo de exposición mediante la evaluación de predicciones de modelos sobre el tráfico aleatorio de exclusión. Se están realizando evaluaciones para detectar y reducir la amplificación de sesgos y los bucles de retroalimentación durante la implementación del modelo.
* **Sesgos de datos**: el conjunto de datos proviene principalmente de usuarios con un alto nivel de participación, lo que puede introducir sesgos de selección. Para mitigar esto, el modelo aplica estrategias de muestreo. Según el caso de uso, los clientes deben considerar cómo los potenciales sesgos en los resultados del modelo pueden alinearse con o afectar a su aplicación prevista.

## Solidez {#robustness}

**Solidez del modelo**: El modelo mantiene una fuerte generalización para los nuevos registros de consumidores. El rendimiento permanece estable en distintos segmentos de consumidores, pero muestra una ligera degradación cuando el comportamiento del usuario se desvía significativamente de los patrones históricos.

## Consideraciones éticas {#ethical-considerations}

**Consideraciones éticas asociadas con el modelo**: este modelo está diseñado para casos de uso de marketing y los clientes deben tener mucho cuidado al aplicarlo en dominios confidenciales o regulados, como el crédito o el empleo. Los resultados son probabilísticos y se derivan de datos de comportamiento, que pueden reflejar sesgos históricos o de representación. Se recomienda a los clientes que apliquen la supervisión humana. Adobe Experience Platform sigue las directrices de IA responsable, lo que garantiza que los modelos se sometan a auditorías de sesgos, pruebas de equidad y supervisión humana antes de la implementación. Para obtener más información, consulte los [Principios éticos de IA de Adobe](https://www.adobe.com/content/dam/cc/en/ai-ethics/pdfs/Adobe-AI-Ethics-Principles.pdf?msockid=0d85c8269eb36f0801d0ddb49fd16ebc).