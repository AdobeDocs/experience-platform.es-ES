---
title: Algoritmos de clasificación
description: Aprenda a configurar y optimizar varios algoritmos de clasificación con parámetros clave, descripciones y códigos de ejemplo para ayudarle a implementar modelos estadísticos avanzados.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 3%

---

# Algoritmos de clasificación {#classification-algorithms}

Este documento proporciona una visión general de varios algoritmos de clasificación, centrándose en su configuración, parámetros clave y uso práctico en modelos estadísticos avanzados. Los algoritmos de clasificación se utilizan para asignar categorías a puntos de datos en función de las funciones de entrada. Cada sección incluye descripciones de parámetros y código de ejemplo para ayudarle a implementar y optimizar estos algoritmos para tareas como árboles de decisión, bosques aleatorios y clasificaciones nativas de Bayes.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] es un enfoque de aprendizaje supervisado que se utiliza en estadísticas, minería de datos y aprendizaje automático. En este enfoque, se utiliza un árbol de decisión como modelo predictivo para tareas de clasificación, sacando conclusiones de un conjunto de observaciones.

**Parámetros**

En la tabla siguiente se describen los parámetros clave para configurar y optimizar el rendimiento de [!DNL Decision Tree Classifier].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | El número máximo de grupos determina cómo se dividen las funciones continuas en intervalos discretos. Esto afecta a la forma en que se dividen las funciones en cada nodo del árbol de decisión. Más grupos proporcionan una mayor granularidad. | 32 | Debe ser al menos 2 y al menos igual al número de categorías en cualquier característica categórica. |
| `CACHE_NODE_IDS` | Si `false`, el algoritmo pasa árboles a los ejecutores para que coincidan con las instancias con los nodos. Si `true`, el algoritmo almacena en caché los ID de nodo de cada instancia, lo que acelera la formación de árboles más profundos. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica la frecuencia con la que se deben comprobar los ID de nodo en caché. Por ejemplo, `10` significa que la caché se comprueba cada 10 iteraciones. | 10 | (>= 1) |
| `IMPURITY` | El criterio utilizado para calcular la ganancia de información (sin distinción de mayúsculas y minúsculas). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Profundidad máxima del árbol (no negativa). Por ejemplo, la profundidad `0` significa 1 nodo hoja y la profundidad `1` significa 1 nodo interno y 2 nodos hoja. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Ganancia mínima de información necesaria para que una división se considere en un nodo de árbol. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fracción mínima del recuento de muestra ponderado que cada hijo debe tener después de una división. Si una división hace que la fracción del peso total en cualquiera de los hijos sea menor que este valor, se descarta. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Número mínimo de instancias que debe tener cada hijo después de una división. Si una división genera menos instancias que este valor, se descarta la división. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria máxima, en MB, asignada a la agregación del histograma. Si este valor es demasiado pequeño, sólo se divide 1 nodo por iteración y sus agregados pueden superar este tamaño. | 256 |                    |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `SEED` | La semilla aleatoria. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `WEIGHT_COL` | El nombre de la columna, por ejemplo, pesos. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier cadena |
| `ONE_VS_REST` | Habilita o deshabilita el ajuste de este algoritmo con One-vs-Rest, usado para problemas de clasificación de varias clases. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

[!DNL Factorization Machine Classifier] es un algoritmo de clasificación que admite el descenso de degradado normal y el solucionador AdamW. El modelo de clasificación de la máquina de factorización utiliza la pérdida logística, que puede optimizarse a través del descenso de gradiente, y a menudo incluye términos de regularización como L2 para evitar el sobreajuste.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Factorization Machine Classifier].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | La tolerancia de convergencia, que controla la precisión de la optimización. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | La dimensionalidad de los factores. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Especifica si se ajusta a un término de intercepción. | `true` | `true`, `false` |
| `FIT_LINEAR` | Especifica si se ajusta al término lineal (también conocido como término unidireccional). | `true` | `true`, `false` |
| `INIT_STD` | Desviación estándar para los coeficientes de inicialización. | 0,01 | (>= 0) |
| `MAX_ITER` | Número máximo de iteraciones para ejecutar el algoritmo. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | La fracción de datos que se va a utilizar en minilotes durante el entrenamiento. Debe estar en el rango `(0, 1]`. | 1,0 | `(0, 1]` |
| `REG_PARAM` | El parámetro de regularización, que ayuda a controlar la complejidad del modelo y a evitar el sobreajuste. | 0,0 | (>= 0) |
| `SEED` | La semilla aleatoria para controlar procesos aleatorios en el algoritmo. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `SOLVER` | Algoritmo del solucionador utilizado para la optimización. Las opciones compatibles son `gd` (pendiente de degradado) y `adamW`. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | El tamaño inicial del paso de optimización, que a menudo se interpreta como la tasa de aprendizaje. | 1,0 | > 0 |
| `PROBABILITY_COL` | Nombre de columna para las probabilidades condicionales de clase predichas. Nota: no todos los modelos generan probabilidades bien calibradas; estas deben tratarse como puntuaciones de confianza en lugar de probabilidades exactas. | &quot;probabilidad&quot; | Cualquier cadena |
| `PREDICTION_COL` | Nombre de columna de las etiquetas de clase previstas. | &quot;predicción&quot; | Cualquier cadena |
| `RAW_PREDICTION_COL` | El nombre de columna para los valores de predicción sin procesar (también conocidos como confianza). | &quot;rawPrediction&quot; | Cualquier cadena |
| `ONE_VS_REST` | Especifica si se habilita Uno frente a Rest para la clasificación de varias clases. | FALSE | `true`, `false` |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

