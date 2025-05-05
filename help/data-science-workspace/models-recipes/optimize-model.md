---
keywords: Experience Platform; optimizar; modelo; Data Science Espacio de trabajo; temas populares; Perspectivas del modelo
solution: Experience Platform
title: Optimización de un modelo mediante el marco de Insights de modelos
type: Tutorial
description: El marco de datos de Model Insights proporciona al científico de datos las herramientas de Data Science Workspace para tomar decisiones rápidas e informadas sobre modelos óptimos de aprendizaje automático basados en experimentos.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---

# Optimizar un modelo con el marco de trabajo de perspectivas del modelo

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

El Marco de datos de perspectivas del modelo proporciona al científico de datos las herramientas de [!DNL Data Science Workspace] para tomar decisiones rápidas e informadas con el fin de obtener modelos óptimos de aprendizaje automático basados en experimentos. El marco mejorará la velocidad y la eficacia del flujo de trabajo de aprendizaje automático, así como la facilidad de uso de los científicos de datos. Para ello, proporcione una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático que le ayude a ajustar el modelo. El resultado final permite a los científicos de datos y científicos de datos ciudadanos tomar mejores decisiones de optimización de modelos para sus clientes finales.

## ¿Qué son las métricas?

Después de implementar y aprendizaje un modelo, el siguiente paso que haría un científico de datos es encontrar qué tan bien funcionará el modelo. Se utilizan varias métricas para encontrar la eficacia de un modelo en comparación con otros. Algunos ejemplos de métricas utilizadas incluyen:
- Precisión de clasificación
- Área bajo curva
- Matriz de confusión
- Informe de clasificación

## Configuración del código de fórmula

Actualmente, Model Insights Framework admite los siguientes tiempos de ejecución:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

Se puede encontrar código de muestra para fórmulas en el repositorio [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) en `recipes`. Se hará referencia a archivos específicos de este repositorio a través de este tutorial.

### Scala {#scala}

Existen dos formas de añadir métricas a las recetas. Una es utilizar las métricas de evaluación predeterminadas proporcionadas por el SDK y la otra es escribir métricas de evaluación personalizadas.

#### Métricas de evaluación predeterminadas para Scala

Las evaluaciones predeterminadas se calculan como parte de los algoritmos clasificación. Estos son algunos de los valores predeterminados para los evaluadores que están implementados actualmente:

| Clase de evaluador | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

El evaluador se puede definir en el fórmula en el [archivo aplicación.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) de la `recipe` carpeta. A continuación se muestra un código de ejemplo que activa la `DefaultBinaryClassificationEvaluator` opción:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Después de habilitar una clase de evaluador, se calculará un número de métricas durante el aprendizaje de forma predeterminada. Las métricas predeterminadas se pueden declarar explícitamente añadiendo la línea siguiente a su `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Si la Métrica no está definida, las métricas predeterminadas se activan.

Se puede activar un Métrica específico cambiando el valor `evaluation.metrics.com`de . En el ejemplo siguiente, la Métrica Puntuación F está activada.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

La siguiente tabla indica las métricas predeterminadas para cada clase. Un usuario también puede utilizar los valores de la `evaluation.metric` columna para activar un Métrica específico.

| `evaluator.class` | Métricas predeterminadas | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precisión <br>-Recall <br>-Matriz <br>de confusión -F-Score <br>-Precisión <br>-Características <br>operativas del receptor -Área debajo de las características operativas del receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>- -`ROC` <br>`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precisión <br>-Recall <br>-Matriz <br>de confusión -F-Score <br>-Precisión <br>-Características <br>operativas del receptor -Área debajo de las características operativas del receptor | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>- -`ROC` <br>`AUROC` |
| `RecommendationsEvaluator` | -Precisión media media (MAP) <br>-Ganancia <br>acumulada descontada normalizada -Clasificación <br>recíproca media -Métrica K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Métricas de evaluación personalizadas para Scala

El evaluador personalizado se puede proporcionar ampliando la interfaz de `MLEvaluator.scala` en su `Evaluator.scala` archivo. En el archivo Evaluator.scala de ejemplo[, definimos la personalización `split()` y `evaluate()` las](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) funciones. Nuestra `split()` función divide nuestros datos aleatoriamente con una proporción de 8: 2 y nuestra `evaluate()` función define y devuelve 3 métricas: MAPE, MAE y RMSE.

