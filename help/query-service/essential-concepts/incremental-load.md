---
title: Carga incremental en el servicio de consulta
description: La función de carga incremental utiliza funciones de bloques anónimos y de instantánea para proporcionar una solución casi en tiempo real que permita mover datos del lago de datos al almacén de datos e ignorar los datos coincidentes.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Carga incremental en el servicio de consulta

El patrón de diseño de carga incremental es una solución para administrar datos. El patrón solo procesa la información del conjunto de datos que se ha creado o modificado desde la última ejecución de carga.

La carga incremental utiliza varias funciones proporcionadas por el servicio de consulta de Adobe Experience Platform, como bloques anónimos e instantáneas. Este patrón de diseño aumenta la eficacia del procesamiento, ya que cualquier dato que ya se haya procesado desde el origen se omite. Se puede utilizar tanto con el procesamiento de datos por flujo continuo como por lotes.

Este documento proporciona una serie de instrucciones para crear un patrón de diseño para el procesamiento incremental. Estos pasos se pueden utilizar como plantilla para crear sus propias consultas de carga de datos incrementales.

## Primeros pasos

Los ejemplos SQL de este documento requieren que conozca las capacidades anónimas de bloque y instantánea. Se recomienda leer el [muestras de consultas de bloques anónimas](./anonymous-block.md) y también la [cláusula de instantánea](../sql/syntax.md#snapshot-clause) documentación.

Para obtener instrucciones sobre cualquier terminología utilizada en esta guía, consulte la [Guía de sintaxis SQL](../sql/syntax.md).

## Carga incremental de datos

Los pasos siguientes muestran cómo crear y cargar datos de forma incremental mediante instantáneas y la función de bloques anónimos. El patrón de diseño se puede utilizar como plantilla para su propia secuencia de consultas.

1 Cree un `checkpoint_log` para realizar un seguimiento de la instantánea más reciente utilizada para procesar los datos correctamente. La tabla de seguimiento (`checkpoint_log` en este ejemplo) primero debe inicializarse a `null` para procesar un conjunto de datos de forma incremental.

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

2 Rellene el `checkpoint_log` con un registro vacío para el conjunto de datos que necesita procesamiento incremental. `DIM_TABLE_ABC` es el conjunto de datos que se va a procesar en el ejemplo siguiente. En la primera ocasión de la transformación `DIM_TABLE_ABC`, el `last_snapshot_id` se inicializa como `null`. Esto le permite procesar todo el conjunto de datos en la primera vez e incrementarlo posteriormente.

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3 A continuación, inicialice `DIM_TABLE_ABC_Incremental` para contener la salida procesada de `DIM_TABLE_ABC`. El bloque anónimo de la variable **obligatorio** la sección de ejecución del ejemplo SQL a continuación, como se describe en los pasos uno a cuatro, se ejecuta secuencialmente para procesar los datos de forma incremental.

1. Configure las variables `from_snapshot_id` que indica desde dónde comienza el procesamiento. La variable `from_snapshot_id` en el ejemplo se consulta desde el `checkpoint_log` tabla para usar con `DIM_TABLE_ABC`. En la ejecución inicial, el ID de instantánea será `null` lo que significa que se procesará todo el conjunto de datos.
2. Configure las variables `to_snapshot_id` como ID de instantánea actual de la tabla de origen (`DIM_TABLE_ABC`). En el ejemplo, esto se consulta desde la tabla de metadatos de la tabla de origen.
3. Utilice la variable `CREATE` palabra clave que crear `DIM_TABLE_ABC_Incremenal` como tabla de destino. La tabla de destino conserva los datos procesados del conjunto de datos de origen (`DIM_TABLE_ABC`). Esto permite procesar los datos de la tabla de origen entre `from_snapshot_id` y `to_snapshot_id`, que se anexará gradualmente a la tabla de destino.
4. Actualice el `checkpoint_log` con la variable `to_snapshot_id` para los datos de origen que `DIM_TABLE_ABC` se ha procesado correctamente.
5. Si falla alguna de las consultas ejecutadas secuencialmente del bloque anónimo, la variable **opcional** se ejecuta. Esto devuelve un error y finaliza el proceso.

>[!NOTE]
>
>La variable `history_meta('source table name')` es un método conveniente que se utiliza para obtener acceso a instantáneas disponibles en un conjunto de datos.

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

4 Utilice la lógica de carga de datos incrementales en el ejemplo de bloque anónimo a continuación para permitir que cualquier nuevo dato del conjunto de datos de origen (desde la marca de tiempo más reciente), se procese y se añada a la tabla de destino en una cadencia normal. En el ejemplo, los datos cambian a `DIM_TABLE_ABC` se procesarán y adjuntarán a `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` es la clave principal en ambos `DIM_TABLE_ABC_Incremental` y `SELECT history_meta('DIM_TABLE_ABC')`.

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
>Los metadatos de la instantánea caducan después de **two** días. Una instantánea caducada invalida la lógica de la secuencia de comandos proporcionada anteriormente.

Para resolver el problema de un ID de instantánea caducado, inserte el siguiente comando al principio del bloque anónimo. La siguiente línea de código anula la función `@from_snapshot_id` con la versión más temprana disponible `snapshot_id` de metadatos.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

El bloque de código completo tiene el siguiente aspecto:

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

Al leer este documento, debe comprender mejor cómo utilizar las funciones de bloque anónimo y de instantánea para realizar cargas incrementales y puede aplicar esta lógica a sus propias consultas específicas. Para obtener instrucciones generales sobre la ejecución de consultas, lea la [guía sobre la ejecución de consultas en Query Service](../best-practices/writing-queries.md).
