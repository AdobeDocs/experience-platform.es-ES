---
title: Algoritmos de clúster
description: Aprenda a configurar y optimizar varios algoritmos de agrupación en clúster con parámetros clave, descripciones y códigos de ejemplo para ayudarle a implementar modelos estadísticos avanzados.
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
source-git-commit: 69c08f688d355e689e78426dd4b0ed1f4934965c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 4%

---

# Algoritmos de clúster {#clustering-algorithms}

Los algoritmos de agrupación agrupan los puntos de datos en distintos clústeres en función de sus similitudes, lo que permite al aprendizaje no supervisado descubrir patrones dentro de los datos. Para crear un algoritmo de clúster, use el parámetro `type` en la cláusula `OPTIONS` para especificar el algoritmo que desea usar para la formación de modelos. A continuación, defina los parámetros relevantes como pares clave-valor para ajustar el modelo.

>[!NOTE]
>
>Asegúrese de comprender los requisitos de parámetros del algoritmo elegido. Si decide no personalizar ciertos parámetros, el sistema aplica la configuración predeterminada. Consulte la documentación pertinente para comprender la función y los valores predeterminados de cada parámetro.

## [!DNL K-Means] {#kmeans}

`K-Means` es un algoritmo de agrupación en clúster que divide los puntos de datos en un número predefinido de clústeres (k). Es uno de los algoritmos más utilizados para la agrupación en clúster debido a su simplicidad y eficiencia.

**Parámetros**

Al utilizar `K-Means`, se pueden establecer los siguientes parámetros en la cláusula `OPTIONS`:

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | El número de iteraciones que debe ejecutarse el algoritmo. | `20` | (>= 0) |
| `TOL` | El nivel de tolerancia de convergencia. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Número de clústeres que se van a crear (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Algoritmo utilizado para calcular la distancia entre dos puntos. El valor distingue entre mayúsculas y minúsculas. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Algoritmo de inicialización para los centros de agrupamiento. | `k-means\|\|` | `random`, `k-means\|\|` (Una versión paralela de k-medias++) |
| `INIT_STEPS` | El número de pasos para el modo de inicialización `k-means\|\|` (aplicable solo cuando `KMEANS_INIT_METHOD` es `k-means\|\|`). | `2` | (>0) |
| `PREDICTION_COL` | Nombre de la columna donde se almacenarán las predicciones. | `prediction` | Cualquier cadena |
| `SEED` | Una semilla aleatoria para la reproducibilidad. | `-1689246527` | Cualquier número de 64 bits |
| `WEIGHT_COL` | Nombre de la columna utilizada para las ponderaciones de instancia. Si no se configura, todas las instancias se ponderan de forma equitativa. | `not set` | N/A |

{style="table-layout:auto"}

**Ejemplo**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means] es un algoritmo de agrupación en clúster jerárquico que usa un enfoque divisivo (o &quot;descendente&quot;). Todas las observaciones comienzan en un único grupo y las divisiones se realizan de forma recursiva a medida que se crea la jerarquía. [!DNL Bisecting K-means] puede ser a menudo más rápido que las K-medias normales, pero normalmente produce resultados de clúster diferentes.

**Parámetros**

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Número máximo de iteraciones que ejecuta el algoritmo. | 20 | (>= 0) |
| `WEIGHT_COL` | El nombre de la columna para las ponderaciones de instancia. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier cadena |
| `NUM_CLUSTERS` | El número deseado de grupos de hojas. El número real podría ser menor si no quedan clústeres divisibles. | 4 | (> 1) |
| `SEED` | La semilla aleatoria utilizada para controlar procesos aleatorios en el algoritmo. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `DISTANCE_MEASURE` | La medida de distancia utilizada para calcular la similitud entre puntos. | &quot;euclidiano&quot; | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | El número mínimo de puntos (si >= 1,0) o la proporción mínima de puntos (si &lt; 1,0) necesaria para que un grupo sea divisible. | 1,0 | (>= 0) |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] representa una distribución compuesta en la que los puntos de datos se extraen de una de las subdistribuciones k de Gauss, cada una con su propia probabilidad. Se utiliza para modelar conjuntos de datos que se supone que se generan a partir de una mezcla de varias distribuciones gaussianas.

