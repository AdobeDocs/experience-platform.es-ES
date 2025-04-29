---
title: Modelos
description: Modele la administración del ciclo vital con la extensión SQL de Data Distiller. Aprenda a crear, entrenar y administrar modelos estadísticos avanzados mediante SQL, incluidos procesos clave como versiones, evaluación y predicción de modelos, para obtener perspectivas procesables de sus datos.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 09129d9d19816b4d93b4979305f4ad532e5ffde4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 1%

---

# Modelos

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el complemento Data Distiller. Para obtener más información, contacte con su representante de Adobe.

El servicio de consulta ahora es compatible con los procesos principales de creación e implementación de un modelo. Puede utilizar SQL para entrenar el modelo con los datos, evaluar su precisión y, a continuación, utilizar el modelo entrenado para hacer predicciones sobre los nuevos datos. A continuación, puede utilizar el modelo para generalizar a partir de los datos anteriores para tomar decisiones informadas sobre escenarios reales.

Los tres pasos del ciclo de vida del modelo para generar perspectivas procesables son los siguientes:

1. **Formación**: el modelo aprende patrones del conjunto de datos proporcionado. (crear o reemplazar modelo)
2. **Pruebas/Evaluación**: El rendimiento del modelo se evalúa mediante un conjunto de datos independiente. (`model_evaluate`)
3. **Predicción**: el modelo entrenado se usa para hacer predicciones sobre datos nuevos no vistos.

Utilice la extensión SQL del modelo, agregada a la gramática SQL existente, para administrar el ciclo de vida del modelo según sus necesidades comerciales. Este documento cubre el SQL necesario para crear o reemplazar un modelo, entrenar, evaluar, volver a entrenar cuando sea necesario y predecir perspectivas.

## Creación y formación de modelos {#create-and-train}

Aprenda a definir, configurar y entrenar un modelo de aprendizaje automático mediante comandos SQL. El siguiente SQL muestra cómo crear un modelo, aplicar transformaciones de ingeniería de funciones e iniciar el proceso de formación para garantizar que el modelo esté configurado correctamente para un uso futuro. Los siguientes comandos SQL detallan distintas opciones para la creación y administración de modelos:

- **CREAR MODELO**: crea y entrena un nuevo modelo en un conjunto de datos especificado. Si ya existe un modelo con el mismo nombre, este comando devuelve un error.
- **CREAR MODELO SI NO EXISTE**: crea y entrena un nuevo modelo solamente si no existe ya un modelo con el mismo nombre en el conjunto de datos especificado.
- **CREAR O REEMPLAZAR MODELO**: crea y entrena un modelo, reemplazando la última versión de un modelo existente con el mismo nombre en el conjunto de datos especificado.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**Ejemplo**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

Para ayudarle a comprender los componentes y las configuraciones clave del proceso de creación y formación del modelo, las siguientes notas explican el propósito y la función de cada elemento del ejemplo de SQL anterior.

- `<model_alias>`: el alias del modelo es un nombre reutilizable asignado al modelo, al que se puede hacer referencia posteriormente. Es necesario darle un nombre al modelo.
- `transform`: la cláusula de transformación se usa para aplicar transformaciones de ingeniería de características (por ejemplo, codificación de una sola sesión e indexación de cadenas) al conjunto de datos antes de entrenar el modelo. La última cláusula de la instrucción `TRANSFORM` debe ser una `vector_assembler` con una lista de columnas que compondrían las características para la formación de modelos o un tipo derivado de `vector_assembler` (como `max_abs_scaler(feature)`, `standard_scaler(feature)`, etc.). Solo se utilizarán para formación las columnas mencionadas en la última cláusula; se excluirán todas las demás columnas, incluso si están incluidas en la consulta `SELECT`.
- `label = <label-COLUMN>`: columna de etiqueta del conjunto de datos de formación que especifica el objetivo o el resultado que el modelo pretende predecir.
- `training-dataset`: esta sintaxis selecciona los datos utilizados para entrenar el modelo.
- `type = 'LogisticRegression'`: esta sintaxis especifica el tipo de algoritmo de aprendizaje automático que se va a utilizar. Las opciones incluyen `LinearRegression`, `LogisticRegression` y `KMeans`.
- `options`: esta palabra clave proporciona un conjunto flexible de pares clave-valor para configurar el modelo.
   - `Key model_type`: `model_type = '<supported algorithm>'`: especifica el tipo de algoritmo de aprendizaje automático que se va a utilizar. Las opciones admitidas incluyen `LinearRegression`, `LogisticRegression` y `KMeans`.
   - `Key label`: `label = <label_COLUMN>`: define la columna de etiqueta en el conjunto de datos de aprendizaje, que indica el objetivo o el resultado que el modelo pretende predecir.

Utilice SQL para hacer referencia al conjunto de datos utilizado para la formación.

