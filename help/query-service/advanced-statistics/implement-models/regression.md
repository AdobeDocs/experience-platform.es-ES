---
title: Algoritmos de regresión
description: Aprenda a configurar y optimizar varios algoritmos de regresión con parámetros clave, descripciones y códigos de ejemplo para ayudarle a implementar modelos estadísticos avanzados.
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
source-git-commit: 8b9cfb48a11701f0e4b358416c6b627bedf1db8b
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 4%

---

# Algoritmos de regresión {#regression-algorithms}

Este documento proporciona una visión general de varios algoritmos de regresión, centrándose en su configuración, parámetros clave y uso práctico en modelos estadísticos avanzados. Los algoritmos de regresión se utilizan para modelar la relación entre variables dependientes e independientes, prediciendo resultados continuos basados en los datos observados. Cada sección incluye descripciones de parámetros y código de ejemplo para ayudarle a implementar y optimizar estos algoritmos para tareas como regresión lineal, de bosque aleatorio y de supervivencia.

## [!DNL Decision Tree] regresión {#decision-tree-regression}

El aprendizaje de [!DNL Decision Tree] es un método de aprendizaje supervisado que se utiliza en estadísticas, minería de datos y aprendizaje automático. En este enfoque, se utiliza un árbol de decisión de clasificación o regresión como modelo predictivo para extraer conclusiones sobre un conjunto de observaciones.

**Parámetros**