**Parámetros**

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Número máximo de iteraciones para ejecutar el algoritmo. | 100 | (>= 0) |
| `WEIGHT_COL` | El nombre de la columna, por ejemplo, pesos. Si no está establecido o vacío, todos los pesos de instancia se tratan como `1.0`. | SIN CONFIGURAR | Cualquier nombre de columna válido o vacío |
| `NUM_CLUSTERS` | Número de distribuciones gaussianas independientes en el modelo de mezcla. | 2 | (> 1) |
| `SEED` | La semilla aleatoria utilizada para controlar procesos aleatorios en el algoritmo. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `AGGREGATION_DEPTH` | Este parámetro controla la profundidad de los árboles de agregación utilizados durante el cálculo. | 2 | (>= 1) |
| `PROBABILITY_COL` | Nombre de columna para las probabilidades condicionales de clase predichas. Estos deben tratarse como puntuaciones de confianza en lugar de probabilidades exactas. | &quot;probabilidad&quot; | Cualquier cadena |
| `TOL` | La tolerancia de convergencia para algoritmos iterativos. | 0,01 | (>= 0) |
| `PREDICTION_COL` | El nombre de columna para la salida de predicción. | &quot;predicción&quot; | Cualquier cadena |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) es un modelo probabilístico que captura la estructura del tema subyacente de una colección de documentos. Es un modelo bayesiano jerárquico de tres niveles con capas de palabras, temas y documentos. LDA utiliza estas capas, junto con los documentos observados, para crear una estructura de temas latente.

**Parámetros**

| Parámetro | Descripción | Valor predeterminado | Valores posibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Número máximo de iteraciones que ejecuta el algoritmo. | 20 | (>= 0) |
| `OPTIMIZER` | El optimizador o algoritmo de inferencia utilizado para estimar el modelo LDA. Las opciones compatibles son `"online"` (Variaciones de bayas en línea) y `"em"` (Expectación-Maximización). | &quot;en línea&quot; | `online`, `em` (sin distinción de mayúsculas y minúsculas) |
| `NUM_CLUSTERS` | Número de clústeres que se van a crear (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Especifica la frecuencia con la que se deben comprobar los ID de nodo en caché. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | El parámetro de concentración (&quot;alpha&quot;) determina las suposiciones anteriores con respecto a la distribución temática entre documentos. El comportamiento predeterminado viene determinado por el optimizador. Para el optimizador `EM`, los valores alfa deben ser mayores que 1,0 (predeterminado: distribuido uniformemente como (50/k) + 1), lo que garantiza distribuciones de temas simétricas. Para el optimizador `online`, los valores alfa pueden ser 0 o mayores (predeterminado: distribuido uniformemente como 1,0/k), lo que permite una inicialización de tema más flexible. | Automático | Cualquier valor único o vector de longitud k donde los valores > 1 para EM |
| `KEEP_LAST_CHECKPOINT` | Indica si se debe mantener el último punto de comprobación al usar el optimizador `em`. La eliminación del punto de comprobación puede provocar errores si se pierde una partición de datos. Los puntos de comprobación se eliminan automáticamente del almacenamiento cuando ya no son necesarios, según lo determinado por el recuento de referencias. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Tasa de aprendizaje para el optimizador `online`, establecida como una tasa de disminución exponencial entre `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Un parámetro de aprendizaje para el optimizador `online` que reduce el valor de las iteraciones tempranas para que las iteraciones tempranas cuenten menos. | 1024 | (> 0) |
| `SEED` | Raíz aleatoria para controlar procesos aleatorios en el algoritmo. | SIN CONFIGURAR | Cualquier número de 64 bits |
| `OPTIMIZE_DOC_CONCENTRATION` | Para el optimizador `online`: si se debe optimizar `docConcentration` (parámetro Dirichlet para la distribución de temas de documentos) durante la formación. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Para el optimizador `online`: la fracción del corpus muestreada y utilizada en cada iteración de descenso de degradado de minilotes, en el rango `(0, 1]`. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | El parámetro de concentración (&quot;beta&quot; o &quot;eta&quot;) define las suposiciones previas colocadas en las distribuciones de los temas sobre los términos. El optimizador determina el valor predeterminado: Para `EM`, valores > 1,0 (predeterminado = 0,1 + 1). Para `online`, los valores ≥ 0 (predeterminado = 1,0/k). | Automático | Cualquier valor único o vector de longitud k, donde los valores > 1 para EM |
| `TOPIC_DISTRIBUTION_COL` | Este parámetro genera la distribución estimada de la mezcla de temas para cada documento, a menudo referido como &quot;theta&quot; en la literatura. Para documentos vacíos, devuelve un vector de ceros. Las estimaciones se derivan mediante una aproximación variacional (&quot;gamma&quot;). | SIN CONFIGURAR | Cualquier cadena |

{style="table-layout:auto"}

**Ejemplo**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Pasos siguientes

Después de leer este documento, ahora sabe cómo configurar y utilizar varios algoritmos de agrupación en clúster. A continuación, consulte los documentos sobre [clasificación](./classification.md) y [regresión](./regression.md) para obtener más información sobre otros tipos de modelos estadísticos avanzados.
