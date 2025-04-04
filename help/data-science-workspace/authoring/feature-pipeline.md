---
keywords: Experience Platform;Tutorial;canalización de características;Workspace de ciencia de datos;temas populares
title: Creación de una canalización de funciones mediante la SDK de creación de modelos
type: Tutorial
description: Adobe Experience Platform le permite crear canalizaciones de funciones personalizadas para realizar ingeniería de funciones a escala a través del tiempo de ejecución de Sensei Machine Learning Framework. En este documento se describen las distintas clases que se encuentran en una canalización de funciones y se proporciona un tutorial paso a paso para crear una canalización de funciones personalizada mediante la SDK de creación de modelos en PySpark.
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Creación de una canalización de funciones mediante la SDK de creación de modelos

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

>[!IMPORTANT]
>
> Actualmente, las canalizaciones de funciones solo están disponibles a través de la API.

Adobe Experience Platform le permite crear canalizaciones de funciones personalizadas para realizar ingeniería de funciones a escala a través del tiempo de ejecución de Sensei Machine Learning Framework (en adelante, &quot;tiempo de ejecución&quot;).

En este documento se describen las distintas clases que se encuentran en una canalización de características y se proporciona un tutorial paso a paso para crear una canalización de características personalizada mediante [Model Authoring SDK](./sdk.md) en PySpark.

El siguiente flujo de trabajo tiene lugar cuando se ejecuta una canalización de funciones:

1. La fórmula carga el conjunto de datos en una canalización.
2. La transformación de funciones se realiza en el conjunto de datos y se vuelve a escribir en Adobe Experience Platform.
3. Los datos transformados se cargan para la formación.
4. La tubería de funciones define las etapas con el Regresor de ampliación de degradado como modelo elegido.
5. La canalización se utiliza para ajustar los datos de formación y se crea el modelo entrenado.
6. El modelo se transforma con el conjunto de datos de puntuación.
7. A continuación, se seleccionan y se guardan en [!DNL Experience Platform] columnas interesantes de la salida con los datos asociados.

## Introducción

Para ejecutar una fórmula en cualquier organización, se requiere lo siguiente:
- Un conjunto de datos de entrada.
- El esquema del conjunto de datos.
- Un esquema transformado y un conjunto de datos vacío basado en ese esquema.
- Un esquema de salida y un conjunto de datos vacío basado en ese esquema.

Todos los conjuntos de datos anteriores deben cargarse en la interfaz de usuario de [!DNL Experience Platform]. Para configurarlo, use el [script de bootstrap](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap) proporcionado por Adobe.

## Clases de canalización de funciones

En la tabla siguiente se describen las principales clases abstractas que se deben extender para generar una canalización de características:

| Clase abstracta | Descripción |
| -------------- | ----------- |
| DataLoader | Una clase DataLoader proporciona implementación para la recuperación de datos de entrada. |
| DatasetTransformer | Una clase DatasetTransformer proporciona implementaciones para transformar el conjunto de datos de entrada. Puede optar por no proporcionar una clase DatasetTransformer e implementar la lógica de ingeniería de características en la clase FeaturePipelineFactory. |
| FeaturePipelineFactory | Una clase FeaturePipelineFactory crea una canalización de chispa que consta de una serie de transformadores de chispa para realizar ingeniería de funciones. Puede optar por no proporcionar una clase FeaturePipelineFactory e implementar la lógica de ingeniería de características dentro de la clase DatasetTransformer en su lugar. |
| DataSaver | Una clase DataSaver proporciona la lógica para el almacenamiento de un conjunto de datos de características. |

Cuando se inicia un trabajo de canalización de características, el motor en tiempo de ejecución ejecuta primero DataLoader para cargar datos de entrada como DataFrame y, a continuación, modifica DataFrame ejecutando DatasetTransformer, FeaturePipelineFactory o ambos. Por último, el conjunto de datos de características resultante se almacena mediante DataSaver.

