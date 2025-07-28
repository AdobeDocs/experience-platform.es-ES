---
title: Habilite la captura de datos modificados para las conexiones de origen en la API
description: Obtenga información sobre cómo habilitar la captura de datos de cambios para conexiones de origen en la API
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Habilite la captura de datos modificados para las conexiones de origen en la API

Cambiar la captura de datos en las fuentes de Adobe Experience Platform es una capacidad que puede utilizar para mantener la sincronización de datos en tiempo real entre los sistemas de origen y destino.

Actualmente, Experience Platform admite **copia de datos incremental**, lo que garantiza que los registros recién creados o actualizados en el sistema de origen se copien periódicamente en los conjuntos de datos ingeridos. Este proceso se basa en el uso de la **columna de marca de tiempo**, como `LastModified`, para poder rastrear cambios y capturar **solo los datos recién insertados o actualizados**. Sin embargo, este método no tiene en cuenta los registros eliminados, lo que puede provocar incoherencias en los datos a lo largo del tiempo.

Con la captura de datos de cambio, un flujo determinado captura y aplica todos los cambios, incluidas las inserciones, las actualizaciones y las eliminaciones. Del mismo modo, los conjuntos de datos de Experience Platform permanecen totalmente sincronizados con el sistema de origen.

Puede utilizar la captura de datos modificados para las siguientes fuentes:

## [!DNL Amazon S3]

Asegúrese de que `_change_request_type` esté presente en el archivo [!DNL Amazon S3] que desea ingerir en Experience Platform. Además, debe asegurarse de que los siguientes valores válidos estén incluidos en el archivo:

* `u`: para inserciones y actualizaciones
* `d`: para eliminaciones.

Si `_change_request_type` no está presente en el archivo, se usará el valor predeterminado de `u`.

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Amazon S3]:

* [Crear una [!DNL Amazon S3] conexión base](../api/create/cloud-storage/s3.md).
* [Crear una conexión de origen para un almacenamiento en la nube](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Asegúrese de que `_change_request_type` esté presente en el archivo [!DNL Azure Blob] que desea ingerir en Experience Platform. Además, debe asegurarse de que los siguientes valores válidos estén incluidos en el archivo:

* `u`: para inserciones y actualizaciones
* `d`: para eliminaciones.

Si `_change_request_type` no está presente en el archivo, se usará el valor predeterminado de `u`.

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Azure Blob]:

* [Crear una [!DNL Azure Blob] conexión base](../api/create/cloud-storage/blob.md).
* [Crear una conexión de origen para un almacenamiento en la nube](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

Debe habilitar **cambiar fuente de datos** en la tabla [!DNL Azure Databricks] para usar la captura de datos modificados en la conexión de origen.

Utilice los siguientes comandos para habilitar explícitamente la opción de cambiar fuente de datos en [!DNL Azure Databricks]

**Nueva tabla**

Para aplicar el cambio de fuente de datos a una nueva tabla, debe establecer la propiedad de tabla `delta.enableChangeDataFeed` en `TRUE` en el comando `CREATE TABLE`.

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Tabla existente**

Para aplicar el cambio de fuente de datos a una tabla existente, debe establecer la propiedad de tabla `delta.enableChangeDataFeed` en `TRUE` en el comando `ALTER TABLE`.

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Todas las tablas nuevas**

Para aplicar el cambio de fuente de datos a todas las tablas nuevas, debe establecer las propiedades predeterminadas en `TRUE`.

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

Para obtener más información, lea la [[!DNL Azure Databricks] guía sobre cómo habilitar la fuente de datos para cambios](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed).

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Azure Databricks]:

* [Crear una [!DNL Azure Databricks] conexión base](../api/create/databases/databricks.md).
* [Crear una conexión de origen para una base de datos](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

Debe habilitar **cambiar fuente de datos** en la tabla [!DNL Data Landing Zone] para usar la captura de datos modificados en la conexión de origen.

Utilice los siguientes comandos para habilitar explícitamente la opción de cambiar fuente de datos en [!DNL Data Landing Zone].

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Data Landing Zone]:

* [Crear una [!DNL Data Landing Zone] conexión base](../api/create/cloud-storage/data-landing-zone.md).
* [Crear una conexión de origen para un almacenamiento en la nube](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

Para usar la captura de datos modificados en su conexión de origen de [!DNL Google BigQuery]. Vaya a la página [!DNL Google BigQuery] en la consola [!DNL Google Cloud] y establezca `enable_change_history` en `TRUE`. Esta propiedad habilita el historial de cambios para la tabla de datos.

Para obtener más información, lea la guía de [instrucciones de lenguaje de definición de datos en [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Google BigQuery]:

* [Crear una [!DNL Google BigQuery] conexión base](../api/create/databases/bigquery.md).
* [Crear una conexión de origen para una base de datos](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Asegúrese de que `_change_request_type` esté presente en el archivo [!DNL Google Cloud Storage] que desea ingerir en Experience Platform. Además, debe asegurarse de que los siguientes valores válidos estén incluidos en el archivo:

* `u`: para inserciones y actualizaciones
* `d`: para eliminaciones.

Si `_change_request_type` no está presente en el archivo, se usará el valor predeterminado de `u`.

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Google Cloud Storage]:

* [Crear una [!DNL Google Cloud Storage] conexión base](../api/create/cloud-storage/google.md).
* [Crear una conexión de origen para un almacenamiento en la nube](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Asegúrese de que `_change_request_type` esté presente en el archivo [!DNL SFTP] que desea ingerir en Experience Platform. Además, debe asegurarse de que los siguientes valores válidos estén incluidos en el archivo:

* `u`: para inserciones y actualizaciones
* `d`: para eliminaciones.

Si `_change_request_type` no está presente en el archivo, se usará el valor predeterminado de `u`.

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL SFTP]:

* [Crear una [!DNL SFTP] conexión base](../api/create/cloud-storage/sftp.md).
* [Crear una conexión de origen para un almacenamiento en la nube](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

Debe habilitar **el seguimiento de cambios** en sus tablas [!DNL Snowflake] para poder usar la captura de datos de cambios en las conexiones de origen.

En [!DNL Snowflake], habilite el seguimiento de cambios usando `ALTER TABLE` y estableciendo `CHANGE_TRACKING` en `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Para obtener más información, lea la [[!DNL Snowflake] guía sobre el uso de la cláusula de cambios](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Snowflake]:

* [Crear una [!DNL Snowflake] conexión base](../api/create/databases/snowflake.md).
* [Crear una conexión de origen para una base de datos](../api/collect/database-nosql.md#create-a-source-connection).

