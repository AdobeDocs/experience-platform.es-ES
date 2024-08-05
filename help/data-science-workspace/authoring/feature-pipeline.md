---
keywords: Experience Platform; Tutorial; canalización de características; Data Science Espacio de trabajo; Temas populares
title: Crear una canalización de funciones mediante el SDK de creación de modelos
type: Tutorial
description: Adobe Experience Platform le permite versión y crear canalizaciones de características personalizadas para realizar ingeniería de características a escala a través del Sensei Machine Learning Framework Runtime. Este documento describe las distintas clases que se encuentran en una canalización de funciones y proporciona un tutorial paso a paso para crear una canalización de funciones personalizada mediante el SDK de creación de modelos en PySpark.
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Creación de una canalización de funciones mediante el SDK de creación de modelos

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

>[!IMPORTANT]
>
> Actualmente, las canalizaciones de funciones solo están disponibles a través de la API.

Adobe Experience Platform le permite crear canalizaciones de funciones personalizadas para realizar ingeniería de funciones a escala a través del tiempo de ejecución de Sensei Machine Learning Framework (en adelante, &quot;tiempo de ejecución&quot;).

Este documento describe las distintas clases que se encuentran en una canalización de características y proporciona un tutorial paso a paso para crear una canalización de características personalizada mediante el [SDK](./sdk.md) de creación de modelos en PySpark.

La siguiente flujo de trabajo tiene lugar cuando se ejecuta una canalización de características:

1. El fórmula carga el conjunto de datos en una canalización.
2. El transformación de características se realiza en la conjunto de datos y se vuelve a escribir en Adobe Experience Platform.
3. Los datos transformados se cargan para aprendizaje.
4. La canalización de características define las etapas con el regresor de aumento de gradiente como el modelo elegido.
5. La canalización se utiliza para adaptarse al datos de capacitación y se crea el modelo entrenado.
6. El modelo se transforma con el conjunto de datos de puntuación.
7. Las columnas interesantes de la salida se seleccionan y se guardan de nuevo [!DNL Experience Platform] con los datos asociados.

## Introducción

Para ejecutar un fórmula en cualquier organización, se requiere lo siguiente:
- Un conjunto de datos de entrada.
- El esquema del conjunto de datos.
- Un esquema transformado y un conjunto de datos vacío basado en ese esquema.
- Un esquema de salida y un conjunto de datos vacío basados en ese esquema.

