---
keywords: Experience Platform;optimizar;modelo;Workspace de ciencia de datos;temas populares;perspectivas del modelo
solution: Experience Platform
title: Optimización de un modelo mediante el marco de datos de modelo
type: Tutorial
description: El marco de datos de Model Insights proporciona al científico de datos las herramientas de Data Science Workspace para tomar decisiones rápidas e informadas sobre modelos óptimos de aprendizaje automático basados en experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Optimizar un modelo con el marco de trabajo de perspectivas del modelo

El Marco de datos de perspectivas del modelo proporciona al científico de datos las herramientas de [!DNL Data Science Workspace] para tomar decisiones rápidas e informadas con el fin de obtener modelos óptimos de aprendizaje automático basados en experimentos. El marco mejorará la velocidad y la eficacia del flujo de trabajo de aprendizaje automático, así como la facilidad de uso de los científicos de datos. Para ello, proporcione una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático que le ayude a ajustar el modelo. El resultado final permite a los científicos de datos y a los científicos de datos ciudadanos tomar mejores decisiones de optimización de modelos para sus clientes finales.

## ¿Qué son las métricas?

Después de implementar y entrenar un modelo, el siguiente paso que un científico de datos haría es encontrar el rendimiento del modelo. Se utilizan varias métricas para encontrar la eficacia que tendrá un modelo en comparación con otros. Algunos ejemplos de métricas utilizadas son:
- Precisión de clasificación
- Área bajo curva
- Matriz de confusión
- Informe de clasificación

## Configuración del código de fórmula

Actualmente, el módulo de información del modelo admite los siguientes tiempos de ejecución:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

Se puede encontrar código de muestra para fórmulas en el repositorio [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) en `recipes`. Se hará referencia a archivos específicos de este repositorio a través de este tutorial.

### Scala {#scala}

Existen dos formas de añadir métricas a las recetas. Una es utilizar las métricas de evaluación predeterminadas proporcionadas por el SDK y la otra es escribir métricas de evaluación personalizadas.

#### Métricas de evaluación predeterminadas para Scala

Las evaluaciones predeterminadas se calculan como parte de los algoritmos de clasificación. Estos son algunos valores predeterminados para los evaluadores que están implementados actualmente:

| Clase de evaluador | `evaluation.class` |
|--- | ---|
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

Una vez habilitada una clase de evaluador, se calcularán varias métricas durante la formación de forma predeterminada. Las métricas predeterminadas se pueden declarar explícitamente agregando la línea siguiente a su `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Si la métrica no está definida, las métricas predeterminadas estarán activas.

Se puede habilitar una métrica específica cambiando el valor de `evaluation.metrics.com`. En el ejemplo siguiente, la métrica de puntuación F está habilitada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

En la tabla siguiente se muestran las métricas predeterminadas de cada clase. Un usuario también puede usar los valores de la columna `evaluation.metric` para habilitar una métrica específica.

| `evaluator.class` | Métricas predeterminadas | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precisión <br>-Recuperar <br>-Matriz de confusión <br>-Puntuación F <br>-Precisión <br>-Características operativas del receptor <br>-Área bajo las características operativas del receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precisión <br>-Recuperar <br>-Matriz de confusión <br>-Puntuación F <br>-Precisión <br>-Características operativas del receptor <br>-Área bajo las características operativas del receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Media de precisión media (MAP) <br>-Ganancia acumulativa descontada normalizada <br>-Media de clasificación recíproca <br>-Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de evaluación personalizadas para Scala

Se puede proporcionar el evaluador personalizado ampliando la interfaz de `MLEvaluator.scala` en el archivo `Evaluator.scala`. En el archivo [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) de ejemplo, definimos las funciones `split()` y `evaluate()` personalizadas. Nuestra función `split()` divide nuestros datos aleatoriamente con una relación de 8:2 y nuestra función `evaluate()` define y devuelve 3 métricas: MAPE, MAE y RMSE.

>[!IMPORTANT]
>
>Para la clase `MLMetric`, no use `"measures"` para `valueType` al crear un nuevo `MLMetric`; de lo contrario, la métrica no se rellenará en la tabla de métricas de evaluación personalizadas.
>  
> Haga esto: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> No es esto: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una vez definida en la fórmula, el siguiente paso es habilitarla en las fórmulas. Esto se hace en el archivo [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) de la carpeta `resources` del proyecto. Aquí `evaluation.class` está establecido en la clase `Evaluator` definida en `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

En [!DNL Data Science Workspace], el usuario podría ver las perspectivas en la pestaña &quot;Métricas de evaluación&quot; en la página del experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Por ahora, no hay métricas de evaluación predeterminadas para [!DNL Python] o [!DNL Tensorflow]. Por lo tanto, para obtener las métricas de evaluación de [!DNL Python] o [!DNL Tensorflow], deberá crear una métrica de evaluación personalizada. Esto se puede hacer implementando la clase `Evaluator`.

