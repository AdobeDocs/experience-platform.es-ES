---
title: Bloque anónimo en el servicio de consultas
description: El bloque anónimo es una sintaxis SQL admitida por Adobe Experience Platform Query Service, que le permite ejecutar de forma eficaz una secuencia de consultas
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 9193ba821409806cd7b4667c5de73a0cf2660c66
workflow-type: tm+mt
source-wordcount: '616'
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

## Ejemplos de consultas de bloque anónimas

La siguiente consulta muestra un ejemplo de encadenamiento de instrucciones SQL. Consulte el documento [Sintaxis SQL en Query Service](../sql/syntax.md) para obtener más información sobre cualquiera de las sintaxis SQL utilizadas.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

En el ejemplo siguiente, `SET` conserva el resultado de una consulta `SELECT` en la variable local especificada. La variable está vinculada al bloque anónimo.

El id. de instantánea se almacena como variable local (`@current_sid`). A continuación, se utiliza en la siguiente consulta para devolver resultados basados en la INSTANTÁNEA del mismo conjunto de datos o tabla.

Una instantánea de base de datos es una vista estática de sólo lectura de una base de datos de SQL Server. Para obtener más [información sobre la cláusula de instantánea](../sql/syntax.md#SNAPSHOT-clause), consulte la documentación de sintaxis SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Bloque anónimo con clientes de terceros {#third-party-clients}

Algunos clientes de terceros pueden requerir un identificador independiente antes y después de un bloque SQL para indicar que una parte de la secuencia de comandos debe gestionarse como una sola instrucción. Si recibe un mensaje de error al utilizar el servicio de consulta con un cliente de terceros, debe consultar la documentación del cliente de terceros sobre el uso de un bloque SQL.

Por ejemplo, **DbVisualizer** requiere que el delimitador sea el único texto de la línea. En DbVisualizer, el valor predeterminado para el identificador inicial es `--/` y para el identificador final es `/`. A continuación se muestra un ejemplo de bloque anónimo en DbVisualizer:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

Para DbVisualizer en particular, también hay una opción en la IU para &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. Consulte la [documentación de DbVisualizer](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) para obtener más información.

## Pasos siguientes

Al leer este documento, ahora tiene una comprensión clara de los bloques anónimos y de cómo están estructurados. Lea la [guía de ejecución de consultas](../best-practices/writing-queries.md) para obtener más información sobre cómo escribir consultas.

También debería leer acerca de [cómo se usan los bloques anónimos con el patrón de diseño de carga incremental](./incremental-load.md) para aumentar la eficacia de la consulta.