Todos los conjuntos de datos anteriores deben cargarse en la [!DNL Platform] IU. Para configurarlo, utilice el script](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap) de arranque proporcionado por [Adobe Systems.

## Clases de canalización de funciones

En la tabla siguiente se describen las principales clases abstractas que se deben extender para generar una canalización de características:

| Clase abstracta | Descripción |
| -------------- | ----------- |
| DataLoader | Una clase DataLoader proporciona implementación para la recuperación de datos de entrada. |
| DatasetTransformer | Una clase DatasetTransformer proporciona implementaciones para transformar el conjunto de datos de entrada. Puede optar por no proporcionar una clase DatasetTransformer e implementar la lógica de ingeniería de características en la clase FeaturePipelineFactory. |
| FeaturePipelineFactory | Una clase FeaturePipelineFactory crea una canalización de chispa que consta de una serie de transformadores de chispa para realizar ingeniería de funciones. Puede optar por no proporcionar una clase FeaturePipelineFactory e implementar la lógica de ingeniería de características dentro de la clase DatasetTransformer en su lugar. |
| Protector de datos | Una clase DataSaver proporciona la lógica para el almacenamiento de un conjunto de datos de entidades. |

Cuando se inicia un trabajo de canalización de características, el motor en tiempo de ejecución ejecuta primero el DataLoader para cargar los datos de entrada como un DataFrame y, a continuación, modifica el DataFrame ejecutando DatasetTransformer, FeaturePipelineFactory o ambos. Por último, el conjunto de datos de características resultante se almacena a través de DataSaver.

El siguiente diagrama de flujo muestra el orden de ejecución del tiempo de ejecución:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementar las clases de canalización de entidades {#implement-your-feature-pipeline-classes}

En las secciones siguientes se proporcionan detalles y ejemplos sobre la implementación de las clases necesarias para una canalización de funciones.

### Defina las variables en el archivo JSON de configuración {#define-variables-in-the-configuration-json-file}

El archivo JSON de configuración consta de pares clave-valor y está diseñado para que especifique cualquier variable que deba definirse posteriormente durante el tiempo de ejecución. Estos pares clave-valor pueden definir propiedades como la ubicación del conjunto de datos de entrada, el ID del conjunto de datos de salida, el ID de inquilino, los encabezados de columna, etc.

El ejemplo siguiente muestra los pares clave-valor encontrados dentro de un archivo de configuración:

**Ejemplo de JSON de configuración**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```

Puede acceder al JSON de configuración a través de cualquier método de clase que defina `config_properties` como parámetro. Por ejemplo:

**Chispa PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Consulte el archivo pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) proporcionado por el [Espacio de trabajo de ciencia de datos para obtener un ejemplo de configuración más detallado.

### Preparar los datos de entrada con DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader es responsable de la recuperación y el filtrado de los datos de entrada. Su implementación de DataLoader debe extender la clase `DataLoader` abstracta y anular el método `load`abstracto.

En el ejemplo siguiente se recupera un [!DNL Platform] conjunto de datos por ID y se devuelve como DataFrame, donde el conjunto de datos ID (`dataset_id`) es un Propiedad definido en el archivo de configuración.

**Ejemplo de PySpark**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

    query_options = get_query_options(spark.sparkContext)

    pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
        .option(query_options.userToken(), user_token) \
        .option(query_options.serviceToken(), service_token) \
        .option(query_options.imsOrg(), org_id) \
        .option(query_options.apiKey(), api_key) \
        .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
        .option(query_options.datasetId(), dataset_id) \
        .load()
    pd.show()

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### Transformar un conjunto de datos con DatasetTransformer {#transform-a-dataset-with-datasettransformer}

Un DatasetTransformer proporciona la lógica para transformar un DataFrame de entrada y devuelve un nuevo DataFrame derivado. Esta clase se puede implementar para trabajar de forma cooperativa con una FeaturePipelineFactory, trabajar como el único componente de ingeniería de características o puede optar por no implementar esta clase.

El ejemplo siguiente amplía la clase DatasetTransformer:

**Ejemplo de PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### Diseñe funciones de datos con FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Un FeaturePipelineFactory le permite implementar su lógica de ingeniería de características definiendo y encadenando una serie de Spark Transformers a través de un Spark Pipeline. Esta clase se puede implementar para trabajar en cooperación con un DatasetTransformer, trabajar como el único componente de ingeniería de características o puede optar por no implementar esta clase.

En el ejemplo siguiente se amplía la clase FeaturePipelineFactory:

**Ejemplo de PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### Almacene su conjunto de datos de características con DataSaver {#store-your-feature-dataset-with-datasaver}

DataSaver es responsable de almacenar los conjuntos de datos de características resultantes en una ubicación de almacenamiento. La implementación de DataSaver debe extender la clase abstracta `DataSaver` y reemplazar el método abstracto `save`.

El ejemplo siguiente amplía la clase DataSaver, que almacena datos en un conjunto de datos [!DNL Platform] por identificador, donde el identificador del conjunto de datos (`featureDatasetId`) y el identificador de inquilino (`tenantId`) son propiedades definidas en la configuración.

**Ejemplo de PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```


### Especifique los nombres de las clases implementadas en el archivo de aplicación {#specify-your-implemented-class-names-in-the-application-file}

Ahora que las clases de canalización de entidades están definidas e implementadas, debe especificar los nombres de las clases en el archivo YAML de aplicación.

En los ejemplos siguientes se especifican los nombres de clase implementados:

**Ejemplo de PySpark**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## Crear motor de canalización de características mediante la API {#create-feature-pipeline-engine-api}

Ahora que ha creado su canalización de características, debe crear una imagen de Docker para realizar una llamada a los puntos finales de canalización de características en la [!DNL Sensei Machine Learning] API. Necesita un URL de imagen de Docker para realizar una llamada a los puntos finales de canalización de características.

>[!TIP]
>
>Si no tiene un URL de Docker, visita los archivos de origen del [paquete en una tutorial de fórmula](../models-recipes/package-source-files-recipe.md) para obtener un tutorial paso a paso sobre la creación de un host URL de Docker.

Opcionalmente, también puede usar la siguiente colección de Postman para ayudar a completar el flujo de trabajo de API de canalización de características:

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### Crear un motor de canalización de características {#create-engine-api}

Una vez que tenga la ubicación de la imagen de Docker, puede [crear un motor](../api/engines.md#feature-pipeline-docker) de canalización de características mediante la [!DNL Sensei Machine Learning] API realizando un POST a `/engines`. Si crea correctamente un motor de canalización de características, recibirá un identificador único de motor (`id`). Asegúrese de guardar este valor antes de continuar.

### Crear una instancia de MLI {#create-mlinstance}

Con su `engineID` recién creada, debe [crear una MLIstance](../api/mlinstances.md#create-an-mlinstance) realizando una solicitud de POST al extremo `/mlInstance`. Una respuesta correcta devuelve una carga útil que contiene los detalles de la MLInstance recién creada, incluido su identificador único (`id`) utilizado en la siguiente llamada de API.

### Crear un experimento {#create-experiment}

Siguiente, debe [crear un Experimento](../api/experiments.md#create-an-experiment). Para crear un experimento, necesita tener su identificador único de MLIstance (`id`) y realizar una solicitud de POST al extremo `/experiment`. Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento recién creado, incluido su identificador único (`id`) utilizado en la siguiente llamada de API.

### Especifique la tarea de canalización de la función de ejecución del experimento {#specify-feature-pipeline-task}

Después de crear un experimento, debe cambiar el modo del experimento a `featurePipeline`. Para cambiar el modo, haga un POST adicional a [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) con su `EXPERIMENT_ID` y envíe `{ "mode":"featurePipeline"}` en el cuerpo para especificar una ejecución del experimento de canalización de características.

Una vez finalizado, realice una solicitud de GET a `/experiments/{EXPERIMENT_ID}` para [recuperar el estado del experimento](../api/experiments.md#retrieve-specific) y espere a que se complete la actualización del estado del experimento.

### Especifique la tarea de formación Ejecución del experimento {#training}

Siguiente, debe [especificar la aprendizaje ejecutar tarea](../api/experiments.md#experiment-training-scoring). Haga una POST y `experiments/{EXPERIMENT_ID}/runs` en el cuerpo establezca el modo y `train` envíe una matriz de tareas que contengan sus parámetros aprendizaje. Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento solicitado.

Una vez finalizado, realice una solicitud de GET a `/experiments/{EXPERIMENT_ID}` para [recuperar el estado del experimento](../api/experiments.md#retrieve-specific) y espere a que se complete la actualización del estado del experimento.

### Especificar la tarea de puntuación de ejecución de experimento {#scoring}

>[!NOTE]
>
> Para completar este paso, debe tener al menos una ejecución de formación correcta asociada a su experimento.

Después de una ejecución de aprendizaje correcta, debe [especificar el tarea](../api/experiments.md#experiment-training-scoring) de ejecución de puntuación. Realice una POST y `experiments/{EXPERIMENT_ID}/runs` en el cuerpo establezca el `mode` atributo en &quot;puntuación&quot;. Esto inicia la ejecución del experimento de puntuación.

Una vez finalizado, realice una solicitud de GET a `/experiments/{EXPERIMENT_ID}` para [recuperar el estado del experimento](../api/experiments.md#retrieve-specific) y espere a que se complete la actualización del estado del experimento.

Una vez finalizada la puntuación, la canalización de funciones debe estar operativa.

## Pasos siguientes {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Al leer este documento, ha creado una canalización de funciones mediante el SDK de creación de modelos, ha creado una imagen de Docker y ha utilizado la URL de imagen de Docker para crear un modelo de canalización de funciones mediante la API [!DNL Sensei Machine Learning]. Ya está listo para continuar transformando conjuntos de datos y extrayendo características de datos a escala mediante [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