#### Métricas de evaluación personalizadas para [!DNL Python]

Para las métricas de evaluación personalizadas, hay dos métodos principales que deben implementarse para el evaluador: `split()` y `evaluate()`.

Para [!DNL Python], estos métodos se definirían en [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para la clase `Evaluator`. Siga el vínculo [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para ver un ejemplo de `Evaluator`.

La creación de métricas de evaluación en [!DNL Python] requiere que el usuario implemente los métodos `evaluate()` y `split()`.

El método `evaluate()` devuelve el objeto de métrica que contiene una matriz de objetos de métrica con propiedades de `name`, `value` y `valueType`.

El propósito del método `split()` es introducir datos y generar un conjunto de datos de prueba y aprendizaje. En nuestro ejemplo, el método `split()` introduce datos mediante el SDK `DataSetReader` y, a continuación, limpia los datos eliminando columnas no relacionadas. A partir de ahí, se crean funciones adicionales a partir de las funciones sin procesar existentes en los datos.

El método `split()` debe devolver un marco de datos de prueba y aprendizaje que luego utilizan los métodos `pipeline()` para entrenar y probar el modelo XML.

#### Métricas de evaluación personalizadas para Tensorflow

Para [!DNL Tensorflow], similar a [!DNL Python], será necesario implementar los métodos `evaluate()` y `split()` en la clase `Evaluator`. Para `evaluate()`, se deben devolver las métricas mientras `split()` devuelve los conjuntos de datos de prueba y tren.

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

El propósito principal de `applicationEvaluator` es devolver un objeto JSON que contiene pares de métricas clave-valor.

Este [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) se puede usar como ejemplo. En este ejemplo, `applicationEvaluator` se divide en tres secciones familiares:
- Carga de datos
- Preparación de datos/ingeniería de funciones
- Recuperar modelo guardado y evaluar

Los datos se cargan primero en un conjunto de datos desde un origen tal como se define en [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir de ahí, los datos se limpian y se diseñan para adaptarse al modelo de aprendizaje automático. Por último, el modelo se utiliza para hacer una predicción con nuestro conjunto de datos y a partir de los valores predichos y los valores reales, se calculan las métricas. En este caso, MAPE, MAE y RMSE se definen y devuelven en el objeto `metrics`.

## Uso de métricas creadas previamente y gráficos de visualización

[!DNL Sensei Model Insights Framework] admitirá una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático. La tabla siguiente muestra las clases de algoritmos comunes de aprendizaje automático de alto nivel y las métricas y visualizaciones de evaluación correspondientes.

| Tipo de algoritmo XML | Métricas de evaluación | Visualizaciones |
| --- | --- | --- |
| Regresión | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Curva de superposición de valores predichos frente a reales |
| Clasificación binaria | - Matriz de confusión<br>- Recuperación de precisión<br>- Precisión<br>- Puntuación F (específicamente F1 ,F2)<br>- AUC<br>- ROC | Curva ROC y matriz de confusión |
| Clasificación de varias clases | -Matriz de confusión <br>- Para cada clase: <br>- precisión de recuperación <br>- puntuación F (específicamente F1, F2) | Curva ROC y matriz de confusión |
| Clúster (con verdad de tierra) | - NMI (puntuación de información mutua normalizada), AMI (puntuación de información mutua ajustada)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- puntuación de homogeneidad, puntuación de integridad, y V-measure<br>- FMI (índice Fowlkes-Mallow)<br>- Pureza<br>- índice Jaccard | El gráfico de clústeres muestra clústeres y centroides con tamaños de clúster relativos que reflejan puntos de datos que se encuentran dentro del clúster |
| Clúster (sin verdad de masa) | - Inercia<br>- Coeficiente de silueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice Dunn | El gráfico de clústeres muestra clústeres y centroides con tamaños de clúster relativos que reflejan puntos de datos que se encuentran dentro del clúster |
| Recomendación | -Media de precisión media (MAP) <br>-Ganancia acumulativa descontada normalizada <br>-Media de clasificación recíproca <br>-Métrica K | Por determinar |
| Casos de uso de TensorFlow | Análisis del modelo TensorFlow (TFMA) | Comparación/visualización del modelo de red neuronal de comparación profunda |
| Otro mecanismo de captura/error | Lógica de métrica personalizada (y gráficos de evaluación correspondientes) definida por el autor del modelo. Gestión correcta de errores en caso de que la plantilla no coincida | Tabla con pares de clave-valor para métricas de evaluación |