En la tabla siguiente se describen los parámetros clave para configurar y optimizar el rendimiento de los modelos del árbol de decisión.

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Este parámetro especifica el número máximo de grupos utilizados para discretizar funciones continuas y determinar divisiones en cada nodo. Más bandejas ofrecen una granularidad y un detalle más precisos. | 32 | Debe ser al menos 2 y el número de categorías de cualquier característica categórica. |
| `CACHE_NODE_IDS` | Este parámetro determina si se deben almacenar en caché los ID de nodo para cada instancia. Si `false`, el algoritmo pasa árboles a los ejecutores para que coincidan con las instancias con los nodos. Si `true`, el algoritmo almacena en caché los ID de nodo de cada instancia, lo que puede acelerar la formación de árboles más profundos. Los usuarios pueden configurar la frecuencia con la que se debe comprobar o deshabilitar la caché estableciendo `CHECKPOINT_INTERVAL`. | false | `true` o `false` |
| `CHECKPOINT_INTERVAL` | Este parámetro especifica la frecuencia con la que se deben comprobar los ID de nodo en caché. Por ejemplo, si se establece en `10`, la caché se comprobará cada 10 iteraciones. Esto solo es aplicable si `CACHE_NODE_IDS` está establecido en `true` y el directorio de puntos de comprobación está configurado en `org.apache.spark.SparkContext`. | 10 | (>=1) |
| `IMPURITY` | Este parámetro especifica el criterio utilizado para calcular la ganancia de información. Los valores admitidos son `entropy` y `gini`. | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Este parámetro especifica la profundidad máxima del árbol. Por ejemplo, una profundidad de `0` significa 1 nodo hoja, mientras que una profundidad de `1` significa 1 nodo interno y 2 nodos hoja. La profundidad debe estar dentro del intervalo `[0, 30]`. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Este parámetro establece la ganancia mínima de información necesaria para que una división se considere válida en un nodo de árbol. | 0,0 | (>=0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Este parámetro especifica la fracción mínima del recuento de muestra ponderado que cada nodo secundario debe tener después de una división. Si alguno de los nodos secundarios tiene una fracción inferior a este valor, la división se descartará. | 0,0 | [0,0; 0,5] |
| `MIN_INSTANCES_PER_NODE` | Este parámetro establece el número mínimo de instancias que cada nodo secundario debe tener después de una división. Si una división genera menos instancias que este valor, la división se descarta como no válida. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Este parámetro especifica la memoria máxima, en megabytes (MB), asignada para la agregación del histograma. Si la memoria es demasiado pequeña, sólo se dividirá un nodo por iteración y sus agregados pueden superar este tamaño. | 256 | Cualquier valor entero positivo |
| `PREDICTION_COL` | Este parámetro especifica el nombre de la columna utilizada para almacenar predicciones. | &quot;predicción&quot; | Cualquier cadena |
| `SEED` | Este parámetro define la semilla aleatoria utilizada en el modelo. | Ninguna | Cualquier número de 64 bits |
| `WEIGHT_COL` | Este parámetro especifica el nombre de la columna de peso. Si este parámetro no está establecido o está vacío, todos los pesos de instancia se tratan como `1.0`. | Sin configurar | Cualquier cadena |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Factorization Machines] regresión {#factorization-machines-regression}

[!DNL Factorization Machines] es un algoritmo de aprendizaje de regresión que admite el descenso de degradado normal y el solucionador AdamW. El algoritmo se basa en el documento de S. Rendle (2010), &quot;[!DNL Factorization Machines]&quot;.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de la regresión [!DNL Factorization Machines].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | Este parámetro especifica la tolerancia de convergencia para el algoritmo. Los valores más altos pueden dar como resultado una convergencia más rápida, pero con menos precisión. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Este parámetro define la dimensionalidad de los factores. Los valores más altos aumentan la complejidad del modelo. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Este parámetro indica si el modelo debe incluir un término de intersección. | `true` | `true`, `false` |
| `FIT_LINEAR` | Este parámetro especifica si se debe incluir un término lineal (también denominado término unidireccional) en el modelo. | `true` | `true`, `false` |
| `INIT_STD` | Este parámetro define la desviación estándar de los coeficientes iniciales utilizados en el modelo. | 0,01 | (>= 0) |
| `MAX_ITER` | Este parámetro especifica el número máximo de iteraciones para que se ejecute el algoritmo. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Este parámetro establece la fracción de minilote, que determina la parte de datos utilizada en cada lote. Debe estar en el rango `(0, 1]`. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Este parámetro establece el parámetro de regularización para evitar el sobreajuste. | 0,0 | (>= 0) |
| `SEED` | Este parámetro especifica la semilla aleatoria utilizada para la inicialización del modelo. | Ninguna | Cualquier número de 64 bits |
| `SOLVER` | Este parámetro especifica el algoritmo de Solver utilizado para la optimización. | &quot;adamW&quot; | `gd` (descenso de degradado), `adamW` |
| `STEP_SIZE` | Este parámetro especifica el tamaño inicial del paso (o la tasa de aprendizaje) para el primer paso de optimización. | 1,0 | Cualquier valor positivo |
| `PREDICTION_COL` | Este parámetro especifica el nombre de la columna donde se almacenan las predicciones. | &quot;predicción&quot; | Cualquier cadena |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Generalized Linear] regresión {#generalized-linear-regression}

A diferencia de la regresión lineal, que supone que el resultado sigue una distribución normal (gaussiana), los modelos [!DNL Generalized Linear] (GLM) permiten que el resultado siga diferentes tipos de distribuciones, como [!DNL Poisson] o binomial, según la naturaleza de los datos.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de la regresión [!DNL Generalized Linear].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Establece el número máximo de iteraciones (aplicable cuando se usa el solucionador `irls`). | 25 | (>= 0) |
| `REG_PARAM` | El parámetro de regularización. | SIN CONFIGURAR | (>= 0) |
| `TOL` | La tolerancia de convergencia. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profundidad sugerida para `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | El parámetro de familia, que describe la distribución de error utilizada en el modelo. Las opciones compatibles son `gaussian`, `binomial`, `poisson`, `gamma` y `tweedie`. | &quot;gaussiano&quot; | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Si encaja o no con un término de intersección. | `true` | `true`, `false` |
| `LINK` | La función link, que define la relación entre el predictor lineal y la media de la función de distribución. Las opciones compatibles son `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` y `sqrt`. | SIN CONFIGURAR | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | Este parámetro especifica el índice en la función de vínculo de alimentación. El parámetro solo es aplicable a la familia [!DNL Tweedie]. Si no se establece, el valor predeterminado es `1 - variancePower`, que se ajusta al paquete R `statmod`. Las potencias específicas de los vínculos de 0, 1, -1 y 0,5 corresponden a los vínculos Log, Identity, Inverse y Sqrt, respectivamente. | 1 | Cualquier valor numérico |
| `SOLVER` | Algoritmo del solucionador utilizado para la optimización. Opción admitida: `irls` (mínimos cuadrados ponderados de forma iterativa). | &quot;chicas&quot; | `irls` |
| `VARIANCE_POWER` | Este parámetro especifica la potencia en la función de varianza de la distribución [!DNL Tweedie], definiendo la relación entre varianza y media. Los valores admitidos son 0 y `[1, inf)`. Los poderes de varianza de 0, 1 y 2 corresponden a las familias Gaussiana, Poisson y Gamma, respectivamente. | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | El nombre de la columna predicción de vínculos (predictor lineal). | SIN CONFIGURAR | Cualquier cadena |
| `OFFSET_COL` | Nombre de la columna de desplazamiento. Si no se define, todos los desplazamientos de instancia se tratan como 0,0. La función de desvío tiene un coeficiente constante de 1,0. | SIN CONFIGURAR | Cualquier cadena |
| `WEIGHT_COL` | Nombre de la columna de peso. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. En la familia Binomial, los pesos corresponden al número de ensayos y los pesos no enteros se redondean en el cálculo de AIC. | SIN CONFIGURAR | Cualquier cadena |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree] regresión {#gradient-boosted-tree-regression}

Los árboles impulsados por gradiente (TGB) son un método efectivo de clasificación y regresión que combina las predicciones de múltiples árboles de decisión para mejorar la precisión predictiva y el rendimiento del modelo.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de la regresión [!DNL Gradient Boosted Tree].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Número máximo de grupos utilizados para dividir funciones continuas en intervalos discretos, lo que ayuda a determinar cómo se dividen las funciones en cada nodo del árbol de decisión. Más grupos proporcionan una mayor granularidad. | 32 | Debe ser al menos 2 e igual o mayor que el número de categorías de cualquier característica categórica. |
| `CACHE_NODE_IDS` | Si `false`, el algoritmo pasa árboles a los ejecutores para que coincidan con las instancias con los nodos. Si `true`, el algoritmo almacena en caché los ID de nodo de cada instancia. El almacenamiento en caché puede acelerar el entrenamiento de árboles más profundos. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica la frecuencia con la que se deben comprobar los ID de nodo en caché. Por ejemplo, `10` significa que la caché se comprueba cada 10 iteraciones. | 10 | (>= 1) |
| `MAX_DEPTH` | Profundidad máxima del árbol (no negativa). Por ejemplo, la profundidad `0` significa 1 nodo hoja y la profundidad `1` significa 1 nodo interno con 2 nodos hoja. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Ganancia mínima de información necesaria para que una división se considere en un nodo de árbol. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fracción mínima del recuento de muestra ponderado que cada hijo debe tener después de una división. Si una división hace que la fracción del peso total en cualquiera de los hijos sea menor que este valor, se descarta. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Número mínimo de instancias que debe tener cada hijo después de una división. Si una división genera menos instancias que este valor, se descarta la división. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria máxima, en MB, asignada a la agregación del histograma. Si este valor es demasiado pequeño, sólo se divide 1 nodo por iteración y sus agregados pueden superar este tamaño. | 256 | Cualquier valor entero positivo |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `VALIDATION_INDICATOR_COL` | El nombre de la columna que indica si cada fila se utiliza para aprendizaje o validación. `false` para aprendizaje y `true` para validación. | SIN CONFIGURAR | Cualquier cadena |
| `LEAF_COL` | El nombre de columna para los índices de hoja. El índice de hoja predicho de cada instancia en cada árbol, generado por el recorrido de preorden. | &quot;&quot; | Cualquier cadena |
| `FEATURE_SUBSET_STRATEGY` | Este parámetro especifica el número de funciones que se deben tener en cuenta para las divisiones en cada nodo de árbol. | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2` o una fracción entre 0 y 1,0 |
| `SEED` | La semilla aleatoria. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `WEIGHT_COL` | El nombre de la columna, por ejemplo, pesos. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier cadena |
| `LOSS_TYPE` | Este parámetro especifica la función de pérdida que minimiza el modelo [!DNL Gradient Boosted Tree]. | &quot;al cuadrado&quot; | `squared` (L2) y `absolute` (L1). Nota: Los valores no distinguen entre mayúsculas y minúsculas. |
| `STEP_SIZE` | El tamaño del paso (también conocido como tasa de aprendizaje) en el rango `(0, 1]`, utilizado para reducir la contribución de cada estimador. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Número máximo de iteraciones del algoritmo. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | La fracción de datos de formación utilizados para aprender cada árbol de decisión, en el rango `(0, 1]`. | 1,0 | `(0, 1]` |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Isotonic] regresión {#isotonic-regression}

[!DNL Isotonic Regression] es un algoritmo utilizado para ajustar distancias de forma iterativa preservando al mismo tiempo el orden relativo de las disimilitudes en los datos.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Isotonic Regression].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Especifica si la secuencia de salida debe ser isotónica (aumentando) al `true` o antitónica (disminuyendo) al `false`. | `true` | `true`, `false` |
| `WEIGHT_COL` | El nombre de la columna, por ejemplo, pesos. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier cadena |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `FEATURE_INDEX` | El índice de la característica, aplicable cuando `featuresCol` es una columna vectorial. Si no se establece, el valor predeterminado es `0`. De lo contrario, no tiene ningún efecto. | 0 | Cualquier entero no negativo. |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Linear] regresión {#linear-regression}

[!DNL Linear Regression] es un algoritmo de aprendizaje automático supervisado que ajusta una ecuación lineal a los datos para modelar la relación entre una variable dependiente y características independientes.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Linear Regression].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Número máximo de iteraciones. | 100 | (>= 0) |
| `REGPARAM` | Parámetro de regularización utilizado para controlar la complejidad del modelo. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | El parámetro de mezcla ElasticNet, que controla el equilibrio entre las penalizaciones L1 (Lasso) y L2 (Ridge). El valor 0 aplica una penalización L2, mientras que el valor 1 aplica una penalización L1. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] es un algoritmo ensamblado que crea varios árboles de decisión durante el entrenamiento y devuelve la predicción promedio de esos árboles para tareas de regresión, lo que ayuda a evitar el sobreajuste.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Random Forest Regression].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Número máximo de grupos utilizados para diferenciar las funciones continuas y determinar cómo se dividen las funciones en cada nodo. Más grupos proporcionan una mayor granularidad. | 32 | Debe ser al menos 2 y al menos igual al número de categorías en cualquier característica categórica. |
| `CACHE_NODE_IDS` | Si `false`, el algoritmo pasa árboles a los ejecutores para que coincidan con las instancias con los nodos. Si `true`, el algoritmo almacena en caché los ID de nodo de cada instancia, lo que acelera la formación de árboles más profundos. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Especifica la frecuencia con la que se deben comprobar los ID de nodo en caché. Por ejemplo, `10` significa que la caché se comprueba cada 10 iteraciones. | 10 | (>= 1) |
| `IMPURITY` | El criterio utilizado para calcular la ganancia de información (sin distinción de mayúsculas y minúsculas). | &quot;entropía&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Profundidad máxima del árbol (no negativa). Por ejemplo, la profundidad `0` significa 1 nodo hoja y la profundidad `1` significa 1 nodo interno y 2 nodos hoja. | 5 | Cualquier entero no negativo. |
| `MIN_INFO_GAIN` | Ganancia mínima de información necesaria para que una división se considere en un nodo de árbol. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fracción mínima del recuento de muestra ponderado que cada hijo debe tener después de una división. Si una división hace que la fracción del peso total en cualquiera de los hijos sea menor que este valor, se descarta. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Número mínimo de instancias que debe tener cada hijo después de una división. Si una división genera menos instancias que este valor, se descarta la división. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria máxima, en MB, asignada a la agregación del histograma. Si este valor es demasiado pequeño, sólo se divide 1 nodo por iteración y sus agregados pueden superar este tamaño. | 256 | (>= 1) |
| `BOOTSTRAP` | Indica si se deben usar muestras de bootstrap al crear árboles. | VERDADERO | `true`, `false` |
| `NUM_TREES` | El número de árboles para entrenar (al menos 1). Si `1`, no se usa el bootstrapping. Si es mayor que `1`, se aplica el bootstrapping. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | La fracción de datos de formación utilizada para entrenar cada árbol de decisión, en el intervalo `(0, 1]`. | 1,0 | (>= 0,0, &lt;= 1) |
| `LEAF_COL` | El nombre de columna para los índices de hojas, que es el índice de hojas previsto de cada instancia en cada árbol, generado por el recorrido de orden previo. | &quot;&quot; | Cualquier cadena |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `SEED` | La semilla aleatoria. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `WEIGHT_COL` | El nombre de la columna, por ejemplo, pesos. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier nombre de columna válido o déjelo vacío. |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] se usa para ajustar un modelo paramétrico de regresión de supervivencia, conocido como el modelo [!DNL Accelerated Failure Time] (AFT), basado en [!DNL Weibull distribution]. Puede apilar instancias en bloques para obtener un rendimiento mejorado.

**Parámetros**

La tabla siguiente describe los parámetros clave para configurar y optimizar el rendimiento de [!DNL Survival Regression].

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Número máximo de iteraciones que debe ejecutarse el algoritmo. | 100 | (>= 0) |
| `TOL` | La tolerancia de convergencia. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profundidad sugerida para `treeAggregate`. Si las cotas de la función o el número de particiones son grandes, este parámetro se puede definir en un valor mayor. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Si encaja o no con un término de intersección. | VERDADERO | `true`, `false` |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |
| `CENSOR_COL` | El nombre de columna para la censura. El valor `1` indica que el evento se produjo (sin censura), mientras que `0` significa que el evento está censurado. | &quot;censurar&quot; | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | Memoria máxima en MB para apilar los datos de entrada en bloques. Si el tamaño de datos restante en una partición es menor, este valor se ajusta en consecuencia. El valor `0` permite el ajuste automático. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Pasos siguientes

Después de leer este documento, ahora sabe cómo configurar y utilizar varios algoritmos de regresión. A continuación, consulte los documentos sobre [clasificación](./classification.md) y [agrupación en clúster](./clustering.md) para obtener más información sobre otros tipos de modelos estadísticos avanzados.
