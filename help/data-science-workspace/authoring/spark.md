---
keywords: Experience Platform;inicio;temas populares;acceso a datos;spark sdk;api de acceso a datos;fórmula de spark;leer chispa;escribir chispa
solution: Experience Platform
title: Acceso a datos mediante Spark en Data Science Workspace
type: Tutorial
description: El siguiente documento contiene ejemplos sobre cómo acceder a datos mediante Spark para utilizarlos en Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Acceso a los datos mediante Spark en Data Science Workspace

El siguiente documento contiene ejemplos sobre cómo acceder a datos mediante Spark para utilizarlos en Data Science Workspace. Para obtener información sobre el acceso a los datos mediante los blocs de notas de JupyterLab, visite [Acceso a los datos de los portátiles JupyterLab](../jupyterlab/access-notebook-data.md) documentación.

## Primeros pasos

Uso [!DNL Spark] requiere optimizaciones de rendimiento que se deben agregar al `SparkSession`. Además, también puede configurar `configProperties` para leer y escribir más tarde en conjuntos de datos.

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
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Leer un conjunto de datos

Mientras utiliza Spark tiene acceso a dos modos de lectura: interactivo y por lotes.

El modo interactivo crea una conexión de Java Database Connectivity (JDBC) a [!DNL Query Service] y obtiene resultados a través de un JDBC normal `ResultSet` que se traduce automáticamente a un `DataFrame`. Este modo funciona de forma similar al integrado [!DNL Spark] method `spark.read.jdbc()`. Este modo solo está diseñado para conjuntos de datos pequeños. Si el conjunto de datos supera los 5 millones de filas, se sugiere que cambie al modo por lotes.

El modo por lotes utiliza [!DNL Query Service]El comando COPY de para generar conjuntos de resultados de parquet en una ubicación compartida. Estos archivos de parquet se pueden seguir procesando.

A continuación se puede ver un ejemplo de lectura de un conjunto de datos en modo interactivo:

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
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

Del mismo modo, a continuación se puede ver un ejemplo de lectura de un conjunto de datos en modo por lotes:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
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

La cláusula DISTINCT permite recuperar todos los valores distintos a nivel de fila/columna, eliminando todos los valores duplicados de la respuesta.

Un ejemplo de uso de la variable `distinct()` a continuación:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### cláusula WHERE

La variable [!DNL Spark] El SDK admite dos métodos de filtrado: Uso de una expresión SQL o filtrado mediante condiciones.

A continuación se puede ver un ejemplo del uso de estas funciones de filtrado:

#### Expresión SQL

```scala
df.where("age > 15")
```

#### Condiciones de filtrado

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Cláusula ORDER BY

La cláusula ORDER BY permite ordenar los resultados recibidos por una columna especificada en un orden específico (ascendente o descendente). En el [!DNL Spark] SDK, esto se realiza utilizando la variable `sort()` función.

Un ejemplo de uso de la variable `sort()` a continuación:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Cláusula LIMIT

La cláusula LIMIT permite limitar el número de registros recibidos del conjunto de datos.

Un ejemplo de uso de la variable `limit()` a continuación:

```scala
df = df.limit(100)
```

## Escritura en un conjunto de datos

Uso de `configProperties` asignación, puede escribir en un conjunto de datos en Experience Platform mediante `QSOption`.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Pasos siguientes

Adobe Experience Platform Data Science Workspace proporciona un ejemplo de fórmula Scala (Spark) que utiliza los ejemplos de código anteriores para leer y escribir datos. Si desea obtener más información sobre cómo utilizar Spark para acceder a sus datos, consulte la [Repositorio de Data Science Workspace Scala GitHub](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
