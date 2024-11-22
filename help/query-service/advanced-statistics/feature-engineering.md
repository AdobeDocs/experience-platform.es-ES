---
title: Extensión SQL de ingeniería de funciones
description: Obtenga información acerca de la extensión SQL de ingeniería de funciones de Data Distiller para preprocesar datos para un modelado estadístico avanzado. Abarca las técnicas disponibles de extracción, transformación y selección de funciones.
role: Developer
exl-id: 622c8ef3-9651-46b3-ad22-021a93190149
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# Extensión SQL de ingeniería de funciones

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el complemento Data Distiller. Para obtener más información, contacte con su representante de Adobe.

Para satisfacer sus necesidades de ingeniería de funciones, utilice la extensión del transformador SQL para simplificar y automatizar el preprocesamiento de datos. Utilice esta extensión para crear funciones y disfrutar de una experimentación perfecta con diferentes técnicas de ingeniería de funciones, incluida su asociación con modelos. Diseñado para la informática distribuida, puede realizar ingeniería de funciones en grandes conjuntos de datos de forma paralela y escalable, lo que reduce significativamente el tiempo necesario para el preprocesamiento de datos con la extensión SQL de ingeniería de funciones de Data Distiller.

## Resumen de técnica {#technique-overview}

Las funciones de ingeniería de funciones cubren tres áreas principales: Extracción de funciones, Transformación de funciones y Selección de funciones. Cada área incluye funciones específicas diseñadas para extraer, convertir, enfocar y mejorar el preprocesamiento de datos.

### Extracción de funciones {#feature-extraction}

Extraiga información relevante de los datos, especialmente datos de texto, y conviértala en un formato numérico que los modelos compatibles puedan consumir o transformar y derivar conjuntos de datos. Utilice las siguientes funciones para realizar la extracción de características:

- **[Transformador de texto](./feature-transformation.md#textual-transformations)**: convierta los datos de texto en características numéricas.
- **[Contar vectorizador](./feature-transformation.md#countvectorizer)**: transforme una colección de documentos de texto en vectores de recuentos de tokens.
- **[N-gram](./feature-transformation.md#ngram)**: genera secuencias de n-gramas a partir de datos de texto.
- **[Detener el eliminador de palabras](./feature-transformation.md#stopwordsremover)**: filtre las palabras comunes que no tengan un significado significativo.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: Mida la importancia de las palabras de un documento en relación con un corpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)**: desglosa el texto en términos individuales (palabras).
- **[Word2Vec](./feature-transformation.md#word2vec)**: asigne palabras a vectores de tamaño fijo y cree incrustaciones de palabras.

### Transformación de funciones {#feature-transformation}

Además de extraer funciones, utilice los siguientes transformadores generales para preparar sus funciones para modelos estadísticos avanzados y conjuntos de datos derivados. Aplique escalado, normalización o codificación para asegurarse de que las funciones están en la misma escala y tienen una distribución similar.

#### Transformadores generales

A continuación se muestra una lista de herramientas para procesar una amplia gama de tipos de datos para mejorar el flujo de trabajo de preprocesamiento de datos.

- **[Imputador numérico](./feature-transformation.md#numeric-imputer)**: Rellene los valores que faltan en columnas numéricas con un valor especificado, como la media o la mediana.
- **[Imputador de cadena](./feature-transformation.md#string-imputer)**: reemplace los valores de cadena que faltan por un valor especificado, como la cadena más frecuente de la columna.
- **[Ensamblador vectorial](./feature-transformation.md#vector-assembler)**: Combine varias columnas en una sola columna vectorial para preparar los datos para los modelos de aprendizaje automático.
- **[Imputador booleano](./feature-transformation.md#boolean-imputer)**: Rellene los valores booleanos que faltan con un valor especificado, como `true` o `false`.

#### Transformadores numéricos

Aplique estas técnicas para procesar y escalar datos numéricos de forma eficaz para mejorar el rendimiento del modelo.

- **[Binarizer](./feature-transformation.md#binarizer)**: Convierta características continuas en valores binarios basados en un umbral.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: asigne funciones continuas a bloques discretos.
- **[Escalador mín.-máx.](./feature-transformation.md#minmaxscaler)**: cambie el tamaño de las características a un intervalo especificado, normalmente [0, 1].
- **[Escalador Abs máximo](./feature-transformation.md#maxabsscaler)**: cambie las características de escala al rango [-1, 1] sin alterar la dispersión.
- **[Normalizador](./feature-transformation.md#normalizer)**: Normalice los vectores para que tengan la norma de unidad.
- **[Discretizador de cuantílculos](./feature-transformation.md#quantilediscretizer)**: convierta las características continuas en características categóricas agrupándolas en cuantiles.
- **[Escalador estándar](./feature-transformation.md#standardscaler)**: Normalice las características para que tengan una desviación estándar unitaria o una media cero.

#### Transformadores categóricos

Utilice estos transformadores para convertir y codificar datos categóricos en formatos adecuados para los modelos de aprendizaje automático.

- **[Indexador de cadenas](./feature-transformation.md#stringindexer)**: Convierta datos de cadena categóricos en índices numéricos.
- **[Un codificador activo](./feature-transformation.md#onehotencoder)**: asigne datos categóricos a vectores binarios.

### Selección de funciones {#feature-selection}

A continuación, concéntrese en seleccionar un subconjunto de las funciones más importantes del conjunto original. Este proceso ayuda a reducir la dimensionalidad de los datos, lo que facilita el procesamiento de los modelos y mejora el rendimiento general del modelo.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## Implementar la cláusula OPTIONS {#options-clause}

Cuando defina el modelo, utilice la cláusula `OPTIONS` para especificar el algoritmo y sus parámetros. Comience por establecer el parámetro `type` para indicar el algoritmo que está utilizando, como `K-Means`. A continuación, defina los parámetros relevantes en la cláusula `OPTIONS` como pares clave-valor para ajustar el modelo. Si decide no personalizar ciertos parámetros, el sistema aplica la configuración predeterminada. Consulte la documentación pertinente para comprender la función y los valores predeterminados de cada parámetro.

### Pasos siguientes

Después de conocer las técnicas de ingeniería de características descritas en este documento, avance en el documento [Modelos](./models.md). Le guía a través del proceso de creación, formación y administración de modelos de confianza mediante las funciones que ha diseñado. Una vez que se hayan creado los modelos, continúe con el documento [Implementar modelos estadísticos avanzados.](./implement-models/implement-models.md). Este documento sirve como información general, y vincula a guías detalladas para diferentes técnicas de modelado, incluidas la agrupación en clústeres, la clasificación y la regresión. Al seguir estos documentos, aprenderá a configurar e implementar varios modelos de confianza dentro de sus flujos de trabajo SQL y a optimizar sus modelos para un análisis de datos avanzado.
