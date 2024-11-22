---
title: Técnicas de transformación de funciones
description: Obtenga información acerca de las técnicas de preprocesamiento esenciales, como la transformación de datos, la codificación y la escala de características, que preparan los datos para la formación del modelo estadístico. Cubre la importancia de gestionar los valores que faltan y convertir los datos categóricos para mejorar el rendimiento y la precisión del modelo.
role: Developer
exl-id: ed7fa9b7-f74e-481b-afba-8690ce50c777
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '3450'
ht-degree: 8%

---

# Técnicas de transformación de funciones

Las transformaciones son pasos de preprocesamiento cruciales que convierten o escalan los datos en un formato adecuado para la formación y el análisis de modelos, lo que garantiza un rendimiento y una precisión óptimos. Este documento sirve como recurso de sintaxis complementario, que proporciona detalles exhaustivos sobre las técnicas clave de transformación de funciones para el preprocesamiento de datos.

Los modelos de aprendizaje automático no pueden procesar directamente valores de cadena o valores nulos, por lo que el preprocesamiento de datos es esencial. En esta guía se explica cómo utilizar varias transformaciones para imputar valores que faltan, convertir datos categóricos en formatos numéricos y aplicar técnicas de escalado de funciones como codificación y vectorización en un solo paso. Estos métodos permiten a los modelos interpretar y aprender eficazmente de los datos, mejorando finalmente su rendimiento.

## Transformación automática de funciones {#automatic-transformations}

Si elige omitir la cláusula `TRANSFORM` en el comando `CREATE MODEL`, la transformación de características se produce automáticamente. El preprocesamiento automático de datos incluye el reemplazo nulo y las transformaciones de funciones estándar (según el tipo de datos). Las columnas numéricas y de texto se imputan automáticamente y, a continuación, se llevan a cabo transformaciones de funciones para garantizar que los datos tengan un formato adecuado para la formación del modelo de aprendizaje automático. Este proceso incluye la imputación de datos que faltan y transformaciones categóricas, numéricas y booleanas.

>[!IMPORTANT]
>
>La transformación de funciones utilizada en el momento del entrenamiento también se utilizará para la transformación de funciones en el momento de la predicción y evaluación.

En las tablas siguientes se explica cómo se controlan los distintos tipos de datos cuando se omite la cláusula `TRANSFORM` durante el comando `CREATE MODEL`.

### Reemplazo nulo {#automatic-null-replacement}

| Tipo de datos | Reemplazo nulo |
|-----------------|-----------------------------------------------------|
| Numérico | Los valores nulos se sustituyen por el valor medio de la columna. |
| Categórico | Los valores nulos se reemplazan con la palabra clave `ml_unknown`. |
| Booleano | Los valores nulos se reemplazan con un valor `FALSE`. |
| Marca de tiempo | Se espera que este sea un campo continuo. |
| Anidado/STRUCT | El reemplazo depende del tipo de datos del nodo de hoja. |

### Transformación de funciones {#automatic-feature-transformation}

| Tipo de datos | Transformación de funciones |
|-----------------|-----------------------------------------------------|
| Numérico | NO OBLIGATORIO: dado que los algoritmos de aprendizaje automático comprenden este tipo de datos. |
| Cadena | Se produce la indexación de cadenas. |
| Booleano | Se produce la indexación de cadenas. |
| Marca de tiempo | No se produce ninguna operación. |
| STRUCT | El valor se expande a su nodo de hoja. La transformación se produce en función del tipo de datos del nodo de hoja. |

