---
title: Habilite la captura de datos modificados para las conexiones de origen en la API
description: Obtenga información sobre cómo habilitar la captura de datos de cambios para conexiones de origen en la API
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Habilite la captura de datos modificados para las conexiones de origen en la API

Utilice la captura de datos modificados en las fuentes de Adobe Experience Platform para mantener los sistemas de origen y destino sincronizados en tiempo casi real.

Experience Platform admite actualmente **copia de datos incremental**, que transfiere periódicamente registros recién creados o actualizados del sistema de origen a los conjuntos de datos ingeridos. Este método se basa en una **columna de marca de tiempo** para realizar el seguimiento de los cambios, pero no detecta las eliminaciones, lo que puede provocar incoherencias en los datos a lo largo del tiempo.

Por el contrario, change data capture captura y aplica inserciones, actualizaciones y eliminaciones en tiempo casi real. Este completo seguimiento de cambios garantiza que los conjuntos de datos permanezcan totalmente alineados con el sistema de origen y proporciona un historial de cambios completo, más allá de lo que admite la copia incremental. Sin embargo, las operaciones de eliminación requieren una consideración especial, ya que afectan a todas las aplicaciones que utilizan los conjuntos de datos de destinatario.

Para cambiar la captura de datos en Experience Platform se requiere **[Data Mirror](../../../xdm/data-mirror/overview.md)** con [esquemas relacionales](../../../xdm/schema/relational.md). Puede proporcionar datos de cambio a Data Mirror de dos formas:

