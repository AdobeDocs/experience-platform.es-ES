---
keywords: Experience Platform; guía de desarrolladores; SDK; Autoría de modelos; Data Science Espacio de trabajo; temas populares; ensayo
solution: Experience Platform
title: SDK de creación de modelos
description: El SDK de creación de modelos permite desarrollar recetas y canalizaciones de características personalizadas de aprendizaje automático que se pueden usar en Adobe Experience Platform Espacio de trabajo de ciencia de datos, proporcionando plantillas implementables en PySpark y Spark (Scala).
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 1%

---

# SDK de creación de modelos

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

El SDK de creación de modelos permite desarrollar fórmulas y canalizaciones de características de aprendizaje automático personalizadas que se pueden usar en [!DNL Adobe Experience Platform] Espacio de trabajo de ciencia de datos, proporcionando plantillas implementables en [!DNL PySpark] y [!DNL Spark (Scala)].

Este documento proporciona información sobre las distintas clases que se encuentran en el SDK de creación de modelos.

## Cargador de datos {#dataloader}

La clase DataLoader encapsula todo lo relacionado con la recuperación, filtrado y devolución de datos de entrada sin procesar. Los ejemplos de datos de entrada incluyen los de aprendizaje, puntuación o ingeniería de características. Los cargadores de datos amplían la clase abstracta `DataLoader` y deben invalidar el método abstracto `load`.

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
                <p>Carga y devolución de datos Platform como un diagrama de datos de Pandas</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Autorreferencia</li>
                    <li><code>configProperties</code>: Mapa de propiedades de configuración</li>
                    <li><code>spark</code>: sesión de Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

