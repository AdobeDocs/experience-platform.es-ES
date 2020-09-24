---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics;model insights
solution: Experience Platform
title: Optimizar un modelo
topic: tutorial
type: Tutorial
description: El marco de perspectivas de modelo proporciona al científico de datos herramientas en el área de trabajo de ciencias de datos para realizar elecciones rápidas e informadas para modelos óptimos de aprendizaje automático basados en experimentos.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---


# Optimizar un modelo mediante el marco de perspectivas de modelo

El marco de perspectivas del modelo proporciona al científico de datos herramientas para [!DNL Data Science Workspace] realizar elecciones rápidas e informadas para modelos óptimos de aprendizaje automático basados en experimentos. El marco mejorará la velocidad y la eficacia del flujo de trabajo del aprendizaje automático, así como la facilidad de uso de los científicos de datos. Esto se lleva a cabo proporcionando una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático para facilitar el ajuste del modelo. El resultado final permite a los científicos de datos y a los científicos de datos ciudadanos tomar mejores decisiones de optimización de modelos para sus clientes finales.

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

El código de muestra de las fórmulas se encuentra en el repositorio [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) , en `recipes`. En este tutorial se hará referencia a archivos específicos de este repositorio.

### Scala {#scala}

Existen dos maneras de incorporar métricas a las fórmulas. Una es utilizar las métricas de evaluación predeterminadas proporcionadas por el SDK y la otra es escribir métricas de evaluación personalizadas.

#### Métricas de evaluación predeterminadas para Scala

Las evaluaciones predeterminadas se calculan como parte de los algoritmos de clasificación. Estos son algunos valores predeterminados para los evaluadores que están implementados actualmente:

| Clase de evaluador | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

El evaluador se puede definir en la fórmula del archivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) de la `recipe` carpeta. A continuación se muestra el código de muestra que habilita `DefaultBinaryClassificationEvaluator` el

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

En la tabla siguiente se indican las métricas predeterminadas de cada clase. Un usuario también puede utilizar los valores de la `evaluation.metric` columna para habilitar una métrica específica.

| `evaluator.class` | Medidas predeterminadas | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall- <br>-Confusión Matriz <br>-F-Puntuación <br>-Precisión <br>-Características de funcionamiento <br>del receptor-Área bajo las Características de Funcionamiento del Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall- <br>-Confusión Matriz <br>-F-Puntuación <br>-Precisión <br>-Características de funcionamiento <br>del receptor-Área bajo las Características de Funcionamiento del Receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisión media promedio (MAP) <br>-Ganancia acumulativa <br>media descontada normalizada-Clasificación recíproca <br>métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de evaluación personalizadas para Scala

El evaluador personalizado se puede proporcionar ampliando la interfaz de `MLEvaluator.scala` en el `Evaluator.scala` archivo. En el archivo [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) de ejemplo, definimos las funciones personalizadas `split()` y `evaluate()` . Nuestra `split()` función divide nuestros datos al azar con una proporción de 8:2 y nuestra `evaluate()` función define y devuelve 3 métricas: MAPE, MAE y RMSE.

