---
title: Ejemplo de consultas de bloques anónimas
description: 'El bloque anónimo es una sintaxis SQL admitida por el servicio de consulta de Adobe Experience Platform, que le permite ejecutar de forma eficaz una secuencia de consultas '
source-git-commit: dffa03d9ab8e26e2c99a359ae000022d6d469572
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Consultas de ejemplo para el bloque Anonymous

El servicio de consulta de Adobe Experience Platform admite bloques anónimos. La función de bloque anónimo permite encadenar una o más instrucciones SQL que se ejecutan en secuencia. También permiten la opción de la gestión de excepciones.

La función de bloque anónimo es una forma eficaz de realizar una secuencia de operaciones o consultas. La cadena de consultas dentro del bloque se puede guardar como una plantilla y programarse para ejecutarse en un intervalo o una hora determinados. Estas consultas se pueden utilizar para escribir y anexar datos con el fin de crear un nuevo conjunto de datos, y normalmente se utilizan cuando tiene una dependencia.

La tabla proporciona un desglose de las secciones principales del bloque: ejecución y gestión de excepciones. Las secciones están definidas por las palabras clave `BEGIN`, `END` y `EXCEPTION`.

| sección | descripción |
|---|---|
| execution | Una sección ejecutable comienza con la palabra clave `BEGIN` y termina con la palabra clave `END`. Cualquier conjunto de instrucciones incluidas en las palabras clave `BEGIN` y `END` se ejecutará en secuencia y garantiza que las consultas subsiguientes no se ejecutarán hasta que se haya completado la consulta anterior de la secuencia. |
| control de excepciones | La sección opcional de administración de excepciones comienza con la palabra clave `EXCEPTION`. Contiene el código para capturar y gestionar excepciones en caso de que falle cualquiera de las instrucciones SQL de la sección de ejecución. Si falla alguna de las consultas, se detiene todo el bloque. |

Cabe señalar que un bloque es una instrucción ejecutable y, por lo tanto, se puede anidar dentro de otros bloques.

>[!NOTE]
>
> Se recomienda encarecidamente probar las consultas en conjuntos de datos más pequeños y asegurarse de que funcionan según lo esperado. Si una consulta tiene un error de sintaxis, se produce la excepción y se anula todo el bloque. Una vez verificada la integridad de las consultas, puede comenzar a encadenarlas. Esto garantiza que el bloque funcione según lo esperado antes de ponerlo en funcionamiento.

## Ejemplos de consultas de bloques anónimas

La siguiente consulta muestra un ejemplo de cómo encadenar sentencias SQL. Consulte el documento [SQL sintaxis en Query Service](../sql/syntax.md) para obtener más información sobre cualquiera de las sintaxis SQL utilizadas.

```SQL
$$BEGIN
     
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
     
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
     
END$$;
```

<!-- The block below uses `SET` to persist the result of a select query with a variable. It is used in the anonymous block to store the response from a query as a local variable for use with the `SNAPSHOT` feature. -->

En el ejemplo siguiente, `SET` persiste en el resultado de una consulta `SELECT` en la variable local especificada. La variable tiene un alcance del bloque anónimo.

El ID de instantánea se almacena como una variable local (`@current_sid`). A continuación, se utiliza en la siguiente consulta para devolver resultados basados en la SNAPSHOT de la misma tabla o conjunto de datos.

Una instantánea de base de datos es una vista estática de sólo lectura de una base de datos de SQL Server. Para obtener más [información sobre la cláusula de instantánea](../sql/syntax.md#SNAPSHOT-clause), consulte la documentación de sintaxis SQL.

```SQL
$$BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                                     
END$$;
```

## Pasos siguientes

Al leer este documento, ahora tiene una clara comprensión de los bloques anónimos y de cómo están estructurados. [Para obtener más información sobre la ejecución](./writing-queries.md) de consultas, lea la guía sobre la ejecución de consultas en el servicio de consultas.

Para obtener más ejemplos de consultas que se pueden utilizar dentro del servicio de consulta, lea las guías sobre [Adobe Analytics sample queries](./adobe-analytics.md), [Adobe Target sample queries](./adobe-target.md) o [ExperienceEvent sample queries](./experience-event-queries.md).