>[!TIP]
>
>Para obtener una referencia completa sobre la cláusula `TRANSFORM`, incluidas las funciones compatibles y el uso en `CREATE MODEL` y `CREATE TABLE`, consulte la cláusula [`TRANSFORM` en la documentación de sintaxis SQL](../sql/syntax.md#transform).

## Actualización de un modelo {#update}

Aprenda a actualizar un modelo de aprendizaje automático existente aplicando nuevas transformaciones de ingeniería de funciones y configurando opciones como el tipo de algoritmo y la columna de etiqueta. Cada actualización crea una nueva versión del modelo, incrementada desde la última versión. Esto garantiza que se realice un seguimiento de los cambios y que el modelo se pueda reutilizar en pasos de predicción o evaluación futuros.

El siguiente ejemplo muestra la actualización de un modelo con nuevas transformaciones y opciones:

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**Ejemplo**

Para ayudarle a comprender el proceso de control de versiones, tenga en cuenta el siguiente comando:

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

Una vez ejecutado este comando, el modelo tiene una nueva versión, como se muestra en la tabla siguiente:

| ID de modelo actualizado | Modelo actualizado | Nueva versión |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

En las siguientes notas se explican los componentes y las opciones clave del flujo de trabajo de actualización de modelos.

- `UPDATE model <model_alias>`: el comando de actualización controla las versiones y crea una nueva versión de modelo incrementada con respecto a la última versión.
- `version`: una palabra clave opcional utilizada solo durante las actualizaciones para especificar explícitamente que se debe crear una nueva versión. Si se omite, el sistema incrementa automáticamente la versión.

### Previsualización y persistencia de funciones transformadas {#preview-transform-output}

Utilice la cláusula `TRANSFORM` dentro de las instrucciones `CREATE TABLE` y `CREATE TEMP TABLE` para obtener una vista previa y mantener la salida de las transformaciones de características antes de la formación del modelo. Esta mejora proporciona visibilidad sobre cómo se aplican las funciones de transformación (como codificación, tokenización y ensamblador vectorial) al conjunto de datos.

Al materializar datos transformados en una tabla independiente, se pueden inspeccionar funciones intermedias, validar la lógica de procesamiento y garantizar la calidad de las funciones antes de crear un modelo. Esto mejora la transparencia en toda la canalización de aprendizaje automático y admite una toma de decisiones más informada durante el desarrollo del modelo.

#### Sintaxis {#syntax}

Utilice la cláusula `TRANSFORM` dentro de una instrucción `CREATE TABLE` o `CREATE TEMP TABLE` como se muestra a continuación:

```sql
CREATE TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

O bien:

```sql
CREATE TEMP TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

**Ejemplo**

Cree una tabla con transformaciones básicas:

```sql
CREATE TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review;
```

Cree una tabla temporal siguiendo pasos adicionales de ingeniería de funciones:

```sql
CREATE TEMP TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

A continuación, consulte el resultado:

```sql
SELECT * FROM ctas_transform_table LIMIT 1;
```

#### Consideraciones importantes {#considerations}

Aunque esta característica mejora la transparencia y admite la validación de características, existen limitaciones importantes que se deben tener en cuenta al utilizar la cláusula `TRANSFORM` fuera de la creación del modelo.

- **Salidas vectoriales**: Si la transformación genera salidas de tipo vectorial, se convierten automáticamente en matrices.
- **Limitación de reutilización de lotes**: las tablas creadas con `TRANSFORM` solo pueden aplicar transformaciones durante la creación de tablas. Los nuevos lotes de datos insertados con `INSERT INTO` se **no se transforman automáticamente**. Para aplicar la misma lógica de transformación a los nuevos datos, debe volver a crear la tabla con una nueva instrucción `CREATE TABLE AS SELECT` (CTAS).
- **Limitación de reutilización del modelo**: las tablas creadas con `TRANSFORM` no se pueden usar directamente en instrucciones `CREATE MODEL`. Debe redefinir la lógica `TRANSFORM` durante la creación del modelo. Las transformaciones que producen salidas de tipo vectorial no son compatibles durante la formación del modelo. Para obtener más información, consulte [Tipos de datos de salida de transformación de características](./feature-transformation.md#available-transformations).

>[!NOTE]
>
>Esta función está diseñada para la inspección y validación. No sustituye a la lógica de canalización reutilizable. Cualquier transformación destinada a la entrada de modelo debe redefinirse explícitamente en el paso de creación del modelo.

## Evaluar modelos {#evaluate-model}

Para garantizar resultados confiables, evalúe la precisión y eficacia del modelo antes de implementarlo para predicciones con la palabra clave `model_evaluate`. La instrucción SQL siguiente especifica un conjunto de datos de prueba, columnas específicas y la versión del modelo para probar el modelo mediante la evaluación de su rendimiento.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test_dataset)
```

La función `model_evaluate` toma `model-alias` como primer argumento y una instrucción `SELECT` flexible como segundo argumento. Query Service ejecuta primero la instrucción `SELECT` y asigna los resultados a la función definida por Adobe (ADF) `model_evaluate`. El sistema espera que los nombres de columna y los tipos de datos del resultado de la instrucción `SELECT` coincidan con los utilizados en el paso de aprendizaje. Estos nombres de columna y tipos de datos se tratan como datos de prueba y datos de etiqueta para su evaluación.

>[!IMPORTANT]
>
>Al evaluar (`model_evaluate`) y predecir (`model_predict`), se utilizan las transformaciones realizadas en el momento de la formación.

## Predecir {#predict}

>[!IMPORTANT]
>
>La selección mejorada de columnas y el alias de `model_predict` se controlan mediante un indicador de características. De manera predeterminada, los campos intermedios como `probability` y `rawPrediction` no se incluyen en el resultado de la predicción.\
>Para habilitar el acceso a estos campos intermedios, ejecute el siguiente comando antes de ejecutar `model_predict`:
>
>`set advanced_statistics_show_hidden_fields=true;`

Utilice la palabra clave `model_predict` para aplicar el modelo y la versión especificados a un conjunto de datos y generar predicciones. Puede seleccionar todas las columnas de salida, elegir unas específicas o asignar alias para mejorar la claridad de salida.

De forma predeterminada, solo se devuelven las columnas base y la predicción final a menos que el indicador de funcionalidad esté habilitado.

```sql
SELECT * FROM model_predict(model-alias, version-number, SELECT col1, col2 FROM dataset);
```

### Seleccionar campos de salida específicos {#select-specific-output-fields}

Cuando el indicador de funcionalidad está habilitado, puede recuperar un subconjunto de campos de la salida `model_predict`. Utilice esto para recuperar resultados intermedios, como probabilidades de predicción, puntuaciones de predicción sin procesar y columnas base de la consulta de entrada.

**Caso 1: devolver todos los campos de salida disponibles**

```sql
SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Caso 2: devolver columnas seleccionadas**

```sql
SELECT a, b, c, probability, predictionCol FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Caso 3: devuelve columnas seleccionadas con alias**

```sql
SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

En cada caso, el `SELECT` externo controla qué campos de resultado se devuelven. Estos incluyen campos base de la consulta de entrada, junto con resultados de predicción como `probability`, `rawPrediction` y `predictionCol`.

### Persistir predicciones utilizando CREATE TABLE o INSERT INTO

Puede mantener las predicciones utilizando &quot;CREATE TABLE AS SELECT&quot; o &quot;INSERT INTO SELECT&quot;, incluidos los resultados de predicción si lo desea.

**Ejemplo: crear tabla con todos los campos de salida de predicción**

```sql
CREATE TABLE scored_data AS SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Ejemplo: Insertar campos de salida seleccionados con alias**

```sql
INSERT INTO scored_data SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

Esto proporciona flexibilidad para seleccionar y mantener solo los campos de salida de predicción y las columnas base relevantes para el análisis descendente o la creación de informes.

## Evaluación y administración de modelos

Utilice el comando `SHOW MODELS` para enumerar todos los modelos disponibles que ha creado. Utilícelo para ver los modelos que se han entrenado y que están disponibles para la evaluación o predicción. Cuando se consulta, la información se obtiene del repositorio de modelos que se actualiza durante la creación del modelo. Los detalles devueltos son: ID del modelo, nombre del modelo, versión, conjunto de datos de origen, detalles del algoritmo, opciones/parámetros, hora de creación/actualización y el usuario que ha creado el modelo.

```sql
SHOW MODELS;
```

Los resultados aparecen en una tabla similar a la que se ve a continuación:

| model-id | model-name | version | source-dataset | tipo | opciones | transformar | campos | created | actualizado | creado por |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1,0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;name&quot;, &quot;gender&quot;\] | 2024-08-14 10:30 | 2024-08-14 11:00 AM | `JohnSnow@adobe.com` |

## Limpieza y mantenimiento de sus modelos

Utilice el comando `DROP MODELS` para eliminar los modelos creados del Registro de modelos. Puede utilizarlo para eliminar modelos obsoletos, no utilizados o no deseados. Esto libera recursos y garantiza que solo se mantengan los modelos relevantes. También puede incluir un nombre de modelo opcional para mejorar la especificidad. Esto solo descarta el modelo con la versión de modelo proporcionada.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Pasos siguientes

Después de leer este documento, ahora comprende la sintaxis SQL base necesaria para crear, entrenar y administrar modelos de confianza mediante Data Distiller. A continuación, explore el documento [Implementación de modelos estadísticos avanzados](./implement-models/implement-models.md) para obtener más información sobre los distintos modelos de confianza disponibles y cómo implementarlos de forma eficaz en los flujos de trabajo de SQL. Si aún no lo ha hecho, asegúrese de revisar el documento [Ingeniería de características](./feature-engineering.md) para asegurarse de que los datos estén óptimamente preparados para la formación de modelos.
