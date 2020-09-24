---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics;testing
solution: Experience Platform
title: Guía para desarrolladores de SDK
topic: Overview
description: El SDK de creación de modelos le permite desarrollar fórmulas de aprendizaje automático personalizadas y tuberías de funciones que se pueden utilizar en Adobe Experience Platform Data Science Workspace, proporcionando plantillas implementables en PySpark y Spark (Scala).
translation-type: tm+mt
source-git-commit: e1b8bc378c2f72862c0c28e44dceb8a35e44a29e
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 1%

---


# Guía para desarrolladores de SDK

El SDK de creación de modelos le permite desarrollar fórmulas de aprendizaje automático personalizadas y tuberías de funciones que se pueden utilizar en [!DNL Adobe Experience Platform] Área de trabajo de ciencias de datos, proporcionando plantillas implementables en [!DNL PySpark] y [!DNL Spark (Scala)].

Este documento proporciona información sobre las distintas clases que se encuentran en el SDK de creación de modelos.

## DataLoader {#dataloader}

La clase DataLoader encapsula todo lo relacionado con la recuperación, filtrado y devolución de datos de entrada sin procesar. Algunos ejemplos de datos de entrada son los de capacitación, puntuación o ingeniería de funciones. Los cargadores de datos extienden la clase abstracta `DataLoader` y deben anular el método abstracto `load`.

**PySpark**

En la tabla siguiente se describen los métodos abstractos de una clase PySpark Data Loader:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>Carga y devolución de datos de plataforma como un DataFrame de Pandas</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code>spark</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

