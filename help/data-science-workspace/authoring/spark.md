---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Acceso a datos mediante Spark
topic: tutorial
type: Tutorial
description: El siguiente documento contiene ejemplos de cómo acceder a los datos mediante Spark para utilizarlos en Área de trabajo de ciencias de datos.
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Acceso a datos mediante Spark

El siguiente documento contiene ejemplos de cómo acceder a los datos mediante Spark para utilizarlos en Área de trabajo de ciencias de datos. Para obtener información sobre el acceso a los datos mediante portátiles JupyterLab, visite la documentación de acceso [a los datos de los portátiles de](../jupyterlab/access-notebook-data.md) JupyterLab.

## Primeros pasos

El uso [!DNL Spark] requiere optimizaciones de rendimiento que deben agregarse al `SparkSession`. Además, también puede configurar `configProperties` para que más adelante pueda leer y escribir en conjuntos de datos.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Lectura de un conjunto de datos

Mientras utiliza Spark tiene acceso a dos modos de lectura: interactivo y por lotes.

El modo interactivo crea una conexión de Conectividad de base de datos Java (JDBC) [!DNL Query Service] y obtiene resultados a través de un JDBC regular `ResultSet` que se traduce automáticamente a un `DataFrame`. Este modo funciona de forma similar al [!DNL Spark] método integrado `spark.read.jdbc()`. Este modo solo está diseñado para conjuntos de datos pequeños. Si el conjunto de datos supera los 5 millones de filas, se sugiere cambiar al modo por lotes.

El modo Lote utiliza [!DNL Query Service]el comando COPY de para generar conjuntos de resultados de parquet en una ubicación compartida. Estos archivos de parquet pueden procesarse posteriormente.

A continuación se muestra un ejemplo de lectura de un conjunto de datos en modo interactivo:

```scala
  // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

De manera similar, a continuación se muestra un ejemplo de lectura de un conjunto de datos en modo por lotes:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### SELECCIONAR columnas del conjunto de datos

```scala
df = df.select("column-a", "column-b").show()
```

### Cláusula DISTINCT

La cláusula DISTINCT permite recuperar todos los valores distintos en un nivel de fila/columna, eliminando todos los valores de duplicado de la respuesta.

A continuación se muestra un ejemplo del uso de la `distinct()` función:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### cláusula WHERE

El [!DNL Spark] SDK admite dos métodos de filtrado: Uso de una expresión SQL o filtrado mediante condiciones.

A continuación se muestra un ejemplo del uso de estas funciones de filtrado:

#### EXPRESIÓN SQL

```scala
df.where("age > 15")
```

#### Condiciones de filtrado

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Cláusula ORDER BY

La cláusula ORDER BY permite ordenar los resultados recibidos por una columna específica en un orden específico (ascendente o descendente). En el [!DNL Spark] SDK, esto se realiza mediante la `sort()` función .

A continuación se muestra un ejemplo del uso de la `sort()` función:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Cláusula LIMIT

La cláusula LIMIT permite limitar el número de registros recibidos del conjunto de datos.

A continuación se muestra un ejemplo del uso de la `limit()` función:

```scala
df = df.limit(100)
```

## Escritura en un conjunto de datos

Con la `configProperties` asignación, puede escribir en un conjunto de datos en un Experience Platform mediante `QSOption`.

```scala
val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Pasos siguientes

Adobe Experience Platform Data Science Workspace proporciona un ejemplo de fórmula Scala (Spark) que utiliza las muestras de código anteriores para leer y escribir datos. Si desea obtener más información sobre cómo utilizar Spark para acceder a sus datos, consulte el repositorio [de](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)Data Science Workspace Scala GitHub.