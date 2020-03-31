---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: Creación de una canalización de funciones
topic: Tutorial
translation-type: tm+mt
source-git-commit: b9b0578a43182650b3cfbd71f46bcb817b3b0cda

---


# Creación de una canalización de funciones

Adobe Experience Platform le permite crear y crear tuberías de funciones personalizadas para realizar ingeniería de funciones a escala a través de Sensei Machine Learning Framework Runtime (en adelante, &quot;Runtime&quot;).

Este documento describe las distintas clases que se encuentran en una canalización de funciones y proporciona un tutorial paso a paso para crear una canalización de funciones personalizada mediante el SDK [de creación de](./sdk.md) modelos en PySpark y Spark.

El tutorial cubre los siguientes pasos:
- [Implemente sus clases de Feature Pipeline](#implement-your-feature-pipeline-classes)
   - [Definir variables en un archivo de configuración](#define-variables-in-the-configuration-json-file)
   - [Preparación de los datos de entrada con DataLoader](#prepare-the-input-data-with-dataloader)
   - [Transformar un conjunto de datos con DatasetTransformer](#transform-a-dataset-with-datasettransformer)
   - [Funciones de datos de ingeniero con FeaturePipelineFactory](#engineer-data-features-with-featurepipelinefactory)
   - [Almacenar el conjunto de datos de funciones con DataSaver](#store-your-feature-dataset-with-datasaver)
   - [Especifique los nombres de clase implementados en el archivo de la aplicación](#specify-your-implemented-class-names-in-the-application-file)
- [Generar el artefacto binario](#build-the-binary-artifact)
- [Creación de un motor de canalización de funciones mediante la API](#create-a-feature-pipeline-engine-using-the-api)

## Clases de canalización de funciones

En la tabla siguiente se describen las principales clases abstractas que debe ampliar para crear una canalización de funciones:

| Clase abstracta | Descripción |
| -------------- | ----------- |
| DataLoader | Una clase DataLoader proporciona implementación para la recuperación de datos de entrada. |
| DatasetTransformer | Una clase DatasetTransformer proporciona implementaciones para transformar el conjunto de datos de entrada. Puede optar por no proporcionar una clase DatasetTransformer e implementar la lógica de ingeniería de funciones en la clase FeaturePipelineFactory. |
| FeaturePipelineFactory | Una clase FeaturePipelineFactory construye una tubería Spark que consiste en una serie de transformadores Spark para realizar ingeniería de funciones. Puede optar por no proporcionar una clase FeaturePipelineFactory e implementar la lógica de ingeniería de funciones en la clase DatasetTransformer. |
| DataSaver | Una clase DataSaver proporciona la lógica para el almacenamiento de un conjunto de datos de funciones. |

Cuando se inicia un trabajo de Canalización de funciones, el motor de ejecución ejecutará primero DataLoader para cargar los datos de entrada como DataFrame y, a continuación, modifica el DataFrame ejecutando DatasetTransformer, FeaturePipelineFactory o ambos. Por último, el conjunto de datos de características resultante se almacena a través de DataSaver.

El siguiente diagrama de flujo muestra el orden de ejecución del motor de ejecución:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implemente sus clases de Feature Pipeline

Las siguientes secciones proporcionan detalles y ejemplos sobre la implementación de las clases requeridas para una canalización de funciones.

### Definición de variables en el archivo JSON de configuración

El archivo JSON de configuración consta de pares clave-valor y está diseñado para que pueda especificar las variables que se definirán posteriormente durante el tiempo de ejecución. Estos pares clave-valor pueden definir propiedades como ubicación del conjunto de datos de entrada, ID del conjunto de datos de salida, ID del inquilino, encabezados de columna, etc.

En el siguiente ejemplo se muestran los pares clave-valor que se encuentran dentro de un archivo de configuración. Expanda el ejemplo para ver los detalles:


**ejemplo de configuración JSON**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
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



Puede acceder a la configuración JSON a través de cualquier método de clase que se defina `configProperties` como parámetro. Por ejemplo:

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### Preparación de los datos de entrada con DataLoader

DataLoader es responsable de la recuperación y el filtrado de los datos de entrada. La implementación de DataLoader debe ampliar la clase abstracta `DataLoader` y anular el método abstracto `load`.

En el ejemplo siguiente se recupera un conjunto de datos de la plataforma por ID y se devuelve como DataFrame, donde el ID del conjunto de datos (`datasetId`) es una propiedad definida en el archivo de configuración. Expanda cada ejemplo para ver los detalles:


**Ejemplo de PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Ejemplo de Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### Transformar un conjunto de datos con DatasetTransformer

DatasetTransformer proporciona la lógica para transformar un DataFrame de entrada y devuelve un DataFrame nuevo derivado. Esta clase se puede implementar para trabajar de forma conjunta con FeaturePipelineFactory, trabajar como el único componente de ingeniería de funciones o puede elegir no implementar esta clase.

En el siguiente ejemplo se amplía la clase DatasetTransformer. Expanda cada ejemplo para ver los detalles:


**Ejemplo de PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Ejemplo de Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Funciones de datos de ingeniero con FeaturePipelineFactory

FeaturePipelineFactory le permite implementar la lógica de ingeniería de características mediante la definición y la agrupación de una serie de transformadores de chispa a través de una tubería de chispa. Esta clase se puede implementar para trabajar de forma conjunta con DatasetTransformer, trabajar como el único componente de ingeniería de funciones o puede elegir no implementar esta clase.

El siguiente ejemplo amplía la clase FeaturePipelieFactory e implementa una serie de transformadores Spark como varias etapas en una tubería Spark. Expanda cada ejemplo para ver los detalles:


**Ejemplo de PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Ejemplo de Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### Almacenar el conjunto de datos de funciones con DataSaver

DataSaver se encarga de almacenar los conjuntos de datos de funciones resultantes en una ubicación de almacenamiento. La implementación de DataSaver debe ampliar la clase abstracta `DataSaver` y anular el método abstracto `save`.

El ejemplo siguiente amplía la clase DataSaver que almacena datos en un conjunto de datos de la plataforma por ID, donde el ID del conjunto de datos (`featureDatasetId`) y el ID del inquilino (`tenantId`) son propiedades definidas en el archivo de configuración. Expanda cada ejemplo para ver los detalles:


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




**Ejemplo de Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### Especifique los nombres de clase implementados en el archivo de la aplicación

Ahora que las clases de Feature Pipeline están definidas e implementadas, debe especificar los nombres de las clases en el archivo de la aplicación.

Los siguientes ejemplos especifican nombres de clase implementados. Expanda el ejemplo para ver los detalles:


**Ejemplo de PySpark**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Ejemplo de Spark**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## Generar el artefacto binario

Ahora que las clases de tuberías de funciones están implementadas, puede compilarlas en un artefacto binario que puede utilizarse para crear una tubería de funciones a través de llamadas de API.

**PySpark**

Para crear una canalización de funciones PySpark, ejecute la secuencia de comandos de Python ubicada en el directorio raíz del SDK de creación de modelos. `setup.py`

>[!NOTE] La creación de una canalización de funciones PySpark requiere que tenga Python 3 instalado en su equipo.

```shell
python3 setup.py bdist_egg
```

La generación exitosa de la tubería de características generará un `.egg` artefacto en el `/dist` directorio, este artefacto se utiliza para crear una tubería de características.

**Spark**

Para crear una canalización de funciones de Spark, ejecute el siguiente comando de consola en el directorio raíz del SDK de creación de modelos:

>[!NOTE] La creación de una tubería de función de chispa requiere que tenga Scala y sbt instalados en su equipo.

```shell
mvn clean install
```

La generación exitosa de la tubería de características generará un `.jar` artefacto en el `/dist` directorio, este artefacto se utiliza para crear una tubería de características.

## Creación de un motor de canalización de funciones mediante la API

Ahora que ha creado la tubería de características y el artefacto binario, puede [crear un motor de tuberías de funciones con la API](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)de aprendizaje automático Sensei. La creación correcta de un motor de canalización de funciones le proporcionará un identificador de motor como parte del cuerpo de respuesta, asegúrese de guardar este valor antes de continuar con los pasos siguientes.

## Pasos siguientes

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

Al leer este documento, ha creado una tubería de funciones con el SDK de creación de modelos, ha creado un artefacto binario y ha utilizado el artefacto para crear un motor de tuberías de funciones mediante una llamada de API. Ya está listo para [crear un modelo](../api/mlinstances.md#create-an-mlinstance) de tubería de funciones con el motor y el inicio recién creados que transforman conjuntos de datos y extraen funciones de datos a escala.