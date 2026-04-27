---
title: Bloque anónimo en el servicio de consultas
description: El bloque anónimo es una sintaxis SQL admitida por Adobe Experience Platform Query Service, que le permite ejecutar de forma eficaz una secuencia de consultas
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: f2d81f05c8c19c6f28849fc4dbe9bfa26be64645
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Bloque anónimo en el servicio de consultas

El servicio de consultas de Adobe Experience Platform admite bloques anónimos. La función de bloque anónimo permite encadenar una o más sentencias SQL que se ejecutan en secuencia. También permiten la opción de la gestión de excepciones.

La función de bloques anónimos es una forma eficaz de realizar una secuencia de operaciones o consultas. La cadena de consultas dentro del bloque se puede guardar como plantilla y programarse para ejecutarse a una hora o intervalo determinados. Estas consultas se pueden utilizar para escribir y anexar datos para crear un nuevo conjunto de datos y, normalmente, se utilizan donde tiene una dependencia.

La tabla proporciona un desglose de las secciones principales del bloque: ejecución y control de excepciones. Las secciones están definidas por las palabras clave `BEGIN`, `END` y `EXCEPTION`.

| sección | descripción |
|---|---|
| ejecución | Una sección ejecutable comienza con la palabra clave `BEGIN` y termina con la palabra clave `END`. Cualquier conjunto de instrucciones incluidas en las palabras clave `BEGIN` y `END` se ejecutará en secuencia y garantiza que las consultas subsiguientes no se ejecutarán hasta que se haya completado la consulta anterior de la secuencia. |
| control de excepciones | La sección opcional de control de excepciones comienza con la palabra clave `EXCEPTION`. Contiene el código para detectar y controlar las excepciones en caso de que alguna de las instrucciones SQL de la sección de ejecución falle. Si alguna de las consultas falla, se detiene todo el bloque. |

Cabe señalar que un bloque es una instrucción ejecutable y, por lo tanto, se puede anidar dentro de otros bloques.

>[!NOTE]
>
> Se recomienda encarecidamente probar las consultas en conjuntos de datos más pequeños y asegurarse de que funcionan según lo esperado. Si una consulta tiene un error de sintaxis, se generará la excepción y se anulará todo el bloque. Una vez verificada la integridad de las consultas, puede empezar a encadenarlas. Esto garantiza que el bloque funcione según lo esperado antes de ponerlo en funcionamiento.

## Sample anonymous block queries

The following query shows an example of chaining SQL statements. See the [SQL syntax in Query Service](../sql/syntax.md) document for more information on any of the SQL syntax used.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHERS THEN SET @ret = SELECT 'ERROR';
END
$$;
```

In the example below, `SET` persists the result of a `SELECT` query in the specified local variable. The variable is scoped to the anonymous block.

The snapshot ID is stored as a local variable (`@current_sid`). It is then used in the next query to return results based on the SNAPSHOT from the same dataset/table. For more [information on the snapshot clause](../sql/syntax.md#SNAPSHOT-clause) see the SQL syntax documentation.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Anonymous block with third-party clients {#third-party-clients}

Certain third-party clients may require a separate identifier before and after an SQL block to indicate that a part of the script should be handled as a single statement. If you receive an error message when using Query Service with a third-party client, you should refer to the documentation of the third-party client regarding the use of an SQL block.

For example, **DbVisualizer** requires that the delimiter must be the only text on the line. In DbVisualizer, the default value for the Begin Identifier is `--/` and for the End Identifier it is `/`. An example of an anonymous block in DbVisualizer is seen below:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHERS THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

For DbVisualizer in particular, there is also an option in the UI to &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. See the [DbVisualizer documentation](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) for more information.

## Próximos pasos

By reading this document, you now have a clear understanding of anonymous blocks and how they are structured. Please read the [query execution guide](../best-practices/writing-queries.md) for more information on writing queries.

You should also read about [how anonymous blocks are used with the incremental load design pattern](./incremental-load.md) to increase query efficiency.