El siguiente diagrama de flujo muestra el orden de ejecución de Runtime:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementación de las clases de canalización de funciones {#implement-your-feature-pipeline-classes}

En las secciones siguientes se proporcionan detalles y ejemplos sobre la implementación de las clases necesarias para una canalización de funciones.

### Defina las variables en el archivo JSON de configuración {#define-variables-in-the-configuration-json-file}

El archivo JSON de configuración consta de pares clave-valor y está diseñado para que especifique cualquier variable que se defina posteriormente durante el tiempo de ejecución. Estos pares clave-valor pueden definir propiedades como la ubicación del conjunto de datos de entrada, el ID del conjunto de datos de salida, el ID de inquilino, los encabezados de columna, etc.

En el siguiente ejemplo se muestran pares de clave-valor encontrados en un archivo de configuración:

**Ejemplo de configuración JSON**

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

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Consulte el archivo [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) proporcionado por Data Science Workspace para ver un ejemplo de configuración más detallado.

### Preparar los datos de entrada con DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader es responsable de la recuperación y el filtrado de los datos de entrada. La implementación de DataLoader debe extender la clase abstracta `DataLoader` y reemplazar el método abstracto `load`.

El ejemplo siguiente recupera un conjunto de datos [!DNL Experience Platform] por identificador y lo devuelve como un DataFrame, donde el identificador del conjunto de datos (`dataset_id`) es una propiedad definida en el archivo de configuración.

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

Un DataSetTransformer proporciona la lógica para transformar un DataFrame de entrada y devuelve un nuevo DataFrame derivado. Esta clase se puede implementar para trabajar conjuntamente con FeaturePipelineFactory, como el único componente de ingeniería de funciones o puede optar por no implementar esta clase.

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

### Funciones de datos de ingeniero con FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory permite implementar la lógica de ingeniería de funciones definiendo y encadenando una serie de transformadores de chispa a través de una canalización de chispa. Esta clase se puede implementar para trabajar de forma cooperativa con DatasetTransformer, como el único componente de ingeniería de características o puede optar por no implementar esta clase.

El ejemplo siguiente amplía la clase FeaturePipelineFactory:

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

El ejemplo siguiente amplía la clase DataSaver, que almacena datos en un conjunto de datos [!DNL Experience Platform] por identificador, donde el identificador del conjunto de datos (`featureDatasetId`) y el identificador de inquilino (`tenantId`) son propiedades definidas en la configuración.

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


### Especifique los nombres de clase implementados en el archivo de aplicación {#specify-your-implemented-class-names-in-the-application-file}

Ahora que las clases de canalización de funciones están definidas e implementadas, debe especificar los nombres de las clases en el archivo YAML de la aplicación.

Los ejemplos siguientes especifican nombres de clase implementados:

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

## Cree su motor de canalización de funciones mediante la API {#create-feature-pipeline-engine-api}

Ahora que ha creado su canalización de características, debe crear una imagen Docker para realizar una llamada a los extremos de la canalización de características en la API [!DNL Sensei Machine Learning]. Necesita una URL de imagen de Docker para realizar una llamada a los extremos de la canalización de funciones.

>[!TIP]
>
>Si no tiene una URL de Docker, visite el tutorial [Empaquetar archivos de origen en una fórmula](../models-recipes/package-source-files-recipe.md) para ver un tutorial paso a paso sobre la creación de una URL de host de Docker.

De forma opcional, también puede utilizar la siguiente colección de Postman para ayudarle a completar el flujo de trabajo de la API de la canalización de funciones:

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### Creación de un motor de canalización de funciones {#create-engine-api}

Una vez que tenga la ubicación de la imagen Docker, podrá [crear un motor de canalización de características](../api/engines.md#feature-pipeline-docker) mediante la API [!DNL Sensei Machine Learning] realizando una PUBLICACIÓN en `/engines`. Si crea correctamente un motor de canalización de características, recibirá un identificador único de motor (`id`). Asegúrese de guardar este valor antes de continuar.

### Crear una instancia de MLI {#create-mlinstance}

Con su `engineID` recién creada, debe [crear una MLIstance](../api/mlinstances.md#create-an-mlinstance) realizando una petición POST al extremo `/mlInstance`. Una respuesta correcta devuelve una carga útil que contiene los detalles de la MLInstance recién creada, incluido su identificador único (`id`) utilizado en la siguiente llamada de API.

### Crear un experimento {#create-experiment}

A continuación, debe [crear un experimento](../api/experiments.md#create-an-experiment). Para crear un experimento, necesita tener su identificador único de MLIstance (`id`) y realizar una petición POST al extremo `/experiment`. Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento recién creado, incluido su identificador único (`id`) utilizado en la siguiente llamada de API.

### Especifique la tarea de canalización de la función de ejecución del experimento {#specify-feature-pipeline-task}

Después de crear un experimento, debe cambiar el modo del experimento a `featurePipeline`. Para cambiar el modo, realice una PUBLICACIÓN adicional en [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) con su `EXPERIMENT_ID` y envíe `{ "mode":"featurePipeline"}` en el cuerpo para especificar una ejecución del experimento de canalización de características.

Una vez finalizado, realice una petición GET a `/experiments/{EXPERIMENT_ID}` para [recuperar el estado del experimento](../api/experiments.md#retrieve-specific) y espere a que se complete la actualización del estado del experimento.

### Especifique la tarea de formación Ejecución del experimento {#training}

A continuación, debe [especificar la tarea de ejecución de formación](../api/experiments.md#experiment-training-scoring). Realice una PUBLICACIÓN en `experiments/{EXPERIMENT_ID}/runs` y en el cuerpo establezca el modo en `train` y envíe una matriz de tareas que contengan los parámetros de formación. Una respuesta correcta devuelve una carga útil que contiene los detalles del experimento solicitado.

Una vez finalizado, realice una petición GET a `/experiments/{EXPERIMENT_ID}` para [recuperar el estado del experimento](../api/experiments.md#retrieve-specific) y espere a que se complete la actualización del estado del experimento.

### Especificar la tarea de puntuación de ejecución de experimento {#scoring}

>[!NOTE]
>
> Para completar este paso, debe tener al menos una ejecución de formación correcta asociada a su experimento.

Después de una ejecución de formación correcta, debe [especificar la tarea de ejecución de puntuación](../api/experiments.md#experiment-training-scoring). Realice una PUBLICACIÓN en `experiments/{EXPERIMENT_ID}/runs` y en el cuerpo establezca el atributo `mode` en &quot;puntuación&quot;. Esto inicia la ejecución del experimento de puntuación.

Una vez finalizado, realice una petición GET a `/experiments/{EXPERIMENT_ID}` para [recuperar el estado del experimento](../api/experiments.md#retrieve-specific) y espere a que se complete la actualización del estado del experimento.

Una vez finalizada la puntuación, la canalización de funciones debe estar operativa.

## Pasos siguientes {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Al leer este documento, ha creado una canalización de funciones mediante Model Authoring SDK, ha creado una imagen Docker y ha utilizado la URL de imagen Docker para crear un modelo de canalización de funciones mediante la API [!DNL Sensei Machine Learning]. Ya está listo para continuar transformando conjuntos de datos y extrayendo características de datos a escala mediante [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
