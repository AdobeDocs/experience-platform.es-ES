---
title: Modelos
description: Modele la administración del ciclo vital con la extensión SQL de Data Distiller. Aprenda a crear, entrenar y administrar modelos estadísticos avanzados mediante SQL, incluidos procesos clave como versiones, evaluación y predicción de modelos, para obtener perspectivas procesables de sus datos.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# Modelos

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el complemento Data Distiller. Para obtener más información, contacte con su representante de Adobe.

El servicio de consulta ahora es compatible con los procesos principales de creación e implementación de un modelo. Puede utilizar SQL para entrenar el modelo con los datos, evaluar su precisión y, a continuación, aplicar el modelo de tren para hacer predicciones sobre los nuevos datos. A continuación, puede utilizar el modelo para generalizar a partir de los datos anteriores para tomar decisiones informadas sobre escenarios reales.

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

## Actualización de un modelo {#update}

Aprenda a actualizar un modelo de aprendizaje automático existente aplicando nuevas transformaciones de ingeniería de funciones y configurando opciones como el tipo de algoritmo y la columna de etiqueta. El siguiente SQL muestra cómo aumentar el número de versión del modelo con cada actualización y asegurarse de que se realiza un seguimiento de los cambios para que el modelo se pueda reutilizar en pasos de predicción o evaluación futuros.

```sql
UPDATE model <model_alias> transform( one_hot_encoder(NAME) ohe_name, string_indexer(gender) gendersi) options ( type = 'LogisticRegression', label = <label-COLUMN>, ) ASSELECT col1,
       col2,
       col3
FROM   training-dataset.
```

Para ayudarle a comprender cómo administrar las versiones de los modelos y aplicar las transformaciones de forma eficaz, las siguientes notas explican los componentes y las opciones clave del flujo de trabajo de actualización de modelos.

- `UPDATE model <model_alias>`: el comando de actualización controla las versiones y aumenta el número de versión del modelo con cada actualización.
- `version`: una palabra clave opcional utilizada solo durante las actualizaciones para crear una nueva versión del modelo.

## Evaluar modelos {#evaluate-model}

Para garantizar resultados confiables, evalúe la precisión y eficacia del modelo antes de implementarlo para predicciones con la palabra clave `model_evaluate`. La instrucción SQL siguiente especifica un conjunto de datos de prueba, columnas específicas y la versión del modelo para probar el modelo mediante la evaluación de su rendimiento.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

La función `model_evaluate` toma `model-alias` como primer argumento y una instrucción `SELECT` flexible como segundo argumento. El servicio de consultas ejecuta primero la instrucción `SELECT` y asigna los resultados a la función definida por el Adobe (ADF) `model_evaluate`. El sistema espera que los nombres de columna y los tipos de datos del resultado de la instrucción `SELECT` coincidan con los utilizados en el paso de aprendizaje. Estos nombres de columna y tipos de datos se tratan como datos de prueba y datos de etiqueta para su evaluación.

>[!IMPORTANT]
>
>Al evaluar (`model_evaluate`) y predecir (`model_predict`), se utilizan las transformaciones realizadas en el momento de la formación.

## Predecir {#predict}

A continuación, utilice la palabra clave `model_predict` para aplicar el modelo y la versión especificados a un conjunto de datos y generar predicciones para las columnas seleccionadas. El siguiente SQL muestra este proceso y cómo prever los resultados utilizando el alias y la versión del modelo.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` acepta el alias del modelo como primer argumento y una instrucción `SELECT` flexible como segundo argumento. El servicio de consultas ejecuta primero la instrucción `SELECT` y asigna los resultados al archivo ADF `model_predict`. El sistema espera que los nombres de columna y los tipos de datos del resultado de la instrucción `SELECT` coincidan con los del paso de aprendizaje. Estos datos se utilizan para puntuar y generar predicciones.

>[!IMPORTANT]
>
>Al evaluar (`model_evaluate`) y predecir (`model_predict`), se utilizan las transformaciones realizadas en el momento de la formación.

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