[!DNL Gradient Boosted Tree Classifier] utiliza un conjunto de árboles de decisión para mejorar la precisión de las tareas de clasificación, combinando varios árboles para mejorar el rendimiento del modelo.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Gradient Boosted Tree Classifier].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | El número máximo de grupos determina cómo se dividen las funciones continuas en intervalos discretos. Esto afecta a la forma en que se dividen las funciones en cada nodo del árbol de decisión. Más grupos proporcionan una mayor granularidad. | 32 | Debe ser al menos 2 e igual o mayor que el número de categorías de cualquier característica categórica. |
| `CACHE_NODE_IDS` | Si `false`, el algoritmo pasa árboles a los ejecutores para que coincidan con las instancias con los nodos. Si `true`, el algoritmo almacena en caché los ID de nodo de cada instancia, lo que acelera la formación de árboles más profundos. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica la frecuencia con la que se deben comprobar los ID de nodo en caché. Por ejemplo, `10` significa que la caché se comprueba cada 10 iteraciones. | 10 | (>= 1) |
| `MAX_DEPTH` | Profundidad máxima del árbol (no negativa). Por ejemplo, la profundidad `0` significa 1 nodo hoja y la profundidad `1` significa 1 nodo interno y 2 nodos hoja. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Ganancia mínima de información necesaria para que una división se considere en un nodo de árbol. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fracción mínima del recuento de muestra ponderado que cada hijo debe tener después de una división. Si una división hace que la fracción del peso total en cualquiera de los hijos sea menor que este valor, se descarta. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Número mínimo de instancias que debe tener cada hijo después de una división. Si una división genera menos instancias que este valor, se descarta la división. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria máxima, en MB, asignada a la agregación del histograma. Si este valor es demasiado pequeño, sólo se divide 1 nodo por iteración y sus agregados pueden superar este tamaño. | 256 |                                                                                                      |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `VALIDATION_INDICATOR_COL` | El nombre de la columna indica si cada fila se utiliza para aprendizaje o validación. `false` para aprendizaje y `true` para validación. | SIN CONFIGURAR | Cualquier cadena |
| `RAW_PREDICTION_COL` | El nombre de columna para los valores de predicción sin procesar (también conocidos como confianza). | &quot;rawPrediction&quot; | Cualquier cadena |
| `LEAF_COL` | El nombre de columna para los índices de hojas, que es el índice de hojas previsto de cada instancia en cada árbol, generado por el recorrido de orden previo. | &quot;&quot; | Cualquier cadena |
| `FEATURE_SUBSET_STRATEGY` | Número de funciones que se tienen en cuenta para la división en cada nodo de árbol. Opciones compatibles: `auto`, `all`, `onethird`, `sqrt`, `log2` y `n` (para una fracción de características). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` (donde `n` es una fracción entre 0 y 1,0) |
| `WEIGHT_COL` | El nombre de la columna, por ejemplo, pesos. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR |                                                                                                      |
| `LOSS_TYPE` | La función de pérdida que el modelo [!DNL Gradient Boosted Tree] intenta minimizar. Opciones compatibles: `logistic`. | &quot;logístico&quot; | `logistic` |
| `STEP_SIZE` | El tamaño del paso (también conocido como tasa de aprendizaje) en el rango `(0, 1]`, utilizado para reducir la contribución de cada estimador. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Número máximo de iteraciones del algoritmo. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | La fracción de datos de formación utilizados para entrenar cada árbol de decisión, en el rango `(0, 1]`. | 1,0 | `(0, 1]` |
| `PROBABILITY_COL` | Nombre de columna para las probabilidades condicionales de clase predichas. Nota: no todos los modelos generan probabilidades bien calibradas; estas deben tratarse como puntuaciones de confianza en lugar de probabilidades exactas. | &quot;probabilidad&quot; | Cualquier cadena |
| `ONE_VS_REST` | Habilita o deshabilita el ajuste de este algoritmo con One-vs-Rest para la clasificación multiclase. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LinearSVC) {#linear-support-vector-classifier}

[!DNL Linear Support Vector Classifier] (LinearSVC) construye un hiperplano para clasificar los datos en un espacio de alta dimensión. Puede utilizarlo para maximizar el margen entre clases y minimizar los errores de clasificación.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Linear Support Vector Classifier (LinearSVC)].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Número máximo de iteraciones para ejecutar el algoritmo. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | Profundidad sugerida para la agregación de árbol. | 2 |                                                                                                      |
| `FIT_INTERCEPT` | Si encaja o no con un término de intersección. | `true` | `true`, `false` |
| `TOL` | La tolerancia de convergencia para la optimización. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Memoria máxima en MB para apilar los datos de entrada en bloques. Los datos se apilan dentro de las particiones y, si el tamaño de datos restante de una partición es menor, este valor se ajusta en consecuencia. | 0,0 | (>= 0) |
| `REG_PARAM` | El parámetro de regularización, que ayuda a controlar la complejidad del modelo y a evitar el sobreajuste. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Si se deben estandarizar las funciones de formación antes de ajustar el modelo. | `true` | `true`, `false` |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `RAW_PREDICTION_COL` | El nombre de columna para los valores de predicción sin procesar (también conocidos como confianza). | &quot;rawPrediction&quot; | Cualquier cadena |
| `ONE_VS_REST` | Habilita o deshabilita el ajuste de este algoritmo con One-vs-Rest para la clasificación multiclase. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] es un algoritmo supervisado que se usa para la clasificación binaria. Modela la probabilidad de que una instancia pertenezca a una clase utilizando la función logística, lo que la hace adecuada para tareas cuyo objetivo es clasificar instancias en una de dos categorías.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Logistic Regression].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Número máximo de iteraciones que ejecuta el algoritmo. | 100 | (>= 0) |
| `REGPARAM` | El parámetro de regularización se utiliza para controlar la complejidad del modelo. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | El parámetro de mezcla `ElasticNet` controla el equilibrio entre las penalizaciones L1 (Lasso) y L2 (Ridge). Un valor de 0 aplica una penalización L2 (Cresta, que reduce el tamaño de los coeficientes), mientras que un valor de 1 aplica una penalización L1 (Lasso, que fomenta la dispersión al establecer algunos coeficientes en cero). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

[!DNL Multilayer Perceptron Classifier] es un clasificador de red neuronal artificial de avance que consta de varias capas de nodos totalmente conectados. Cada nodo de una capa asigna entradas a salidas mediante una combinación lineal ponderada de los datos de entrada, con pesos de nodo (`w`) y sesgo (`b`), seguidos de una función de activación. Este proceso ayuda a configurar y optimizar modelos estadísticos avanzados mediante el ajuste de parámetros clave, con ejemplos de código que se proporcionan para obtener más orientación. —>

**Parámetros**

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Número máximo de iteraciones para ejecutar el algoritmo. | 100 | (>= 0) |
| `BLOCK_SIZE` | Tamaño de bloque para apilar datos de entrada en matrices dentro de particiones. Si el tamaño del bloque supera los datos restantes de una partición, se ajusta en consecuencia. | 128 | (>= 0) |
| `STEP_SIZE` | El tamaño del paso utilizado para cada iteración de optimización (aplicable solo para el solucionador `gd`). | 0,03 | (> 0) |
| `TOL` | La tolerancia de convergencia para la optimización. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `SEED` | La semilla aleatoria para controlar procesos aleatorios en el algoritmo. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `PROBABILITY_COL` | Nombre de columna para las probabilidades condicionales de clase predichas. Estos deben tratarse como puntuaciones de confianza en lugar de probabilidades exactas. | &quot;probabilidad&quot; | Cualquier cadena |
| `RAW_PREDICTION_COL` | El nombre de columna para los valores de predicción sin procesar (también conocidos como confianza). | &quot;rawPrediction&quot; | Cualquier cadena |
| `ONE_VS_REST` | Habilita o deshabilita el ajuste de este algoritmo con One-vs-Rest para la clasificación multiclase. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] es un clasificador probabilístico simple multiclase basado en el teorema de Bayes con suposiciones de independencia fuertes (ingenuas) entre características. Es muy eficiente en el aprendizaje, ya que requiere un solo paso sobre los datos de formación para calcular la distribución de probabilidad condicional de cada función con cada etiqueta. Para las predicciones, utiliza el teorema de Bayes para calcular la distribución de probabilidad condicional de cada etiqueta dada una observación.

**Parámetros**

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Especifica el tipo de modelo. Las opciones compatibles son `"multinomial"`, `"complement"`, `"bernoulli"` y `"gaussian"`. El tipo de modelo distingue entre mayúsculas y minúsculas. | &quot;multinomial&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | El parámetro de suavizado, que se utiliza para suavizar los datos categóricos y controlar características no vistas. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | Nombre de columna para las probabilidades condicionales de clase predichas. Estos deben tratarse como puntuaciones de confianza en lugar de probabilidades exactas. | &quot;probabilidad&quot; | Cualquier cadena |
| `WEIGHT_COL` | El nombre de la columna para las ponderaciones de instancia. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier cadena |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `RAW_PREDICTION_COL` | El nombre de columna para los valores de predicción sin procesar (también conocidos como confianza). | &quot;rawPrediction&quot; | Cualquier cadena |
| `ONE_VS_REST` | Especifica si se habilita Uno frente a Rest para la clasificación de varias clases. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] es un algoritmo de aprendizaje conjunto que crea varios árboles de decisión durante la formación. Mitiga el sobreajuste promediando las predicciones y seleccionando la clase elegida por la mayoría de los árboles para las tareas de clasificación.

**Parámetros**

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | El número máximo de grupos determina cómo se dividen las funciones continuas en intervalos discretos. Esto afecta a la forma en que se dividen las funciones en cada nodo del árbol de decisión. Más grupos proporcionan una mayor granularidad. | 32 | Debe ser al menos 2 e igual o mayor que el número de categorías de cualquier característica categórica. |
| `CACHE_NODE_IDS` | Si `false`, el algoritmo pasa árboles a los ejecutores para que coincidan con las instancias con los nodos. Si `true`, el algoritmo almacena en caché los ID de nodo de cada instancia, lo que acelera la formación. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica la frecuencia con la que se deben comprobar los ID de nodo en caché. Por ejemplo, `10` significa que la caché se comprueba cada 10 iteraciones. | 10 | (>= 1) |
| `IMPURITY` | El criterio utilizado para calcular la ganancia de información (sin distinción de mayúsculas y minúsculas). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Profundidad máxima del árbol (no negativa). Por ejemplo, la profundidad `0` significa 1 nodo hoja y la profundidad `1` significa 1 nodo interno y 2 nodos hoja. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Ganancia mínima de información necesaria para que una división se considere en un nodo de árbol. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fracción mínima del recuento de muestra ponderado que cada hijo debe tener después de una división. Si una división hace que la fracción del peso total en cualquiera de los hijos sea menor que este valor, se descarta. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Número mínimo de instancias que debe tener cada hijo después de una división. Si una división genera menos instancias que este valor, se descarta la división. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria máxima, en MB, asignada a la agregación del histograma. Si este valor es demasiado pequeño, sólo se divide 1 nodo por iteración y sus agregados pueden superar este tamaño. | 256 | (>= 1) |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `WEIGHT_COL` | El nombre de la columna, por ejemplo, pesos. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier cadena |
| `SEED` | La semilla aleatoria utilizada para controlar procesos aleatorios en el algoritmo. | -1689246527 | Cualquier número de 64 bits |
| `BOOTSTRAP` | Indica si se utilizan muestras de bootstrap al crear árboles. | `true` | `true`, `false` |
| `NUM_TREES` | Número de árboles que se van a entrenar. Si `1`, no se usa el bootstrapping. Si es mayor que `1`, se aplica el bootstrapping. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | La fracción de datos de formación utilizados para aprender cada árbol de decisiones. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | El nombre de columna para los índices de hoja, que contiene el índice de hoja previsto de cada instancia en cada árbol por orden previo. | &quot;&quot; | Cualquier cadena |
| `PROBABILITY_COL` | Nombre de columna para las probabilidades condicionales de clase predichas. Estos deben tratarse como puntuaciones de confianza en lugar de probabilidades exactas. | &quot;probabilidad&quot; | Cualquier cadena |
| `RAW_PREDICTION_COL` | El nombre de columna para los valores de predicción sin procesar (también conocidos como confianza). | &quot;rawPrediction&quot; | Cualquier cadena |
| `ONE_VS_REST` | Especifica si se habilita Uno frente a Rest para la clasificación de varias clases. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Pasos siguientes

Después de leer este documento, ahora sabe cómo configurar y utilizar varios algoritmos de clasificación. A continuación, consulte los documentos sobre [regresión](./regression.md) y [agrupación en clúster](./clustering.md) para obtener más información sobre otros tipos de modelos estadísticos avanzados.