**ejemplo**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Transformaciones manuales de funciones {#manual-transformations}

Para definir el preprocesamiento de datos personalizados en la instrucción `CREATE MODEL`, utilice la cláusula `TRANSFORM` en combinación con cualquier número de funciones de transformación disponibles. Estas funciones de preprocesamiento manual también se pueden utilizar fuera de la cláusula `TRANSFORM`. Todas las transformaciones que se discuten en la sección [transformador a continuación](#available-transformations), se pueden usar para preprocesar los datos manualmente.

### Características principales {#key-characteristics}

Las siguientes son características clave de la transformación de funciones que se deben tener en cuenta al definir las funciones de preprocesamiento:

- **Sintaxis**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - El nombre del alias es obligatorio en la sintaxis. Debe proporcionar un nombre de alias o la consulta fallará.

- **Parámetros**: los parámetros son argumentos de posición. Esto significa que cada parámetro solo puede tomar determinados valores y requerir que se especifiquen todos los parámetros anteriores si se proporcionan valores personalizados. Consulte la documentación relevante para obtener detalles sobre qué función toma qué argumento.

- **Transformadores de encadenamiento**: La salida de un transformador puede convertirse en la entrada de otro transformador.

- **Uso de características**: la última transformación de características se usa como característica del modelo de aprendizaje automático.

**Ejemplo**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## Transformaciones disponibles {#available-transformations}

Hay 19 transformaciones disponibles. Estas transformaciones se dividen en [transformaciones generales](#general-transformations), [transformaciones numéricas](#numeric-transformations), [transformaciones categóricas](#categorical-transformations) y [transformaciones textuales](#textual-transformations).

### Transformaciones generales {#general-transformations}

Lea esta sección para obtener más información sobre los transformadores utilizados para una amplia gama de tipos de datos. Esta información es esencial si necesita aplicar transformaciones que no sean específicas de los datos categóricos o de texto.

>[!NOTE]
>
>El tipo de datos de entrada hace referencia a la columna en la que se aplica la imputación. El tipo de datos de salida hace referencia a la columna que se produce como salida después de que la transformación haya surtido efecto.

#### Imputador numérico {#numeric-imputer}

El transformador **Imputador numérico** completa los valores que faltan en un conjunto de datos. Utiliza la media, la mediana o el modo de las columnas en las que se encuentran los valores que faltan. Las columnas de entrada deben ser `DoubleType` o `FloatType`. Encontrará más información y ejemplos en la [documentación del algoritmo Spark](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).

>[!NOTE]
>
>Todos los valores nulos de las columnas de entrada se tratan como ausentes y, por lo tanto, también se imputan.

**Tipos de datos**

- Tipo de datos de entrada: numérico
- Tipo de datos de salida: numérico

**Definición**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | Una estrategia de imputación. Los valores disponibles son: [`mean`, `median`, `mode`]. | cadena | malo | opcional |

{style="table-layout:auto"}

**Ejemplo antes de la imputación**

| Identificación | hora |
|---|---|
| 0 | 18,0 |
| 1 | null |
| 2 | 8,0 |

**Ejemplo después de la imputación (con estrategia media)**

| Identificación | hora |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Imputador de cadena {#string-imputer}

El transformador **String imputer** completa los valores que faltan en un conjunto de datos utilizando una cadena proporcionada por el usuario como argumento de función. Las columnas de entrada y salida deben ser del tipo de datos `string`.

>[!NOTE]
>
>Todos los valores nulos de las columnas de entrada se tratan como ausentes y se sustituyen por la cadena especificada.

**Tipos de datos**

- Tipo de datos de entrada: cadena
- Tipo de datos de salida: cadena

**Definición**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | El valor que reemplaza los valores nulos. | cadena | ml_unknown | opcional |

{style="table-layout:auto"}

**Ejemplo antes de la imputación**

| Identificación | name |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**Ejemplo después de la imputación (utilizando &#39;ml_unknown&#39; como reemplazo)**

| Identificación | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Imputador booleano {#boolean-imputer}

El transformador **Boolean imputer** completa los valores que faltan en un conjunto de datos para una columna booleana. Las columnas de entrada y salida deben ser del tipo `Boolean`.

>[!NOTE]
>
>Todos los valores nulos de las columnas de entrada se tratan como ausentes y se sustituyen por el valor booleano especificado.

**Tipos de datos**

- Tipo de datos de entrada: booleano
- Tipo de datos de salida: booleano

**Definición**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Imputador booleano. Valores permitidos: [`true`, `false`]. | Booleano | false | opcional |

**Ejemplo antes de la imputación**

| Identificación | indicador |
|---|---|
| 0 | true |
| 1 | null |
| 2 | false |

**Ejemplo después de la imputación (se usa &#39;true&#39; como reemplazo)**

| Identificación | indicador |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### Ensamblador vectorial {#vector-assembler}

El transformador `VectorAssembler` combina una lista especificada de columnas de entrada en una sola columna vectorial, lo que facilita la administración de varias funciones en los modelos de aprendizaje automático. Esto resulta particularmente útil para combinar funciones sin procesar y aquellas generadas por diferentes transformadores de funciones en un vector de funciones unificado. `VectorAssembler` acepta columnas de entrada de tipos numéricos, booleanos y vectoriales. En cada fila, los valores de las columnas de entrada se concatenan en un vector en el orden especificado.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Tipos de datos**

- Tipo de datos de entrada: `array[string]` (nombres de columna con valores numéricos/array[numeric])
- Tipo de datos de salida: `Vector[double]`

**Definición**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
| -------- | ------------ | ----- | -------- | -------- |
| NA | No se requieren parámetros adicionales para este transformador. | NA | NA | NA |

{style="table-layout:auto"}

**Ejemplo antes de la transformación**

| Identificación | hora | móvil | userFeatures | pulsado |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1,0 | [0,0; 10,0; 0,5] | 1,0 |

{style="table-layout:auto"}

**Ejemplo después de la transformación**

| Identificación | hora | móvil | userFeatures | pulsado | características |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1,0 | [0,0; 10,0; 0,5] | 1,0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### Transformaciones numéricas {#numeric-transformations}

Lea esta sección para obtener más información sobre los transformadores disponibles para procesar y escalar datos numéricos. Estos transformadores son necesarios para gestionar y optimizar las funciones numéricas de los conjuntos de datos.

#### Binarizador {#binarizer}

El transformador `Binarizer` convierte las características numéricas en características binarias (0/1) mediante un proceso denominado binarización. Los valores mayores que el umbral especificado se convierten en 1,0, mientras que los valores iguales o menores que el umbral se convierten en 0,0. `Binarizer` admite los tipos `Vector` y `Double` para la columna de entrada.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**Tipos de datos**

- Tipo de datos de entrada: columna numérica
- Tipo de datos de salida: numérico

**Definición**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | Parámetro para el umbral utilizado para binarizar funciones continuas. Las características superiores al umbral se binarizan en 1,0, mientras que las características iguales o inferiores al umbral se binarizan en 0,0. | int/double | 0,0 | opcional |

{style="table-layout:auto"}

**Entrada de ejemplo antes de la binarización**

| Identificación | clasificación |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Ejemplo de salida después de la binarización (umbral predeterminado de 0,0)**

| Identificación | clasificación |
|---|---------|
| 0 | 0,0 |
| 1 | 1,0 |
| 2 | 1,0 |

**Definición con umbral personalizado**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**Ejemplo de salida después de la binarización (con un umbral de 14.0)**

| Identificación | edad |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1,0 |

#### Bucketizer {#bucketizer}

El transformador `Bucketizer` convierte una columna de características continuas en una columna de contenedores de características, según los umbrales especificados por el usuario. Este proceso es útil para segmentar datos continuos en grupos o bloques discretos. El `Bucketizer` requiere un parámetro `splits`, que define los límites de los contenedores.

**Tipos de datos**

- Tipo de datos de entrada: columna numérica
- Tipo de datos de salida: numérico (valores agrupados)

**Definición**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | Un parámetro para asignar funciones continuas a contenedores. Con `n+1` divisiones, hay `n` bloques. Las divisiones deben estar en orden estrictamente creciente y se utiliza el rango (x,y) para cada bloque excepto el último, que incluye y. | array(doble) | N/A | opcional |

{style="table-layout:auto"}

**Ejemplos de divisiones**

- Matriz(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Matriz (0.0, 1.0, 2.0)

Las divisiones deben cubrir todo el rango de valores Double; de lo contrario, los valores fuera de las divisiones especificadas se tratarán como errores.

**Ejemplo de transformación**

Este ejemplo toma una columna de características continuas (`course_duration`), la agrupa según el elemento proporcionado `splits` y, a continuación, ensambla los contenedores resultantes con otras características.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

El transformador `MinMaxScaler` vuelve a escalar cada característica de un conjunto de datos de filas vectoriales a un intervalo especificado, normalmente [0, 1]. Esto garantiza que todas las funciones contribuyan de forma equitativa al modelo. Resulta particularmente útil para modelos sensibles al escalado de características, como los algoritmos basados en degradado y descenso. `MinMaxScaler` funciona con los siguientes parámetros:

- **min**: límite inferior de la transformación, compartido por todas las características. El valor predeterminado es `0.0`.
- **max**: el límite superior de la transformación, compartido por todas las características. El valor predeterminado es `1.0`.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**Tipos de datos**

- Tipo de datos de entrada: `Array[Double]`
- Tipo de datos de salida: `Array[Double]`

**Definición**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | Límite inferior después de la transformación, compartido por todas las funciones. | doble | 0,0 | opcional |
| `max` | Límite superior después de la transformación, compartido por todas las funciones. | doble | 1,0 | opcional |

**Ejemplo de transformación**

En este ejemplo se transforma un conjunto de características y se cambia su escala al rango especificado mediante MinMaxScaler después de aplicar otras transformaciones.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

El transformador `MaxAbsScaler` vuelve a escalar cada característica de un conjunto de datos de filas vectoriales al rango [-1, 1] dividiendo por el valor absoluto máximo de cada característica. Esta transformación es ideal para preservar la dispersión en conjuntos de datos con valores positivos y negativos, ya que no desplaza ni centra los datos. Esto hace que `MaxAbsScaler` sea especialmente adecuado para modelos que son sensibles a la escala de las características de entrada, como aquellos que implican cálculos de distancia.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**Tipos de datos**

- Tipo de datos de entrada: `Array[Double]`
- Tipo de datos de salida: `Array[Double]`

**Definición**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| NA | MaxAbsScaler no requiere ningún parámetro adicional para su funcionamiento. | NA | NA | NA |

**Ejemplo de transformación**

Este ejemplo aplica varias transformaciones, incluido `MaxAbsScaler`, para cambiar el tamaño de las características en el rango [-1, 1].

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normalizador {#normalizer}

El `Normalizer` es un transformador que normaliza cada vector en un conjunto de datos de filas vectoriales para que tenga una norma unitaria. Este proceso asegura una escala consistente sin alterar la dirección de los vectores. Esta transformación es particularmente útil en los modelos de aprendizaje automático que dependen de medidas a distancia u otros cálculos basados en vectores, especialmente cuando la magnitud de los vectores varía significativamente.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**Tipos de datos**

- Tipo de datos de entrada: `array[double]` / `vector[double]`
- Tipo de datos de salida: `vector[double]`

**Definición**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | Especifica el `p-norm` utilizado para la normalización (por ejemplo, `1-norm`, `2-norm`, etc.). | entero | 2 | opcional |

**Ejemplo de transformación**

En este ejemplo se muestra cómo aplicar varias transformaciones, incluida la `Normalizer`, para normalizar un conjunto de características utilizando la `p-norm` especificada.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### CuantilDiscretizer {#quantilediscretizer}

`QuantileDiscretizer` es un transformador que convierte una columna con características continuas en características categóricas agrupadas, con el número de grupos determinado por el parámetro `numBuckets`. En algunos casos, el número real de contenedores puede ser menor que el número especificado si hay demasiado pocos valores distintos para crear suficientes cuantiles.

Esta transformación es especialmente útil para simplificar la representación de datos continuos o prepararlos para algoritmos que funcionen mejor con entradas categóricas.

**Tipos de datos**

- Tipo de datos de entrada: columna numérica
- Tipo de datos de salida: columna numérica (categórica)

**Definición**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | El número de bloques (cuantiles o categorías) en los que se agrupan los puntos de datos. Este número debe ser mayor o igual que dos. | entero | 2 | opcional |

**Ejemplo de transformación**

En este ejemplo se muestra cómo `QuantileDiscretizer` agrupa una columna de características continuas (`hour`) en tres bloques categóricos.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Ejemplo antes y después de la discretización**

| Identificación | hora | resultado |
|---|------|--------|
| 0 | 18,0 | 2.0 |
| 1 | 19,0 | 2.0 |
| 2 | 8,0 | 1,0 |
| 3 | 5.0 | 1,0 |
| 4 | 2,2 | 0,0 |

#### Escalador estándar {#standardscaler}

El `StandardScaler` es un transformador que normaliza cada característica de un conjunto de datos de filas vectoriales para que tenga una desviación estándar unitaria o una media cero. Este proceso hace que los datos sean más adecuados para los algoritmos que suponen que las funciones están centradas en torno a cero con una escala coherente. Esta transformación es particularmente importante para modelos de aprendizaje automático como la VM, la regresión logística y las redes neuronales, donde los datos no estandarizados podrían dar lugar a problemas de convergencia o a una menor precisión.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Tipos de datos**

- Tipo de datos de entrada: Vector
- Tipo de datos de salida: Vector

**Definición**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Escala los datos para que tengan una desviación estándar unitaria. | Booleano | True | opcional |
| `withMean` | Centra los datos con la media antes de escalar. Esta opción produce una salida densa, por lo que tenga cuidado con la entrada dispersa. | Booleano | False | opcional |

**Ejemplo de transformación**

En este ejemplo se muestra cómo aplicar StandardScaler a un conjunto de características, normalizándolas con la desviación estándar unitaria y la media cero.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Transformaciones categorías {#categorical-transformations}

Lea esta sección para obtener una descripción general de los transformadores disponibles diseñados para convertir y preprocesar datos categóricos para modelos de aprendizaje automático. Estas transformaciones están diseñadas para puntos de datos que representan categorías o etiquetas distintas, en lugar de valores numéricos.

#### StringIndexer {#stringindexer}

`StringIndexer` es un transformador que codifica una columna de cadena de etiquetas en una columna de índices numéricos. Los índices varían de 0 a `numLabels` y se ordenan por frecuencia de etiqueta (la etiqueta más frecuente recibe un índice de 0). Si la columna de entrada es numérica, se convierte en una cadena antes de la indexación. Las etiquetas que no se ven se pueden asignar al índice `numLabels` si lo especifica el usuario.

Esta transformación es particularmente útil para convertir datos de cadena categóricos en forma numérica, lo que lo hace adecuado para modelos de aprendizaje automático que requieren entrada numérica.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Tipos de datos**

- Tipo de datos de entrada: cadena
- Tipo de datos de salida: numérico

**Definición**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------|-------------|------|---------|----------|
| NA | `StringIndexer` no requiere ningún parámetro adicional para su funcionamiento. | NA | NA | NA |

**Ejemplo de transformación**

En este ejemplo se muestra cómo aplicar `StringIndexer` a una característica categórica, convirtiéndola en un índice numérico.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

El `OneHotEncoder` es un transformador que convierte una columna de índices de etiquetas en una columna de vectores binarios dispersos, donde cada vector tiene como máximo un solo valor. Esta codificación es especialmente útil para permitir que los algoritmos que requieren entrada numérica, como Regresión logística, incorporen datos categóricos de forma eficaz.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Tipos de datos**

- Tipo de datos de entrada: numérico
- Tipo de datos de salida: Vector[Int]

**Definición**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------|-------------|------|---------|----------|
| NA | OneHotEncoder no requiere ningún parámetro adicional para su funcionamiento. | NA | NA | NA |

**Ejemplo de transformación**

Este ejemplo muestra cómo aplicar primero `StringIndexer` a una característica categórica y, a continuación, utilizar `OneHotEncoder` para convertir los valores indizados en un vector binario.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Transformaciones textuales {#textual-transformations}

Esta sección proporciona detalles sobre los transformadores disponibles para procesar y convertir datos de texto en formatos que los modelos de aprendizaje automático pueden utilizar. Esta sección es crucial para los desarrolladores que trabajan con datos y análisis de texto en lenguaje natural.

#### CountVectorizer {#countvectorizer}

`CountVectorizer` es un transformador que convierte una colección de documentos de texto en vectores de recuentos de tokens, produciendo representaciones dispersas basadas en el vocabulario extraído del corpus. Esta transformación es esencial para convertir los datos de texto en un formato numérico que se puede utilizar en algoritmos de aprendizaje automático, como LDA (Asignación de Dirichlet Latente), representando la frecuencia de tokens dentro de cada documento.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Tipos de datos**

- Tipo de datos de entrada: Matriz[Cadena]
- Tipo de datos de salida: Vector denso

**Definición**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Tamaño máximo del vocabulario. CountVectorizer crea un vocabulario que solo considera los términos principales `vocabSize` ordenados por frecuencia de términos en todo el corpus. | Int | 218 | opcional |
| `MIN_DOC_FREQ` | Especifica el número mínimo de documentos diferentes en los que debe aparecer un término para que se incluya en el vocabulario. Puede ser un número absoluto o una fracción de documentos (si es doble). | Duplicada | 1,0 | opcional |
| `MAX_DOC_FREQ` | Especifica el número máximo de documentos diferentes en los que podría aparecer un término para incluirlos en el vocabulario. Puede ser un número absoluto o una fracción de documentos (si es doble). | Duplicada | (263)-1 | opcional |
| `MIN_TERM_FREQ` | Filtra las palabras raras de un documento. Se omiten los términos con una frecuencia/recuento inferior al umbral dado. Puede ser un número absoluto o una fracción del recuento de tokens del documento. | Duplicada | 1,0 | opcional |

{style="table-layout:auto"}

**Ejemplo de transformación**

En este ejemplo se muestra cómo CountVectorizer convierte una colección de matrices de texto en vectores de recuentos de símbolos, lo que produce una representación dispersa.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Ejemplo antes y después de la vectorización**

| Identificación | textos | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3,[0,1,2],[1.0,1.0,1.0]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

El `NGram` es un transformador que genera una secuencia de n-gramos, donde un n-gramo es una secuencia de tokens (&#39;??&#39;) (normalmente palabras) para algún entero (`𝑛`). El resultado consiste en cadenas delimitadas por espacios de palabras consecutivas &quot;??&quot;, que pueden utilizarse como características en modelos de aprendizaje automático, especialmente aquellos centrados en el procesamiento de lenguajes naturales.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Tipos de datos**

- Tipo de datos de entrada: Matriz[Cadena]
- Tipo de datos de salida: Array[String]

**Definición**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | La longitud mínima de n gramos debe ser mayor o igual que 1. | entero | 2 (características del bigrama) | opcional |

{style="table-layout:auto"}

**Ejemplo de transformación**

Este ejemplo muestra cómo el transformador NGram crea una secuencia de 3 gramos a partir de una lista de tokens derivados de datos de texto.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Ejemplo antes y después de la transformación de n-gramos**

| Identificación | textos | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;esto&quot;, &quot;era&quot;, &quot;un&quot;, &quot;entretenido&quot;, &quot;película&quot;] | [&quot;esto fue una&quot;, &quot;fue una entretenida&quot;, &quot;una entretenida película&quot;] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover` es un transformador que elimina las palabras de detención de una secuencia de cadenas, filtrando las palabras comunes que no tienen un significado significativo. Toma como entrada una secuencia de cadenas (como la salida de un token) y elimina todas las palabras de detención especificadas por el parámetro `stopWords`.

Esta transformación es útil para el preprocesamiento de datos de texto, ya que mejora la eficacia de los modelos de aprendizaje automático posteriores al eliminar palabras que no contribuyen mucho al significado general.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Tipos de datos**

- Tipo de datos de entrada: Matriz[Cadena]
- Tipo de datos de salida: Array[String]

**Definición**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | Las palabras que se filtrarán. | matriz [string] | Predeterminado: palabras de detención en inglés | opcional |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Ejemplo de transformación**

Este ejemplo muestra cómo `StopWordsRemover` filtra las palabras de detención en inglés comunes de una lista de tokens.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Ejemplo antes y después de detener la eliminación de palabras**

| Identificación | crudo | filtrado |
|----|------------------------------|--------------------------|
| 0 | [Yo, vi, el, rojo, globo] | [sierra, roja, globo] |
| 1 | [María, tenía, un, pequeño, cordero] | [María, pequeña, cordero] |

**Ejemplo con palabras de detención personalizadas**

En este ejemplo se muestra cómo utilizar una lista personalizada de palabras de detención para filtrar palabras específicas de las secuencias de entrada.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Ejemplo antes y después de la eliminación de palabras de detención personalizadas**

| Identificación | crudo | filtrado |
|----|------------------------------|--------------------------|
| 0 | [Yo, vi, el, rojo, globo] | [sierra, el, globo] |
| 1 | [María, tenía, un, pequeño, cordero] | [María, una, pequeña, cordero] |

#### TF-IDF {#tf-idf}

`TF-IDF` (Frecuencia de término-Frecuencia de documento inversa) es un transformador que se utiliza para medir la importancia de una palabra dentro de un documento en relación con un corpus. La frecuencia de término (TF) se refiere al número de veces que aparece un término \(t\) en un documento \(d\), mientras que la frecuencia de documento (DF) mide cuántos documentos del cuerpo \(D\) contienen el término \(t\). Este método se utiliza ampliamente en la minería de texto para reducir la influencia de palabras comunes, como &quot;a&quot;, &quot;the&quot; y &quot;of&quot;, que contienen poca información única.

Esta transformación es especialmente valiosa en las tareas de minería de texto y procesamiento de lenguajes naturales, ya que asigna un valor numérico a la importancia de cada palabra dentro de un documento y en todo el corpus.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Tipos de datos**

- Tipo de datos de entrada: Matriz[Cadena]
- Tipo de datos de salida: Vector[Int]

**Definición**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | Número de funciones que se van a generar. Debe ser mayor que 0. | Int | 262144 | opcional |
| `MIN_DOC_FREQ` | El número mínimo de documentos en los que debe aparecer un término para que se incluya en el modelo. | Int | 0 | opcional |

{style="table-layout:auto"}

**Ejemplo de transformación**

En este ejemplo se muestra cómo utilizar TF-IDF para transformar frases con símbolo de token en un vector de características que representa la importancia de cada término en el contexto de todo el cuerpo.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizador {#tokenizer}

`Tokenizer` es un transformador que desglosa texto, como una oración, en términos individuales, normalmente palabras. Convierte frases en matrices de tokens, proporcionando un paso fundamental en el preprocesamiento de texto que prepara los datos para un análisis de texto o procesos de modelado adicionales.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Tipos de datos**

- Tipo de datos de entrada: frase textual
- Tipo de datos de salida: Array[String]

**Definición**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|-----------|-------------|------|---------|----------|
| NA | `Tokenizer` no requiere ningún parámetro adicional para su funcionamiento. | NA | NA | NA |

**Ejemplo de transformación**

En este ejemplo se muestra cómo `Tokenizer` desglosa las frases en palabras individuales (tokens) como parte de una canalización de procesamiento de texto.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec` es un estimador que procesa secuencias de palabras que representan documentos y entrena a `Word2VecModel`. Este modelo asigna cada palabra a un vector de tamaño fijo único y transforma cada documento en un vector promediando los vectores de todas las palabras del documento. Ampliamente utilizado en tareas de procesamiento de lenguaje natural, `Word2Vec` crea incrustaciones de palabras que capturan el significado semántico, convirtiendo los datos de texto en vectores numéricos que representan las relaciones entre las palabras y permitiendo un análisis de texto más efectivo y modelos de aprendizaje automático.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**Tipos de datos**

- Tipo de datos de entrada: Matriz[Cadena]
- Tipo de datos de salida: Vector[Double]

**Definición**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Parámetros**

| Parámetro | Descripción | Tipo | Predeterminado | Opcional |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | Dimensión del vector en el que se transforma cada palabra. | Entero | 100 | opcional |
| `MIN_COUNT` | El número mínimo de veces que debe aparecer un token para incluirse en el vocabulario del modelo `Word2Vec`. | Entero | 5 | opcional |

{style="table-layout:auto"}

**Ejemplo de transformación**

Este ejemplo muestra cómo `Word2Vec` convierte una revisión con token en un vector de tamaño fijo que representa el promedio de los vectores de palabras del documento.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Ejemplo antes y después de la transformación de Word2Vec**

| reseña | tokenizado | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| esta fue una película entretenida | [esto, fue, una, entretenida, película] | [-0.025713888928294182,0.00818799751577899,0.0092235435731709,-0.01515385233797133,0.012175946310162545,3.1129065901041035E-4,0.0025145105042611252,0.005757019785232843,-0.021328244300093502,0.009335877187550069] |

{style="table-layout:auto"}
