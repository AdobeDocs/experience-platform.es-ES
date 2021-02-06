---
keywords: Experience Platform;optimizar;modelo;Área de trabajo de ciencia de datos;temas populares;perspectivas de modelo
solution: Experience Platform
title: Optimizar un modelo con el marco de perspectivas de modelo
topic: tutorial
type: Tutorial
description: El marco de perspectivas de modelo proporciona al científico de datos herramientas en el área de trabajo de ciencias de datos para realizar elecciones rápidas e informadas para modelos óptimos de aprendizaje automático basados en experimentos.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# Optimizar un modelo mediante el marco de perspectivas de modelo

Model Insights Framework proporciona al científico de datos herramientas en [!DNL Data Science Workspace] para tomar decisiones rápidas e informadas para modelos óptimos de aprendizaje automático basados en experimentos. El marco mejorará la velocidad y la eficacia del flujo de trabajo del aprendizaje automático, así como la facilidad de uso de los científicos de datos. Esto se lleva a cabo proporcionando una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático para facilitar el ajuste del modelo. El resultado final permite a los científicos de datos y a los científicos de datos ciudadanos tomar mejores decisiones de optimización de modelos para sus clientes finales.

## ¿Qué son las métricas?

Después de implementar y entrenar un modelo, el próximo paso que un científico de datos daría es encontrar el desempeño del modelo. Se utilizan varias métricas para determinar la eficacia de un modelo en comparación con otros. Algunos ejemplos de métricas utilizadas son:
- Precisión de la clasificación
- Área bajo curva
- Matriz de confusión
- Informe de clasificación

## Configuración del código de fórmula

Actualmente, Model Insights Framework admite los siguientes tiempos de ejecución:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

El código de muestra de las fórmulas se encuentra en el repositorio [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) en `recipes`. En este tutorial se hará referencia a archivos específicos de este repositorio.

### Scala {#scala}

Existen dos maneras de incorporar métricas a las fórmulas. Una es utilizar las métricas de evaluación predeterminadas proporcionadas por el SDK y la otra es escribir métricas de evaluación personalizadas.

#### Métricas de evaluación predeterminadas para Scala

Las evaluaciones predeterminadas se calculan como parte de los algoritmos de clasificación. Estos son algunos valores predeterminados para los evaluadores que están implementados actualmente:

| Clase de evaluador | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

El evaluador se puede definir en la fórmula del archivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) de la carpeta `recipe`. A continuación se muestra el código de muestra que habilita `DefaultBinaryClassificationEvaluator`:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Una vez habilitada una clase de evaluador, se calculará una serie de métricas durante la formación de forma predeterminada. Las métricas predeterminadas se pueden declarar explícitamente agregando la siguiente línea a su `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Si la métrica no está definida, las métricas predeterminadas estarán activas.

Se puede habilitar una métrica específica cambiando el valor de `evaluation.metrics.com`. En el siguiente ejemplo, la métrica F-Score está habilitada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

En la tabla siguiente se indican las métricas predeterminadas de cada clase. Un usuario también puede utilizar los valores de la columna `evaluation.metric` para habilitar una métrica específica.

| `evaluator.class` | Medidas predeterminadas | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Precisión <br>-Características Operativas del Receptor <br>-Área Bajo las Características Operativas del Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Precisión <br>-Características Operativas del Receptor <br>-Área Bajo las Características Operativas del Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisión media promedio (MAP) <br>-Ganancia acumulativa descontada normalizada <br>-Clasificación recíproca media <br>-Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de evaluación personalizadas para Scala

El evaluador personalizado se puede proporcionar ampliando la interfaz de `MLEvaluator.scala` en el archivo `Evaluator.scala`. En el archivo [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) de ejemplo, definimos las funciones `split()` y `evaluate()` personalizadas. Nuestra función `split()` divide nuestros datos al azar con una proporción de 8:2 y nuestra función `evaluate()` define y devuelve 3 métricas: MAPE, MAE y RMSE.

>[!IMPORTANT]
>
>Para la clase `MLMetric`, no utilice `"measures"` para `valueType` al crear un nuevo `MLMetric`, de lo contrario la métrica no se rellenará en la tabla de métricas de evaluación personalizada.
>  
> Haga esto: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> No es esto: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una vez definida en la fórmula, el siguiente paso es habilitarla en las fórmulas. Esto se realiza en el archivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) de la carpeta `resources` del proyecto. Aquí el `evaluation.class` se establece en la clase `Evaluator` definida en `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

En [!DNL Data Science Workspace], el usuario podría ver las perspectivas en la ficha &quot;Métricas de evaluación&quot; en la página del experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Por ahora, no hay métricas de evaluación predeterminadas para [!DNL Python] o [!DNL Tensorflow]. Por lo tanto, para obtener las métricas de evaluación para [!DNL Python] o [!DNL Tensorflow], deberá crear una métrica de evaluación personalizada. Esto se puede hacer implementando la clase `Evaluator`.

