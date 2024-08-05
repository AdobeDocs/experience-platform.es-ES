---
keywords: Experience Platform; hogar; temas populares; acceso a los datos; Spark SDK; API de acceso a datos; chispa fórmula; leer chispa; Escribir chispa
solution: Experience Platform
title: Acceso a datos con Spark en Data Science Espacio de trabajo
type: Tutorial
description: El siguiente documento contiene ejemplos sobre cómo acceder a datos con Spark para su uso en Data Science Espacio de trabajo.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Acceder a datos con Spark en Data Science Espacio de trabajo

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

El siguiente documento contiene ejemplos sobre cómo acceder a datos con Spark para su uso en Data Science Espacio de trabajo. Para obtener información sobre el acceso a los datos con blocs de notas de JupyterLab, visita la documentación de acceso](../jupyterlab/access-notebook-data.md) a datos [de blocs de notas de JupyterLab.

## Primeros pasos

El uso [!DNL Spark] requiere optimizaciones de rendimiento que deben agregarse al `SparkSession`archivo . Además, también puede configurar `configProperties` para que más tarde lea y escriba en conjuntos de datos.

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

## Leer una conjunto de datos

Mientras usas Spark tienes acceso a dos modos de lectura: interactivo y por lotes.

interactivo modo crea una conexión [!DNL Query Service] JDBBC (Java Database Connectivity) y obtiene resultados a través de un JDBC `ResultSet` normal que se traduce automáticamente a un `DataFrame`archivo . Este modo funciona de manera similar al método `spark.read.jdbc()`incorporado[!DNL Spark]. Este modo está pensado solo para conjuntos de datos pequeños. Si su conjunto de datos supera los 5 millones de filas, se recomienda cambiar al modo por lotes.

Lote modo utiliza [!DNL Query Service]el comando COPY de para generar conjuntos de resultados de parquet en una ubicación compartida. Estos archivos Parquet pueden procesarse posteriormente.

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

### SELECCIONAR columnas en el conjunto de datos

```scala
df = df.select("column-a", "column-b").show()
```

### Cláusula DISTINCT

La cláusula DISTINCT le permite obtener todos los valores distintos en un nivel de fila/columna, eliminando todos los valores duplicado de la respuesta.

A continuación se muestra un ejemplo de uso de la `distinct()` función:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### Cláusula WHERE

El [!DNL Spark] SDK permite dos métodos de filtrado: mediante un expresión SQL o filtrando condiciones.

A continuación se muestra un ejemplo del uso de estas funciones de filtrado:

#### expresión SQL

```scala
df.where("age > 15")
```

#### Condiciones de filtrado

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Cláusula ORDER BY

La cláusula ORDER BY permite que los resultados recibidos se ordenen por una columna específica en un orden específico (ascendente o de bajada). En el [!DNL Spark] SDK, esto se hace mediante la `sort()` función.

A continuación se muestra un ejemplo de uso de la `sort()` función:

```scala
df = df.sort($"column1", $"column2".desc)
```

### Cláusula LIMIT

La cláusula LIMIT le permite limitar el número de registros recibidos del conjunto de datos.

A continuación se muestra un ejemplo de uso de la `limit()` función:

```scala
df = df.limit(100)
```

## Escribir a un conjunto de datos

Mediante la `configProperties` asignación, puede escribir en una conjunto de datos de Experience Platform mediante `QSOption`.

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

Adobe Experience Platform Espacio de trabajo de ciencia de datos proporciona un ejemplo de fórmula de Scala (Spark) que usa los ejemplos de código anteriores para leer y escribir datos. Si desea obtener más información sobre cómo usar Spark para acceder a sus datos, consulte el [Repositorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala) de GitHub de Data Science Espacio de trabajo Scala.
