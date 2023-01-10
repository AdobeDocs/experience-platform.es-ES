---
keywords: Experience Platform;optimizar;modelo;Data Science Workspace;temas populares;perspectivas de modelo
solution: Experience Platform
title: Optimización de un modelo mediante el marco de perspectivas del modelo
type: Tutorial
description: El marco de Model Insights proporciona al científico de datos herramientas en Data Science Workspace para tomar decisiones rápidas e informadas para modelos óptimos de aprendizaje automático basados en experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Optimizar un modelo mediante el marco de información del modelo

El marco de perspectivas de modelo proporciona al científico de datos las herramientas indicadas en [!DNL Data Science Workspace] para tomar decisiones rápidas e informadas para lograr modelos óptimos de aprendizaje automático basados en experimentos. El marco mejorará la velocidad y la eficacia del flujo de trabajo de aprendizaje automático, así como la facilidad de uso de los científicos de datos. Esto se hace proporcionando una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático para ayudar con el ajuste del modelo. El resultado final permite a los científicos de datos y a los científicos de datos ciudadanos tomar mejores decisiones de optimización de modelos para sus clientes finales.

## ¿Qué son las métricas?

Después de implementar y entrenar un modelo, el siguiente paso que haría un científico de datos es encontrar el desempeño del modelo. Se utilizan varias métricas para determinar la eficacia de un modelo en comparación con otros. Algunos ejemplos de métricas utilizadas son:
- Precisión de la clasificación
- Área bajo curva
- Matriz de confusión
- Informe de clasificación

## Configuración del código de fórmula