>[!IMPORTANT]
>
>Para la `MLMetric` clase, no use `"measures"` para `valueType` cuando cree una nueva `MLMetric` otra cosa, la Métrica no se rellenará en la tabla de métricas de evaluación personalizada.
>  
> Haga lo siguiente: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> No esto: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Una vez definido en el fórmula, el siguiente paso es habilitarlo en las fórmulas. Esto se realiza en el [archivo aplicación.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) de la carpeta del `resources` proyecto. Aquí el `evaluation.class` se establece en la `Evaluator` clase definida en `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

En el [!DNL Data Science Workspace], el usuario podría ver las perspectivas en las &quot;Métricas de evaluación&quot; pestaña en el Página del experimento.

### [!DNL Python/Tensorflow] {#pythontensorflow}

A partir de ahora, no hay métricas de evaluación predeterminadas para [!DNL Python] o [!DNL Tensorflow]. Por lo tanto, para obtener las métricas de evaluación para [!DNL Python] o [!DNL Tensorflow], deberá crear un Métrica de evaluación personalizado. Esto se puede hacer implementando la `Evaluator` clase.

#### Métricas de evaluación personalizadas para [!DNL Python]

Para las métricas de evaluación personalizadas, existen dos métodos principales que deben implementarse para el evaluador: `split()` y `evaluate()`.

Para [!DNL Python], estos métodos se definirían en [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para la `Evaluator` clase. Siga la vincular de evaluator.py [&#128279;](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) para ver un ejemplo del `Evaluator`archivo .

La creación de métricas de evaluación requiere [!DNL Python] que el usuario implementar los `evaluate()` métodos and `split()` .

El `evaluate()` método devuelve el objeto Métrica que contiene una matriz de objetos Métrica con propiedades de `name`, `value`, y `valueType`.

El objetivo del `split()` método es introducir datos y generar un aprendizaje y un conjunto de datos de prueba. En nuestro ejemplo, el `split()` método introduce datos mediante el `DataSetReader` SDK y, a continuación, limpia los datos eliminando columnas no relacionadas. A partir de ahí, se crean funciones adicionales a partir de las funciones sin procesar existentes en los datos.

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

A partir de ahora, no hay ninguna métrica de evaluación predeterminada para R. Por lo tanto, para obtener las métricas de evaluación para R, deberá definir la `applicationEvaluator` clase como parte del fórmula.

#### Métricas de evaluación personalizadas para R

El objetivo principal de la `applicationEvaluator` es devolver un objeto JSON que contenga pares de métricas clave-valor.

Esta [aplicación Evaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) se puede utilizar como ejemplo. En este ejemplo, `applicationEvaluator` se divide en tres secciones familiares:
- Carga de datos
- Preparación de datos/ingeniería de funciones
- Recuperar modelo guardado y evaluar

Los datos se cargan primero en un conjunto de datos desde un origen tal como se define en [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir de ahí, los datos se limpian y se diseñan para adaptarse al modelo de aprendizaje automático. Por último, el modelo se utiliza para hacer una predicción con nuestro conjunto de datos y a partir de los valores predichos y los valores reales, se calculan las métricas. En este caso, MAPE, MAE y RMSE se definen y se devuelven en el `metrics` objeto.

## Uso de métricas de creado previamente y gráficos de visualización

[!DNL Sensei Model Insights Framework] admitirá una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático. La tabla siguiente muestra las clases de algoritmos comunes de aprendizaje automático de alto nivel y las métricas y visualizaciones de evaluación correspondientes.

| Tipo de algoritmo XML | Métricas de evaluación | Visualizaciones |
| --- | --- | --- |
| Regresión | - RMSE<br>- MAPE-<br> MASE<br>- MAE | Valores predichos frente a valores reales superposición curva |
| binario clasificación | - Matriz<br> de confusión- Precisión-recuperación<br>- Exactitud<br>- F-score (específicamente F1 ,F2)<br>- AUC<br>- ROC | Curva ROC y matriz de confusión |
| clasificación multiclase | -Matriz <br>de confusión - Para cada clase: <br>- precisión-exactitud <br>de recuerdo - F-score (específicamente F1, F2) | Curva ROC y matriz de confusión |
| Clúster (con verdad de tierra) | - NMI (puntuación de información mutua normalizada), AMI (puntuación de información mutua ajustada)<br>- RI (índice Rand), ARI (índice Rand ajustado)<br>- puntuación de homogeneidad, puntuación de integridad, y V-measure<br>- FMI (índice Fowlkes-Mallow)<br>- Pureza<br>- índice Jaccard | El gráfico de clústeres muestra clústeres y centroides con tamaños de clúster relativos que reflejan puntos de datos que se encuentran dentro del clúster |
| Clúster (sin verdad de masa) | - Inercia<br>- Coeficiente de silueta<br>- CHI (índice Calinski-Harabaz)<br>- DBI (índice Davies-Bouldin)<br>- Índice Dunn | El gráfico de clústeres muestra clústeres y centroides con tamaños de clúster relativos que reflejan puntos de datos que se encuentran dentro del clúster |
| Recomendación | -Media de precisión media (MAP) <br>-Ganancia acumulativa descontada normalizada <br>-Media de clasificación recíproca <br>-Métrica K | Por determinar |
| Casos de uso de TensorFlow | Análisis del modelo TensorFlow (TFMA) | Deepcompare la comparación/visualización del modelo de redes neuronales |
| Otro/mecanismo de captura de errores | Lógica de Métrica personalizada (y los gráficos de evaluación correspondientes) definida por el autor del modelo. Gestión correcta de errores en caso de que plantilla discrepancia | Tabla con pares clave-valor para las métricas de evaluación |
