---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api
solution: Experience Platform
title: SDK de acceso a datos Spark seguro
topic: tutorial
type: Tutorial
description: El SDK de acceso a datos Secure Spark es un kit de desarrollo de software que permite leer y escribir conjuntos de datos desde Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# SDK seguro [!DNL Spark Data Access]

El SDK seguro [!DNL Spark] [!DNL Data Access] es un kit de desarrollo de software que permite leer y escribir conjuntos de datos desde Adobe Experience Platform.

## Primeros pasos

Debe haber completado el tutorial de [autenticación](../../tutorials/authentication.md) para tener acceso a los valores y realizar llamadas al SDK seguro [!DNL Spark] [!DNL Data Access] :

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. El uso del [!DNL Spark] SDK requiere el nombre y el ID del simulador para pruebas en el que se realizará la operación:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

## Configuración de entorno

El SDK [!DNL Spark] espera que proporcione las credenciales en las variables de entorno o en las opciones de fuente de datos.

| Variable | Valor |
| -------- | ----- | 
| `SERVICE_TOKEN` | Su token de autorización de servicio. |
| `SERVICE_API_KEY` | Su clave de API de servicio. Generalmente es el mismo que el ID de cliente de IMS. |
| `ORG_ID` | Su valor `{IMS_ORG}` de ID. |
| `USER_TOKEN` | Su `{ACCESS_TOKEN}` valor. |

Otros parámetros de configuración incluyen:

| Variable | Valor |
| -------- | ----- |
| `ENVIRONMENT_NAME` | El entorno al que intenta conectarse. Puede ser de &quot;dev&quot;, &quot;stage&quot; o &quot;prod&quot;. |
| `SANDBOX_NAME` | Nombre del simulador para pruebas al que se está conectando. |

Alternativamente, aparte de `ENVIRONMENT_NAME`, puede configurar cualquiera de las variables de entorno anteriores dentro de `QSOption`, como se muestra en el ejemplo siguiente:

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## Instalación

El uso del [!DNL Spark] SDK requiere optimizaciones de rendimiento que deben agregarse al `SparkSession`. Puede aplicarlas mediante uno de los siguientes métodos:

Aplíquelo directamente a la SparkSession actual:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

Establezca la siguiente configuración antes o en la creación de SparkSession:

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## Lectura de un conjunto de datos

El [!DNL Spark] SDK admite dos modos de lectura: interactivo y por lotes.

El modo interactivo crea una conexión de Conectividad de base de datos Java (JDBC) [!DNL Query Service] y obtiene resultados a través de un JDBC regular `ResultSet` que se traduce automáticamente a un `DataFrame`. Este modo funciona de forma similar al [!DNL Spark] método integrado `spark.read.jdbc()`. Este modo solo está diseñado para conjuntos de datos pequeños y solo requiere un token de usuario para la autenticación.

El modo Lote utiliza [!DNL Query Service]el comando COPY de para generar conjuntos de resultados de parquet en una ubicación compartida. Estos archivos de parquet pueden procesarse posteriormente. Este modo requiere un token de usuario y un token de servicio con el `acp.foundation.catalog.credentials` ámbito.

A continuación se muestra un ejemplo de lectura de un conjunto de datos en modo interactivo:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

De manera similar, a continuación se muestra un ejemplo de lectura de un conjunto de datos en modo por lotes:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
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

La cláusula LIMIT permite a los usuarios limitar el número de registros recibidos del conjunto de datos.

A continuación se muestra un ejemplo del uso de la `limit()` función:

```scala
df = df.limit(100)
```

## Escritura en un conjunto de datos

El [!DNL Spark] SDK admite la escritura de conjuntos de datos. Los usuarios primero tendrán que recuperar un conjunto de datos anterior para escribir en un nuevo conjunto de datos.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