* **[Seguimiento manual de cambios](#file-based-sources)**: incluya una columna `_change_request_type` en el conjunto de datos para los orígenes que no generan de forma nativa registros de captura de datos modificados
* **[Exportaciones nativas de captura de datos modificados](#database-sources)**: utilice registros de captura de datos modificados exportados directamente desde el sistema de origen

Ambos enfoques requieren Data Mirror con esquemas relacionales para preservar las relaciones y exigir la exclusividad.

## Data Mirror con esquemas relacionales

>[!AVAILABILITY]
>
>Los esquemas relacionales y de Data Mirror están disponibles para los titulares de licencias de **campañas orquestadas** de Adobe Journey Optimizer. También están disponibles como una **versión limitada** para los usuarios de Customer Journey Analytics, según su licencia y la habilitación de características. Póngase en contacto con su representante de Adobe para obtener acceso.

>[!NOTE]
>
>**Usuarios de campañas orquestadas**: Use las capacidades de Data Mirror descritas en este documento para trabajar con datos de clientes que mantengan integridad referencial. Incluso si el origen no utiliza el formato de captura de datos modificados, Data Mirror admite funciones relacionales como la aplicación de claves principales, actualizaciones en el nivel de registro y relaciones de esquema. Estas funciones garantizan un modelado de datos coherente y fiable en todos los conjuntos de datos conectados.

Data Mirror utiliza esquemas relacionales para ampliar la captura de datos modificados y habilitar funciones avanzadas de sincronización de bases de datos. Para obtener una descripción general de Data Mirror, consulte [Información general de Data Mirror](../../../xdm/data-mirror/overview.md).

Los esquemas relacionales extienden Experience Platform para exigir la exclusividad de la clave principal, realizar un seguimiento de los cambios de nivel de fila y definir relaciones de nivel de esquema. Con la captura de datos modificados, aplican inserciones, actualizaciones y eliminaciones directamente en el lago de datos, lo que reduce la necesidad de Extraer, Transformar, Cargar (ETL) o reconciliación manual.

Consulte [Información general sobre esquemas relacionales](../../../xdm/schema/relational.md) para obtener más información.

### Requisitos de esquema relacional para capturar datos de cambio

Antes de utilizar un esquema relacional con captura de datos modificados, configure los siguientes identificadores:

* Identifique de forma exclusiva cada registro con una clave principal.
* Aplicar actualizaciones en secuencia utilizando un identificador de versión.
* Para los esquemas de series temporales, añada un identificador de marca de tiempo.

### Control de gestión de columnas {#control-column-handling}

Utilice la columna `_change_request_type` para especificar cómo se debe procesar cada fila:

* `u` — actualizar (valor predeterminado si la columna está ausente)
* `d` — eliminar

Esta columna solo se evalúa durante la ingesta y no se almacena ni asigna a campos XDM.

### Flujo de trabajo {#workflow}

Para habilitar la captura de datos modificados con un esquema relacional:

1. Cree un esquema relacional.
2. Añada los descriptores necesarios:
   * [Descriptor de clave principal](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [Descriptor de versión](../../../xdm/api/descriptors.md#version-descriptor)
   * [Descriptor de marca de tiempo](../../../xdm/api/descriptors.md#timestamp-descriptor) (solo series de tiempo)
3. Cree un conjunto de datos a partir del esquema y habilite la captura de datos modificados.
4. Solo para la ingesta basada en archivos: agregue la columna `_change_request_type` a los archivos de origen si necesita especificar explícitamente operaciones de eliminación. Las configuraciones de exportación de CDC administran esto automáticamente para los orígenes de base de datos.
5. Complete la configuración de la conexión de origen para habilitar la ingesta.

>[!NOTE]
>
>La columna `_change_request_type` solo es necesaria para orígenes basados en archivos (Amazon S3, Azure Blob, Google Cloud Storage, SFTP) cuando desea controlar explícitamente el comportamiento de cambios en el nivel de fila. Para las fuentes de base de datos con capacidades nativas de CDC, las operaciones de cambio se gestionan automáticamente mediante configuraciones de exportación de CDC. La ingesta basada en archivos asume las operaciones de actualización de forma predeterminada; solo es necesario añadir esta columna si desea especificar operaciones de eliminación en las cargas de archivos.

>[!IMPORTANT]
>
>**Se requiere la planificación de la eliminación de datos**. Todas las aplicaciones que utilizan esquemas relacionales deben comprender las implicaciones de eliminación antes de implementar la captura de datos de cambio. Planifique cómo las eliminaciones afectarán a los conjuntos de datos relacionados, los requisitos de cumplimiento y los procesos descendentes. Consulte [consideraciones sobre la higiene de los datos](../../../hygiene/ui/record-delete.md#relational-record-delete) para obtener instrucciones.

## Proporcionar datos de cambio para orígenes basados en archivos {#file-based-sources}

>[!IMPORTANT]
>
>La captura de datos de cambios basada en archivos requiere Data Mirror con esquemas relacionales. Antes de seguir los pasos de formato de archivo siguientes, asegúrese de haber completado el [flujo de trabajo de configuración de Data Mirror](#workflow) descrito anteriormente en este documento. Los pasos siguientes describen cómo dar formato a los archivos de datos para incluir la información de seguimiento de cambios que procesará Data Mirror.

Para los orígenes basados en archivos ([!DNL Amazon S3], [!DNL Azure Blob], [!DNL Google Cloud Storage] y [!DNL SFTP]), incluya una columna `_change_request_type` en los archivos.

Use los valores de `_change_request_type` definidos en la sección [Control column handling](#control-column-handling) anterior.

>[!IMPORTANT]
>
>Para **solo orígenes basados en archivos**, ciertas aplicaciones pueden requerir una columna `_change_request_type` con `u` (actualización) o `d` (eliminación) para validar las capacidades de seguimiento de cambios. Por ejemplo, la función **Campañas orquestadas** de Adobe Journey Optimizer requiere esta columna para habilitar la opción &quot;Campaña orquestada&quot; y permitir la selección de conjuntos de datos para la segmentación. Los requisitos de validación específicos de la aplicación pueden variar.

Siga los pasos específicos de la fuente a continuación.

### Fuentes de almacenamiento en nube {#cloud-storage-sources}

Habilite la captura de datos modificados para las fuentes de almacenamiento en la nube siguiendo estos pasos:

1. Cree una conexión base para el origen:

   | Fuente | Guía de conexión base |
   |---|---|
   | [!DNL Amazon S3] | [Crear una [!DNL Amazon S3] conexión base](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [Crear una [!DNL Azure Blob] conexión base](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [Crear una [!DNL Google Cloud Storage] conexión base](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [Crear una [!DNL SFTP] conexión base](../api/create/cloud-storage/sftp.md) |

2. [Crear una conexión de origen para un almacenamiento en la nube](../api/collect/cloud-storage.md#create-a-source-connection).

Todos los orígenes de almacenamiento en la nube utilizan el mismo formato de columna `_change_request_type` descrito en la sección [Orígenes basados en archivos](#file-based-sources) anterior.

## Orígenes de base de datos {#database-sources}

### [!DNL Azure Databricks]

Para usar la captura de datos modificados con [!DNL Azure Databricks], debe habilitar **cambiar la fuente de datos** en las tablas de origen y configurar Data Mirror con esquemas relacionales en Experience Platform.

Utilice los siguientes comandos para habilitar el cambio de fuente de datos en las tablas:

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

### [!DNL Data Landing Zone]

Para usar la captura de datos modificados con [!DNL Data Landing Zone], debe habilitar **cambiar la fuente de datos** en las tablas de origen y configurar Data Mirror con esquemas relacionales en Experience Platform.

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Data Landing Zone]:

* [Crear una [!DNL Data Landing Zone] conexión base](../api/create/cloud-storage/data-landing-zone.md).
* [Crear una conexión de origen para un almacenamiento en la nube](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

Para usar la captura de datos modificados con [!DNL Google BigQuery], debe habilitar el historial de cambios en las tablas de origen y configurar Data Mirror con esquemas relacionales en Experience Platform.

Para habilitar el historial de cambios en la conexión de origen de [!DNL Google BigQuery], vaya a la página [!DNL Google BigQuery] en la consola [!DNL Google Cloud] y establezca `enable_change_history` en `TRUE`. Esta propiedad habilita el historial de cambios para la tabla de datos.

Para obtener más información, lea la guía de [instrucciones de lenguaje de definición de datos en [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Google BigQuery]:

* [Crear una [!DNL Google BigQuery] conexión base](../api/create/databases/bigquery.md).
* [Crear una conexión de origen para una base de datos](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

Para usar la captura de datos modificados con [!DNL Snowflake], debe habilitar **el seguimiento de cambios** en las tablas de origen y configurar Data Mirror con esquemas relacionales en Experience Platform.

En [!DNL Snowflake], habilite el seguimiento de cambios usando `ALTER TABLE` y estableciendo `CHANGE_TRACKING` en `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Para obtener más información, lea la [[!DNL Snowflake] guía sobre el uso de la cláusula de cambios](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lea la siguiente documentación para ver los pasos que debe seguir para habilitar la captura de datos modificados para la conexión de origen de [!DNL Snowflake]:

* [Crear una [!DNL Snowflake] conexión base](../api/create/databases/snowflake.md).
* [Crear una conexión de origen para una base de datos](../api/collect/database-nosql.md#create-a-source-connection).