>[!IMPORTANT]
>
>Para la `MLMetric` clase, no utilice `"measures"` para `valueType` crear otro `MLMetric` elemento, la métrica no se rellenará en la tabla de métricas de evaluación personalizada.
>  
> Haga esto: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> No es esto: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una vez definida en la fórmula, el siguiente paso es habilitarla en las fórmulas. Esto se realiza en el archivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) de la `resources` carpeta del proyecto. Aquí el `evaluation.class` se establece en la `Evaluator` clase definida en `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

En la página [!DNL Data Science Workspace], el usuario podrá ver las perspectivas en la ficha &quot;Métricas de evaluación&quot; de la página del experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Por ahora, no hay métricas de evaluación predeterminadas para [!DNL Python] o [!DNL Tensorflow]. Por lo tanto, para obtener las métricas de evaluación para [!DNL Python] o [!DNL Tensorflow], deberá crear una métrica de evaluación personalizada. Esto se puede hacer implementando la `Evaluator` clase.

#### Métricas de evaluación personalizadas para [!DNL Python]

Para las métricas de evaluación personalizadas, hay dos métodos principales que deben implementarse para el evaluador: `split()` y `evaluate()`.

Por [!DNL Python], estos métodos se definirían en [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para la `Evaluator` clase. Siga el vínculo [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para ver un ejemplo del `Evaluator`.

La creación de métricas de evaluación en [!DNL Python] requiere que el usuario implemente los `evaluate()` métodos y `split()` .

El `evaluate()` método devuelve el objeto de métrica que contiene una matriz de objetos de métrica con propiedades de `name`, `value`y `valueType`.

El propósito del `split()` método es introducir datos y generar una formación y un conjunto de datos de prueba. En nuestro ejemplo, el `split()` método introduce datos mediante el `DataSetReader` SDK y, a continuación, los limpia eliminando columnas no relacionadas. A partir de ahí, se crean funciones adicionales a partir de las funciones sin procesar existentes en los datos.

El `split()` método debe devolver un datafame de formación y ensayo que se utiliza a continuación por los `pipeline()` métodos de formación y ensayo del modelo ML.

#### Métricas de evaluación personalizadas para Tensorflow

Para [!DNL Tensorflow], de manera similar a [!DNL Python], será necesario implementar los métodos `evaluate()` y `split()` en la `Evaluator` clase. Por `evaluate()`, las métricas deben devolverse mientras `split()` devuelve los conjuntos de datos de prueba y tren.

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

Por ahora, no hay métricas de evaluación predeterminadas para R. Por lo tanto, para obtener las métricas de evaluación para R, deberá definir la `applicationEvaluator` clase como parte de la fórmula.

#### Métricas de evaluación personalizadas para R

El propósito principal del `applicationEvaluator` es devolver un objeto JSON que contenga pares de métricas clave-valor.

Se puede usar [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) como ejemplo. En este ejemplo, el `applicationEvaluator` se divide en tres secciones conocidas:
- Cargar datos
- Preparación de datos/ingeniería de características
- Recuperar modelo guardado y evaluar

Los datos se cargan primero en un conjunto de datos desde un origen como se define en [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Desde allí, los datos se limpian y se diseñan para adaptarse al modelo de aprendizaje automático. Por último, el modelo se utiliza para hacer una predicción utilizando nuestro conjunto de datos y, a partir de los valores predichos y los valores reales, se calculan las métricas. En este caso, MAPE, MAE y RMSE se definen y devuelven en el `metrics` objeto.

## Uso de métricas y gráficos de visualización creados previamente

La plantilla [!DNL Sensei Model Insights Framework] admitirá una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático. La siguiente tabla muestra las clases comunes de algoritmos de aprendizaje automático de alto nivel y las métricas y visualizaciones de evaluación correspondientes.

| Tipo de algoritmo ML | Métricas de evaluación | Visualizaciones |
--- | --- | ---
| Regresión | - RMSE<br>- MAPE<br>- MASA<br>- MAE | Curva de superposición de valores reales frente a valores previstos |
| Clasificación binaria | - Tabla<br>de confusión- Precisión-recuperación<br>- Precisión<br>- F-score (específicamente F1,F2)<br>- AUC<br>- ROC | Curva ROC y matriz de confusión |
| Clasificación de varias clases | -Matriz de confusión <br>- Para cada clase: <br>- precisión-recuperación <br>- F-score (específicamente F1, F2) | Curva ROC y matriz de confusión |
| Agrupación (con la verdad del suelo) | - NMI (puntuación de información mutua normalizada), AMI (puntuación de información mutua ajustada)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- puntuación de homogeneidad, puntuación de integridad y medida<br>V- FMI (índice Fowlkes-Mallow)<br>- Índice de pureza<br>- Jaccard | Diagrama de clústeres que muestra clústeres y centroides con tamaños de clúster relativos que reflejan los puntos de datos que se incluyen dentro del clúster |
| Agrupación (sin la verdad del suelo) | - Inercia<br>- Coeficiente<br>de silueta- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice de Dunn | Diagrama de clústeres que muestra clústeres y centroides con tamaños de clúster relativos que reflejan los puntos de datos que se incluyen dentro del clúster |
| Recomendación | -Precisión media promedio (MAP) <br>-Ganancia acumulativa <br>media descontada normalizada-Clasificación recíproca <br>métrica K | Por determinar |
| Casos de uso de TensorFlow | Análisis del modelo TensorFlow (TFMA) | Comparación/visualización del modelo de red neural en profundidad |
| Otro/mecanismo de captura de errores | Lógica de métrica personalizada (y los correspondientes gráficos de evaluación) definida por el autor del modelo. Gestión de errores correcta en caso de que la plantilla no coincida | Tabla con pares de valor clave para métricas de evaluación |