En la tabla siguiente se describen los métodos abstractos de una clase de cargador de datos [!DNL Spark]:

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
                <p>Carga y devolución de datos de Platform como DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: asignación de propiedades de configuración</li>
                    <li><code>sparkSession</code>: sesión de Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Cargar datos de un conjunto de datos [!DNL Platform] {#load-data-from-a-platform-dataset}

En el ejemplo siguiente se recuperan datos por ID y se devuelve un DataFrame, donde el conjunto de datos ID (`datasetId`) es un Propiedad definido en el archivo de [!DNL Platform] configuración.

**Chispa PySpark**

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

**Spark (Scala)**

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

## Protector de datos {#datasaver}

La clase DataSaver encapsula todo lo relacionado con el almacenamiento de datos de salida, incluidos los de puntuación o ingeniería de características. Los ahorradores de datos amplían la clase `DataSaver` abstracta y deben anular el método `save`abstracto.

**Chispa PySpark**

En la tabla siguiente se describen los métodos abstractos de una [!DNL PySpark] clase de ahorro de datos:

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
                <p>Recibir los datos de salida como un DataFrame y almacenarlos en una Platform conjunto de datos</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Referencia automática</li>
                    <li><code>configProperties</code>: asignación de propiedades de configuración</li>
                    <li><code>dataframe</code>: Datos que se van a almacenar en forma de DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

En la tabla siguiente se describen los métodos abstractos de una [!DNL Spark] clase de ahorro de datos:

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
                <p>Recibir los datos de salida como un DataFrame y almacenarlos en una Platform conjunto de datos</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Mapa de propiedades de configuración</li>
                    <li><code>dataFrame</code>: Datos que se van a almacenar en forma de DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Guardar datos a un [!DNL Platform] conjunto de datos {#save-data-to-a-platform-dataset}

Para tienda datos en una [!DNL Platform] conjunto de datos, las propiedades deben proporcionarse o definirse en el archivo de configuración:

- ID de conjunto de datos válida [!DNL Platform] en la que se almacenarán los datos
- El ID de inquilino que pertenece a su organización

Los siguientes ejemplos tienda datos (`prediction`) en un [!DNL Platform] conjunto de datos, donde el ID de conjunto de datos (`datasetId`) y el ID de inquilino (`tenantId`) son propiedades definidas dentro del archivo de configuración.


**Chispa PySpark**

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

**Spark (Scala)**

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

La clase DatasetTransformer modifica y transforma la estructura de un conjunto de datos. El [!DNL Sensei Machine Learning Runtime] no requiere que se defina este componente y se implementa según sus necesidades.

En lo que respecta a una canalización de características, conjunto de datos transformadores se pueden usar de forma cooperativa con una fábrica de tuberías de características para preparar datos para la ingeniería de características.

**Chispa PySpark**

La tabla siguiente describe los métodos de clase de una clase de transformador conjunto de datos PySpark:

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
                <p><i>abstracto</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>Toma una conjunto de datos como entrada y salida como nueva conjunto de datos derivada</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Autorreferencia</li>
                    <li><code>configProperties</code>: Mapa de propiedades de configuración</li>
                    <li><code>dataset</code>: el conjunto de datos de entrada para transformación</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

La siguiente tabla describe los métodos abstractos de una [!DNL Spark] clase de transformador de conjunto de datos:

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
                <p>Toma un conjunto de datos como entrada y como salida un nuevo conjunto de datos derivado</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: asignación de propiedades de configuración</li>
                    <li><code>dataset</code>: el conjunto de datos de entrada para la transformación</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

La clase FeaturePipelineFactory contiene algoritmos de extracción de características y define las etapas de una canalización de características desde inicio hasta el final.

**Chispa PySpark**

La siguiente tabla describe los métodos de clase de PySpark FeaturePipelineFactory:

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
                <p><i>compendio</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>Crear y devolver una canalización de Spark que contenga una serie de transformadores de Spark</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Autorreferencia</li>
                    <li><code>configProperties</code>: Mapa de propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>compendio</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver el mapa del parámetro desde las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Referencia automática</li>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                    <li><code>sparkSession</code>: Sesión de Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

En la tabla siguiente se describen los métodos de clase de FeaturePipelineFactory [!DNL Spark] :

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
                <p><i>abstracto</i><br/><code>createPipeline(configProperties)</code></p>
                <p>Crear y devolver una canalización que contenga una serie de transformadores</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Mapa de propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstracto</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver el mapa de parámetros desde las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propiedades de configuración</li>
                    <li><code>sparkSession</code>: Sesión de Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

La clase PipelineFactory encapsula métodos y definiciones para la formación y puntuación de modelos, donde la lógica y los algoritmos de formación se definen en forma de canalización [!DNL Spark].

**PySpark**

En la tabla siguiente se describen los métodos de clase de una PipelineFactory de PySpark:

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
                <p><i>abstracto</i><br/><code>apply(self, configProperties)</code></p>
                <p>Crear y Return a Spark Pipeline que contiene la lógica y el algoritmo para la aprendizaje y la puntuación del modelo</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Autorreferencia</li>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstracto</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>Devuelve una canalización personalizada que contiene la lógica y el algoritmo para entrenar un modelo. Este método no es necesario si se utiliza una canalización de Spark</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Autorreferencia</li>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                    <li><code>dataframe</code>: Conjunto de datos de funciones para la entrada de formación</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstracto</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>Puntuar utilizando el modelo entrenado y devolver los resultados</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Autorreferencia</li>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                    <li><code>dataframe</code>: conjunto de datos de entrada para la puntuación</li>
                    <li><code>model</code>: Un modelo entrenado utilizado para la puntuación</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstracto</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver el mapa de parámetros desde las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Autorreferencia</li>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                    <li><code>sparkSession</code>: Sesión de Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

En la tabla siguiente se describen los métodos de clase de PipelineFactory [!DNL Spark] :

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
                <p><i>abstracto</i><br/><code>apply(configProperties)</code></p>
                <p>Crear y devolver una canalización que contenga la lógica y el algoritmo para la formación y la puntuación del modelo</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>compendio</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver el mapa de parámetros desde las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                    <li><code>sparkSession</code>: Sesión de Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluador {#mlevaluator}

La clase MLEvaluator proporciona métodos para definir métricas de evaluación y determinar conjuntos de datos de prueba y aprendizaje.

**PySpark**

En la tabla siguiente se describen los métodos de clase de un MLEvaluator de PySpark:

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
                <p><i>abstracto</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>Divide el conjunto de datos de entrada en subconjuntos de prueba y aprendizaje</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Referencia automática</li>
                    <li><code>configProperties</code>: propiedades de configuración</li>
                    <li><code>dataframe</code>: conjunto de datos de entrada que se va a dividir</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstracto</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Evalúa un modelo entrenado y devuelve los resultados de la evaluación</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Referencia automática</li>
                    <li><code>dataframe</code>: un DataFrame que consta de datos de prueba y aprendizaje</li>
                    <li><code>model</code>: Un modelo entrenado</li>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

En la tabla siguiente se describen los métodos de clase de un MLEvaluator [!DNL Spark]:

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
                <p><i>compendio</i><br/><code>split(configProperties, data)</code></p>
                <p>Divide el conjunto de datos de entrada en subconjuntos de prueba y aprendizaje</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propiedades de configuración</li>
                    <li><code>data</code>: conjunto de datos de entrada que se va a dividir</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>compendio</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>Evalúa un modelo entrenado y devuelve los resultados de la evaluación</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Propiedades de configuración</li>
                    <li><code>model</code>: Un modelo entrenado</li>
                    <li><code>data</code>: un DataFrame que consta de datos de prueba y aprendizaje</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
