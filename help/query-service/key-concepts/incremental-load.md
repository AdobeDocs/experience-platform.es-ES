---
title: Incremental Load in Query Service
description: The incremental load feature uses both anonymous block and snapshot features to provide a near real-time solution for moving data from the data lake to your data warehouse whilst ignoring matching data.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: f2d81f05c8c19c6f28849fc4dbe9bfa26be64645
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Incremental load in Query Service

The incremental load design pattern is a solution for managing data. The pattern only processes information in the dataset that has been created or modified since the last load execution.

Incremental load uses various features provided by Adobe Experience Platform Query Service such as anonymous block and snapshots. This design pattern increases processing efficiency as any data already processed from the source is skipped. It can be used with both streaming and batch data processing.

This document provides a series of instructions to build a design pattern for incremental processing. These steps can be used as a template to create your own incremental data load queries.

## Introducción

The SQL examples throughout this document require you to have an understanding of the anonymous block and snapshot capabilities. It is recommended that you read the [sample anonymous block queries](./anonymous-block.md) documentation and also the [snapshot clause](../sql/syntax.md#snapshot-clause) documentation.

For guidance on any terminology used within this guide, refer to the [SQL syntax guide](../sql/syntax.md).

## Incrementally load data

The steps below demonstrate how to create and incrementally load data using snapshots and the anonymous block feature. The design pattern can be used as a template for your own sequence of queries.

1. Create a `checkpoint_log` table to track the most recent snapshot used to process data successfully. The tracking table (`checkpoint_log` in this example) must first be initialized to `null` in order to incrementally process a dataset.

   ```SQL
   DROP TABLE IF EXISTS checkpoint_log;
   CREATE TABLE  checkpoint_log AS
   SELECT
      cast(NULL AS string) process_name,
      cast(NULL AS string) process_status,
      cast(NULL AS string) last_snapshot_id,
      cast(NULL AS TIMESTAMP) process_timestamp
      WHERE false;
   ```

1. Populate the `checkpoint_log` table with one empty record for the dataset that needs incremental processing. `DIM_TABLE_ABC` is the dataset to be processed in the example below. On the first occasion of processing `DIM_TABLE_ABC`, the `last_snapshot_id` is initialized as `null`. This allows you to process the entire dataset on the first occasion and incrementally thereafter.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. Next, initialize `DIM_TABLE_ABC_Incremental` to contain processed output from `DIM_TABLE_ABC`. The anonymous block in the **required** execution section of the SQL example below, as described in steps one to four, is executed sequentially to process data incrementally.

   1. Set the `from_snapshot_id` which indicates where the processing starts from. Se ha consultado el elemento `from_snapshot_id` del ejemplo en la tabla `checkpoint_log` para su uso con `DIM_TABLE_ABC`. En la primera ejecución, el ID de instantánea será `null`, lo que significa que se procesará todo el conjunto de datos.
   1. Establezca `to_snapshot_id` como el identificador de instantánea actual de la tabla de origen (`DIM_TABLE_ABC`). En el ejemplo, esto se consulta desde la tabla de metadatos de la tabla de origen.
   1. Use la palabra clave `CREATE` para crear `DIM_TABLE_ABC_Incremenal` como tabla de destino. La tabla de destino conserva los datos procesados del conjunto de datos de origen (`DIM_TABLE_ABC`). Esto permite que los datos procesados de la tabla de origen entre `from_snapshot_id` y `to_snapshot_id` se anexen gradualmente a la tabla de destino.
   1. Actualice la tabla `checkpoint_log` con `to_snapshot_id` para los datos de origen que `DIM_TABLE_ABC` procesó correctamente.
   1. Si falla cualquiera de las consultas ejecutadas secuencialmente del bloque anónimo, se ejecuta la sección de excepciones **optional**. Esto devuelve un error y finaliza el proceso.

   >[!NOTE]
   >
   >`history_meta('source table name')` es un método cómodo que se usa para obtener acceso a las instantáneas disponibles en un conjunto de datos.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       CREATE TABLE DIM_TABLE_ABC_Incremental AS
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHERS THEN
       SELECT 'ERROR';
   END 
   $$;
   ```

1. Utilice la lógica de carga de datos incremental en el ejemplo de bloque anónimo siguiente para permitir que cualquier dato nuevo del conjunto de datos de origen (desde la marca de tiempo más reciente) se procese y se anexe a la tabla de destino a una cadencia regular. En el ejemplo, los cambios de datos en `DIM_TABLE_ABC` se procesarán y se anexarán a `DIM_TABLE_ABC_incremental`.

   >[!NOTE]
   >
   > `_ID` es la clave principal en `DIM_TABLE_ABC_Incremental` y `SELECT history_meta('DIM_TABLE_ABC')`.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       INSERT INTO DIM_TABLE_ABC_Incremental
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHERS THEN
       SELECT 'ERROR';
   END
   $$;
   ```

Esta lógica se puede aplicar a cualquier tabla para realizar cargas incrementales.

## Instantáneas caducadas

Para resolver el problema de un ID de instantánea caducado, inserte el siguiente comando al principio del bloque anónimo. La siguiente línea de código anula `@from_snapshot_id` con los primeros `snapshot_id` disponibles de los metadatos.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

Todo el bloque de código tiene el siguiente aspecto:

```SQL
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHERS THEN
    SELECT 'ERROR';
END
$$;
```

## Próximos pasos

Al leer este documento, debería comprender mejor cómo utilizar las funciones de bloqueo anónimo e instantáneas para realizar cargas incrementales y puede aplicar esta lógica a sus propias consultas específicas. Para obtener instrucciones generales sobre la ejecución de consultas, lea la [guía sobre la ejecución de consultas en el servicio de consultas](../best-practices/writing-queries.md).