Actualmente, Model Insights Framework es compatible con los siguientes tiempos de ejecución:
- [Scala](#scala)
- [Pithon/Tensorflow](#pythontensorflow)
- [R](#r)

Puede encontrar el código de muestra de las fórmulas en la [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) repositorio bajo `recipes`. Se hará referencia a archivos específicos de este repositorio a lo largo de este tutorial.

### Scala {#scala}

Existen dos maneras de incorporar métricas a las fórmulas. Una es utilizar las métricas de evaluación predeterminadas proporcionadas por el SDK y la otra es escribir métricas de evaluación personalizadas.

#### Métricas de evaluación predeterminadas para Scala

Las evaluaciones predeterminadas se calculan como parte de los algoritmos de clasificación. Estos son algunos valores predeterminados para los evaluadores que están implementados actualmente:

| Clase de evaluador | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| Evaluador de recomendaciones | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

El evaluador se puede definir en la fórmula de la [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) en el `recipe` carpeta. Código de ejemplo que habilita la variable `DefaultBinaryClassificationEvaluator` se muestra a continuación:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Una vez habilitada una clase de evaluador, se calcularán varias métricas durante la formación de forma predeterminada. Las métricas predeterminadas se pueden declarar explícitamente agregando la línea siguiente al `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Si no se define la métrica, se activarán las métricas predeterminadas.

Se puede habilitar una métrica específica cambiando el valor de `evaluation.metrics.com`. En el siguiente ejemplo, la métrica F-Score está activada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

En la tabla siguiente se indican las métricas predeterminadas de cada clase. Un usuario también puede utilizar los valores de la variable `evaluation.metric` para habilitar una métrica específica.

| `evaluator.class` | Métricas predeterminadas | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precisión <br>-Recordar <br>-Matriz de confusión <br>-F-Score <br>-Precisión <br>-Características operativas del receptor <br>-Área bajo las características operativas del receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precisión <br>-Recordar <br>-Matriz de confusión <br>-F-Score <br>-Precisión <br>-Características operativas del receptor <br>-Área bajo las características operativas del receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Precisión media (MAP) <br>-Ganancia acumulada descontada normalizada <br>-Clasificación recíproca media <br>-Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de evaluación personalizadas para Scala

El evaluador personalizado se puede proporcionar ampliando la interfaz de `MLEvaluator.scala` en su `Evaluator.scala` archivo. En el ejemplo [Evaluator.escala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) , definimos `split()` y `evaluate()` funciones. Nuestra `split()` divide nuestros datos aleatoriamente con una proporción de 8:2 y nuestra `evaluate()` define y devuelve 3 métricas: MAPE, MAE y RMSE.

>[!IMPORTANT]
>
>Para la variable `MLMetric` clase, no use `"measures"` para `valueType` al crear un `MLMetric` de lo contrario, la métrica no se rellenará en la tabla de métricas de evaluación personalizada.
>  
> Haga esto: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> No esto: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una vez definida en la fórmula, el siguiente paso es habilitarla en las fórmulas. Esto se hace en la variable [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) en el `resources` carpeta. Aquí puede consultar la `evaluation.class` se configura como `Evaluator` clase definida en `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

En el [!DNL Data Science Workspace], el usuario podría ver las perspectivas en la pestaña &quot;Métricas de evaluación&quot; de la página del experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

A partir de ahora, no hay métricas de evaluación predeterminadas para [!DNL Python] o [!DNL Tensorflow]. Por lo tanto, para obtener las métricas de evaluación de [!DNL Python] o [!DNL Tensorflow], deberá crear una métrica de evaluación personalizada. Esto se puede hacer implementando la variable `Evaluator` Clase .

#### Métricas de evaluación personalizadas para [!DNL Python]

Para las métricas de evaluación personalizadas, hay dos métodos principales que deben implementarse para el evaluador: `split()` y `evaluate()`.

Para [!DNL Python], estos métodos se definirían en [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para el `Evaluator` Clase . Siga las [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para ver un ejemplo de la variable `Evaluator`.

Creación de métricas de evaluación en [!DNL Python] requiere que el usuario implemente el `evaluate()` y `split()` métodos.

La variable `evaluate()` devuelve el objeto de métrica que contiene una matriz de objetos de métrica con propiedades de `name`, `value`y `valueType`.

El propósito del `split()` es introducir datos y generar una formación y un conjunto de datos de prueba. En nuestro ejemplo, la variable `split()` método de entrada de datos mediante `DataSetReader` SDK y, a continuación, limpia los datos eliminando columnas no relacionadas. A partir de ahí, se crean funciones adicionales a partir de funciones sin procesar existentes en los datos.

La variable `split()` El método debe devolver un datafame de formación y prueba que luego use el `pipeline()` métodos para entrenar y probar el modelo ML.

#### Métricas de evaluación personalizadas para Tensorflow

Para [!DNL Tensorflow], similar a [!DNL Python], los métodos `evaluate()` y `split()` en el `Evaluator` deberá implementarse la clase . Para `evaluate()`, las métricas deben devolverse mientras `split()` devuelve los conjuntos de datos de tren y prueba.

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

A partir de ahora, no hay métricas de evaluación predeterminadas para R. Por lo tanto, para obtener las métricas de evaluación para R, debe definir la variable `applicationEvaluator` como parte de la fórmula.

#### Métricas de evaluación personalizadas para R

El objetivo principal del `applicationEvaluator` es devolver un objeto JSON que contenga pares de métricas clave-valor.

Esta [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) se puede usar como ejemplo. En este ejemplo, la variable `applicationEvaluator` se divide en tres secciones conocidas:
- Carga de datos
- Preparación de datos/ingeniería de características
- Recuperar modelo guardado y evaluar

Los datos se cargan primero en un conjunto de datos desde un origen como se define en [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir de ahí, los datos se limpian y se diseñan para ajustarse al modelo de aprendizaje automático. Por último, el modelo se utiliza para hacer una predicción utilizando nuestro conjunto de datos y a partir de los valores predichos y los valores reales, las métricas se calculan. En este caso, MAPE, MAE y RMSE se definen y devuelven en la variable `metrics` objeto.

## Uso de métricas prediseñadas y gráficos de visualización

La variable [!DNL Sensei Model Insights Framework] admitirá una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático. La siguiente tabla muestra clases comunes de algoritmos de aprendizaje automático de alto nivel y las métricas y visualizaciones de evaluación correspondientes.

| Tipo de algoritmo ML | Métricas de evaluación | Visualizaciones |
| --- | --- | --- |
| Regresión | - RMSE<br>- MAPA<br>- MASA<br>- MAE | Curva de superposición de valores reales y predichos |
| Clasificación binaria | - Matriz de confusión<br>- Recuperación de precisión<br>- Precisión<br>- F-score (específicamente F1 ,F2)<br>- AUC<br>- ROC | Curva ROC y matriz de confusión |
| Clasificación de varias clases | -Matriz de confusión <br>- Para cada clase: <br>- precisión de recuperación de precisión <br>- F-score (específicamente F1, F2) | Curva ROC y matriz de confusión |
| Clustering (con verdad de tierra) | - NMI (puntuación de información mutua normalizada), AMI (puntuación de información mutua ajustada)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- puntuación de homogeneidad, puntuación de integridad y medición de V<br>- FMI (índice Fowlkes-Mallow)<br>- Pureza<br>- Índice Jaccard | Diagrama de clústeres que muestra clústeres y centroides con tamaños de clúster relativos que reflejan los puntos de datos incluidos en el clúster |
| Clustering (sin verdad de tierra) | - Inercia<br>- Coeficiente de silueta<br>- CHI (Índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice Dunn | Diagrama de clústeres que muestra clústeres y centroides con tamaños de clúster relativos que reflejan los puntos de datos incluidos en el clúster |
| Recomendación | -Precisión media (MAP) <br>-Ganancia acumulada descontada normalizada <br>-Clasificación recíproca media <br>-Métrica K | Por determinar |
| Casos de uso de TensorFlow | Análisis del modelo TensorFlow (TFMA) | Comparación/visualización del modelo de red neural en comparación profunda |
| Otro/mecanismo de captura de error | Lógica de métrica personalizada (y los gráficos de evaluación correspondientes) definida por el autor del modelo. Gestión correcta de errores en caso de que la plantilla no coincida | Tabla con pares de clave-valor para métricas de evaluación |
