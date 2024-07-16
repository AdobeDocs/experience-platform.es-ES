---
title: Carga incremental en el servicio de consultas
description: La función de carga incremental utiliza las funciones de bloque anónimo y de instantánea para proporcionar una solución casi en tiempo real que permite mover datos del lago de datos al almacén de datos e ignorar los datos coincidentes.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Carga incremental en el servicio de consultas

El patrón de diseño de carga incremental es una solución para administrar datos. El patrón solo procesa la información en el conjunto de datos que se ha creado o modificado desde la última ejecución de carga.

La carga incremental utiliza varias funciones proporcionadas por Adobe Experience Platform Query Service, como bloque anónimo e instantáneas. Este patrón de diseño aumenta la eficacia del procesamiento, ya que se omiten los datos que ya se han procesado desde el origen. Se puede utilizar con el procesamiento de datos por lotes y el streaming.

Este documento proporciona una serie de instrucciones para crear un patrón de diseño para el procesamiento incremental. Estos pasos se pueden utilizar como plantilla para crear sus propias consultas de carga de datos incrementales.

## Introducción

Los ejemplos de SQL a lo largo de este documento requieren que comprenda las capacidades de bloqueo anónimo e instantánea. Se recomienda leer la documentación de [consultas de bloque anónimas de ejemplo](./anonymous-block.md) y también la documentación de [cláusula de instantánea](../sql/syntax.md#snapshot-clause).

Para obtener instrucciones sobre cualquier terminología utilizada en esta guía, consulte la [guía de sintaxis SQL](../sql/syntax.md).

## Carga incremental de datos

Los pasos siguientes muestran cómo crear y cargar datos de forma incremental mediante instantáneas y la función de bloque anónimo. El patrón de diseño se puede utilizar como plantilla para su propia secuencia de consultas.

1. Cree una tabla `checkpoint_log` para realizar el seguimiento de la instantánea más reciente utilizada para procesar datos correctamente. La tabla de seguimiento (`checkpoint_log` en este ejemplo) debe inicializarse primero en `null` para procesar de forma incremental un conjunto de datos.

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

1. Rellene la tabla `checkpoint_log` con un registro vacío para el conjunto de datos que necesita procesamiento incremental. `DIM_TABLE_ABC` es el conjunto de datos que se procesará en el ejemplo siguiente. En la primera vez que se procese `DIM_TABLE_ABC`, `last_snapshot_id` se inicializó como `null`. Esto le permite procesar todo el conjunto de datos la primera vez e incrementalmente a partir de entonces.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. A continuación, inicialice `DIM_TABLE_ABC_Incremental` para que contenga el resultado procesado de `DIM_TABLE_ABC`. El bloque anónimo de la sección de ejecución **required** del ejemplo de SQL siguiente, tal como se describe en los pasos del uno al cuatro, se ejecuta secuencialmente para procesar los datos de forma incremental.

   1. Establezca `from_snapshot_id`, que indica desde dónde comienza el procesamiento. Se ha consultado el elemento `from_snapshot_id` del ejemplo en la tabla `checkpoint_log` para su uso con `DIM_TABLE_ABC`. En la primera ejecución, el ID de instantánea será `null`, lo que significa que se procesará todo el conjunto de datos.
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
     WHEN OTHER THEN
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
     WHEN OTHER THEN
       SELECT 'ERROR';
   END
   $$;
   ```

Esta lógica se puede aplicar a cualquier tabla para realizar cargas incrementales.

## Instantáneas caducadas

>[!IMPORTANT]
>
>Los metadatos de la instantánea caducan al cabo de **dos** días. Una instantánea caducada invalida la lógica de la secuencia de comandos proporcionada anteriormente.

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
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```

## Pasos siguientes

Al leer este documento, debería comprender mejor cómo utilizar las funciones de bloqueo anónimo e instantáneas para realizar cargas incrementales y puede aplicar esta lógica a sus propias consultas específicas. Para obtener instrucciones generales sobre la ejecución de consultas, lea la [guía sobre la ejecución de consultas en el servicio de consultas](../best-practices/writing-queries.md).