#### Métricas de evaluación personalizadas para [!DNL Python]

Para las métricas de evaluación personalizadas, hay dos métodos principales que deben implementarse para el evaluador: `split()` y `evaluate()`.

Para [!DNL Python], estos métodos se definirían en [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para la clase `Evaluator`. Siga el vínculo [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para ver un ejemplo de `Evaluator`.

La creación de métricas de evaluación en [!DNL Python] requiere que el usuario implemente los métodos `evaluate()` y `split()`.

El método `evaluate()` devuelve el objeto de métrica que contiene una matriz de objetos de métrica con propiedades `name`, `value` y `valueType`.

El propósito del método `split()` es introducir datos y generar una capacitación y un conjunto de datos de prueba. En nuestro ejemplo, el método `split()` ingresa datos mediante el SDK `DataSetReader` y luego limpia los datos eliminando columnas no relacionadas. A partir de ahí, se crean funciones adicionales a partir de las funciones sin procesar existentes en los datos.

El método `split()` debe devolver un juego de datos de prueba y formación que luego utilizan los métodos `pipeline()` para entrenar y probar el modelo ML.

#### Métricas de evaluación personalizadas para Tensorflow

Para [!DNL Tensorflow], de manera similar a [!DNL Python], será necesario implementar los métodos `evaluate()` y `split()` en la clase `Evaluator`. Para `evaluate()`, las métricas deben devolverse mientras que `split()` devuelve los conjuntos de datos de prueba y tren.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

Por ahora, no hay métricas de evaluación predeterminadas para R. Por lo tanto, para obtener las métricas de evaluación para R, deberá definir la clase `applicationEvaluator` como parte de la fórmula.

#### Métricas de evaluación personalizadas para R

El principal propósito de `applicationEvaluator` es devolver un objeto JSON que contenga pares de métricas clave-valor.

Este [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) puede utilizarse como ejemplo. En este ejemplo, `applicationEvaluator` se divide en tres secciones conocidas:
- Cargar datos
- Preparación de datos/ingeniería de características
- Recuperar modelo guardado y evaluar

Los datos se cargan primero en un conjunto de datos desde un origen como se define en [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Desde allí, los datos se limpian y se diseñan para adaptarse al modelo de aprendizaje automático. Por último, el modelo se utiliza para hacer una predicción utilizando nuestro conjunto de datos y, a partir de los valores predichos y los valores reales, se calculan las métricas. En este caso, MAPE, MAE y RMSE se definen y devuelven en el objeto `metrics`.

## Uso de métricas y gráficos de visualización creados previamente

El [!DNL Sensei Model Insights Framework] admitirá una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático. La siguiente tabla muestra las clases comunes de algoritmos de aprendizaje automático de alto nivel y las métricas y visualizaciones de evaluación correspondientes.

| Tipo de algoritmo ML | Métricas de evaluación | Visualizaciones |
--- | --- | ---
| Regresión | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva de superposición de valores reales frente a valores previstos |
| Clasificación binaria | - Matriz de confusión<br>- Precisión-recuperación<br>- Precisión<br>- Puntuación F (específicamente F1 ,F2)<br>- AUC<br>- ROC | Curva ROC y matriz de confusión |
| Clasificación de varias clases | -Matriz de confusión <br>- Para cada clase: <br>- precisión de recuperación de precisión <br>- Puntuación F (específicamente F1, F2) | Curva ROC y matriz de confusión |
| Agrupación (con la verdad del suelo) | - NMI (puntuación de información mutua normalizada), AMI (puntuación de información mutua ajustada)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- puntuación de homogeneidad, puntuación de integridad y variable-medida<br>- FMI (índice Fowlkes-Mallow)<br>- Pureza<br>- Índice Jaccard | Diagrama de clústeres que muestra clústeres y centroides con tamaños de clúster relativos que reflejan los puntos de datos que se incluyen dentro del clúster |
| Agrupación (sin la verdad del suelo) | - Inercia<br>- Coeficiente de silueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice de Dunn | Diagrama de clústeres que muestra clústeres y centroides con tamaños de clúster relativos que reflejan los puntos de datos que se incluyen dentro del clúster |
| Recomendación | -Precisión media promedio (MAP) <br>-Ganancia acumulativa descontada normalizada <br>-Clasificación recíproca media <br>-Métrica K | Por determinar |
| Casos de uso de TensorFlow | Análisis del modelo TensorFlow (TFMA) | Comparación/visualización del modelo de red neural en profundidad |
| Otro/mecanismo de captura de errores | Lógica de métrica personalizada (y los correspondientes gráficos de evaluación) definida por el autor del modelo. Gestión de errores correcta en caso de que la plantilla no coincida | Tabla con pares de valor clave para métricas de evaluación |