En la tabla siguiente se describen los métodos abstractos de una clase [!DNL Spark] Data Loader:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>Carga y devolución de datos de plataforma como marco de datos</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code>sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Carga de datos desde un [!DNL Platform] conjunto de datos {#load-data-from-a-platform-dataset}

En el ejemplo siguiente se recuperan [!DNL Platform] los datos por ID y se devuelve un DataFrame, donde el ID del conjunto de datos (`datasetId`) es una propiedad definida en el archivo de configuración.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

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

        # return as DataFrame
        return pd
```

**Chispa (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## DataSaver {#datasaver}

La clase DataSaver encapsula todo lo relacionado con el almacenamiento de datos de salida, incluidos los datos de puntuación o ingeniería de características. Los responsables de guardar datos amplían la clase abstracta `DataSaver` y deben anular el método abstracto `save`.

**PySpark**

En la tabla siguiente se describen los métodos abstractos de una clase [!DNL PySpark] Data Saver:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>Recibir datos de salida como marco de datos y almacenarlos en un conjunto de datos de plataforma</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code>dataframe</code>:: Datos que se almacenarán en forma de marco de datos</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Chispa (Scala)**

En la tabla siguiente se describen los métodos abstractos de una clase [!DNL Spark] Data Saver:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>Recibir datos de salida como marco de datos y almacenarlos en un conjunto de datos de plataforma</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code>dataFrame</code>:: Datos que se almacenarán en forma de marco de datos</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Guardar datos en un [!DNL Platform] conjunto de datos {#save-data-to-a-platform-dataset}

Para almacenar datos en un [!DNL Platform] conjunto de datos, las propiedades deben proporcionarse o definirse en el archivo de configuración:

- Un ID [!DNL Platform] de conjunto de datos válido al que se almacenarán los datos
- El ID de inquilino que pertenece a su organización

Los siguientes ejemplos almacenan datos (`prediction`) en un [!DNL Platform] conjunto de datos, donde la ID del conjunto de datos (`datasetId`) y la ID del inquilino (`tenantId`) son propiedades definidas dentro del archivo de configuración.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Chispa (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

La clase DatasetTransformer modifica y transforma la estructura de un conjunto de datos. El componente [!DNL Sensei Machine Learning Runtime] no requiere que se defina y se implementa según sus necesidades.

Con respecto a una canalización de funciones, los transformadores de conjuntos de datos se pueden utilizar de manera conjunta con una fábrica de canalizaciones de funciones para preparar datos para la ingeniería de funciones.

**PySpark**

La siguiente tabla describe los métodos de clase de una clase de transformador de conjuntos de datos PySpark:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>Toma un conjunto de datos como entrada y genera un nuevo conjunto de datos derivado</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code>dataset</code>:: El conjunto de datos de entrada para la transformación</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Chispa (Scala)**

En la tabla siguiente se describen los métodos abstractos de una clase de transformador de [!DNL Spark] conjuntos de datos:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>Toma un conjunto de datos como entrada y genera un nuevo conjunto de datos derivado</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code>dataset</code>:: El conjunto de datos de entrada para la transformación</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

La clase FeaturePipelineFactory contiene algoritmos de extracción de funciones y define las etapas de una tubería de funciones de inicio a fin.

**PySpark**

En la tabla siguiente se describen los métodos de clase de PySpark FeaturePipelineFactory:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>Crear y devolver una tubería de spark que contenga una serie de transformadores de chispa</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Chispa (Scala)**

En la tabla siguiente se describen los métodos de clase de un [!DNL Spark] FeaturePipelineFactory:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>createPipeline(configProperties)</code></p>
                <p>Crear y devolver una canalización que contenga una serie de transformadores</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Asignación de propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

La clase PipelineFactory encapsula métodos y definiciones para la formación y puntuación de modelos, donde la lógica y los algoritmos de formación se definen en forma de [!DNL Spark] Canalización.

**PySpark**

En la tabla siguiente se describen los métodos de clase de PySpark PipelineFactory:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(self, configProperties)</code></p>
                <p>Crear y devolver una tubería de spark que contiene la lógica y el algoritmo para la formación y la puntuación de modelos</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>Devolver una canalización personalizada que contenga la lógica y el algoritmo para entrenar un modelo. Este método no es necesario si se utiliza una canalización de Spark</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>dataframe</code>:: Conjunto de datos de funciones para entradas de formación</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>Puntuación mediante el modelo entrenado y devolución de los resultados</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>dataframe</code>:: Conjunto de datos de entrada para la puntuación</li>
                    <li><code>model</code>:: Un modelo entrenado utilizado para la puntuación</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Chispa (Scala)**

En la tabla siguiente se describen los métodos de clase de un [!DNL Spark] PipelineFactory:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(configProperties)</code></p>
                <p>Crear y devolver una canalización que contenga la lógica y el algoritmo para la formación y la puntuación de modelos</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

La clase MLEvaluator proporciona métodos para definir métricas de evaluación y determinar conjuntos de datos de prueba y formación.

**PySpark**

En la tabla siguiente se describen los métodos de clase de PySpark MLEvaluator:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>Divide el conjunto de datos de entrada en subconjuntos de prueba y formación</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>dataframe</code>:: Conjunto de datos de entrada que se va a dividir</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Evalúa un modelo capacitado y devuelve los resultados de la evaluación</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:: Referencia automática</li>
                    <li><code>dataframe</code>:: Un marco de datos que consta de datos de prueba y formación</li>
                    <li><code>model</code>:: Un modelo entrenado</li>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Chispa (Scala)**

En la tabla siguiente se describen los métodos de clase de un [!DNL Spark] valor MLE:

<table>
    <thead>
        <tr>
            <th>Método y descripción</th>
            <th>Parámetros</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(configProperties, data)</code></p>
                <p>Divide el conjunto de datos de entrada en subconjuntos de prueba y formación</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>data</code>:: Conjunto de datos de entrada que se va a dividir</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>Evalúa un modelo capacitado y devuelve los resultados de la evaluación</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:: Propiedades de configuración</li>
                    <li><code>model</code>:: Un modelo entrenado</li>
                    <li><code>data</code>:: Un marco de datos que consta de datos de prueba y formación</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>