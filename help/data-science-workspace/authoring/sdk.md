---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: Guía para desarrolladores de SDK
topic: Overview
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Guía para desarrolladores de SDK

El SDK de creación de modelos le permite desarrollar fórmulas de aprendizaje automático personalizadas y tuberías de funciones que se pueden utilizar en el espacio de trabajo de ciencia de datos de la plataforma Adobe Experience Platform, proporcionando plantillas implementables en PySpark y Spark.

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
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>Carga y devolución de datos de plataforma como un DataFrame de Pandas</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code class=" language-undefined">spark</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

En la tabla siguiente se describen los métodos abstractos de una clase Spark Data Loader:

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
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>Carga y devolución de datos de plataforma como marco de datos</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code class=" language-undefined">sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Carga de datos desde un conjunto de datos de plataforma {#load-data-from-a-platform-dataset}

En el ejemplo siguiente se recuperan los datos de la plataforma por ID y se devuelve un DataFrame, donde el ID del conjunto de datos (`datasetId`) es una propiedad definida en el archivo de configuración.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

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
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
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

## DataSaver {#datasaver}

La clase DataSaver encapsula todo lo relacionado con el almacenamiento de datos de salida, incluidos los datos de puntuación o ingeniería de características. Los responsables de guardar datos amplían la clase abstracta `DataSaver` y deben anular el método abstracto `save`.

**PySpark**

En la tabla siguiente se describen los métodos abstractos de una clase PySpark Data Saver:

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
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>Recibir datos de salida como marco de datos y almacenarlos en un conjunto de datos de plataforma</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code class=" language-undefined">dataframe</code>:: Datos que se almacenarán en forma de marco de datos</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

En la tabla siguiente se describen los métodos abstractos de una clase Spark Data Saver:

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
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>Recibir datos de salida como marco de datos y almacenarlos en un conjunto de datos de plataforma</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code class=" language-undefined">dataFrame</code>:: Datos que se almacenarán en forma de marco de datos</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Guardar datos en un conjunto de datos de la plataforma {#save-data-to-a-platform-dataset}

Para almacenar datos en un conjunto de datos de la Plataforma, las propiedades deben proporcionarse o definirse en el archivo de configuración:

- ID de conjunto de datos de plataforma válida en la que se almacenarán los datos
- El ID de inquilino que pertenece a su organización

Los siguientes ejemplos almacenan datos (`prediction`) en un conjunto de datos de la plataforma, donde la ID del conjunto de datos (`datasetId`) y la ID del inquilino (`tenantId`) son propiedades definidas dentro del archivo de configuración.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
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

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
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

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer {#datasettransformer}

La clase DatasetTransformer modifica y transforma la estructura de un conjunto de datos. Sensei Machine Learning Runtime no requiere que este componente se defina y se implementa según sus necesidades.

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
                <p><i>abstract</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>Toma un conjunto de datos como entrada y genera un nuevo conjunto de datos derivado</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code class=" language-undefined">dataset</code>:: El conjunto de datos de entrada para la transformación</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

La siguiente tabla describe los métodos abstractos de una clase de transformador de conjuntos de datos Spark:

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
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>Toma un conjunto de datos como entrada y genera un nuevo conjunto de datos derivado</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                    <li><code class=" language-undefined">dataset</code>:: El conjunto de datos de entrada para la transformación</li>
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
                <p><i>abstract</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>Crear y devolver una tubería de spark que contenga una serie de transformadores de chispa</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

En la tabla siguiente se describen los métodos de clase de Spark FeaturePipelineFactory:

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
                <p><i>abstract</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>Crear y devolver una canalización que contenga una serie de transformadores</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Asignación de propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

La clase PipelineFactory encapsula métodos y definiciones para la formación y puntuación de modelos, donde la lógica y los algoritmos de formación se definen en forma de Spark Pipeline.

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
                <p><i>abstract</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>Crear y devolver una tubería de spark que contiene la lógica y el algoritmo para la formación y la puntuación de modelos</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>Devolver una canalización personalizada que contenga la lógica y el algoritmo para entrenar un modelo. Este método no es necesario si se utiliza una canalización de Spark</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">dataframe</code>:: Conjunto de datos de funciones para entradas de formación</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>Puntuación mediante el modelo entrenado y devolución de los resultados</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">dataframe</code>:: Conjunto de datos de entrada para la puntuación</li>
                    <li><code class=" language-undefined">model</code>:: Un modelo entrenado utilizado para la puntuación</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">sparkSession</code>:: Sesión de encendido</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

En la tabla siguiente se describen los métodos de clase de Spark PipelineFactory:

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
                <p><i>abstract</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>Crear y devolver una canalización que contenga la lógica y el algoritmo para la formación y la puntuación de modelos</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Recuperar y devolver mapa de parámetros de las propiedades de configuración</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">sparkSession</code>:: Sesión de encendido</li>
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
                <p><i>abstract</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>Divide el conjunto de datos de entrada en subconjuntos de prueba y formación</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">dataframe</code>:: Conjunto de datos de entrada que se va a dividir</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Evalúa un modelo capacitado y devuelve los resultados de la evaluación</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:: Referencia automática</li>
                    <li><code class=" language-undefined">dataframe</code>:: Un marco de datos que consta de datos de prueba y formación</li>
                    <li><code class=" language-undefined">model</code>:: Un modelo entrenado</li>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

En la tabla siguiente se describen los métodos de clase de un MLEvaluator de Spark:

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
                <p><i>abstract</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>Divide el conjunto de datos de entrada en subconjuntos de prueba y formación</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">data</code>:: Conjunto de datos de entrada que se va a dividir</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>Evalúa un modelo capacitado y devuelve los resultados de la evaluación</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:: Propiedades de configuración</li>
                    <li><code class=" language-undefined">model</code>:: Un modelo entrenado</li>
                    <li><code class=" language-undefined">data</code>:: Un marco de datos que consta de datos de prueba y formación</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>