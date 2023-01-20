---
title: Bloque anónimo en el servicio de consulta
description: El bloque anónimo es una sintaxis SQL admitida por Adobe Experience Platform Query Service, que le permite ejecutar de forma eficaz una secuencia de consultas
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Bloque anónimo en el servicio de consulta

El servicio de consulta de Adobe Experience Platform admite bloques anónimos. La función de bloque anónimo permite encadenar una o más instrucciones SQL que se ejecutan en secuencia. También permiten la opción de la gestión de excepciones.

La función de bloque anónimo es una forma eficaz de realizar una secuencia de operaciones o consultas. La cadena de consultas dentro del bloque se puede guardar como una plantilla y programarse para ejecutarse en un intervalo o una hora determinados. Estas consultas se pueden utilizar para escribir y anexar datos con el fin de crear un nuevo conjunto de datos, y normalmente se utilizan cuando tiene una dependencia.

>[!IMPORTANT]
>
>Actualmente, la programación de consultas mediante bloques anónimos solo es posible a través de la variable [!DNL Query Service] API. Consulte la documentación para [instrucciones completas para programar consultas a través de la API](../api/scheduled-queries.md).

La tabla proporciona un desglose de las secciones principales del bloque: ejecución y gestión de excepciones. Las secciones están definidas por las palabras clave `BEGIN`, `END`y `EXCEPTION`.

| sección | description |
|---|---|
| execution | Una sección ejecutable comienza con la palabra clave `BEGIN` y termina con la palabra clave `END`. Cualquier conjunto de instrucciones incluidas en la variable `BEGIN` y `END` las palabras clave se ejecutarán en secuencia y garantizarán que las consultas subsiguientes no se ejecutarán hasta que se haya completado la consulta anterior en la secuencia. |
| control de excepciones | La sección opcional de administración de excepciones comienza con la palabra clave `EXCEPTION`. Contiene el código para capturar y gestionar excepciones en caso de que falle cualquiera de las instrucciones SQL de la sección de ejecución. Si falla alguna de las consultas, se detiene todo el bloque. |

Cabe señalar que un bloque es una instrucción ejecutable y, por lo tanto, puede anidarse dentro de otros bloques.

>[!NOTE]
>
> Se recomienda encarecidamente probar las consultas en conjuntos de datos más pequeños y asegurarse de que funcionan según lo esperado. Si una consulta tiene un error de sintaxis, se produce la excepción y se anula todo el bloque. Una vez verificada la integridad de las consultas, puede comenzar a encadenarlas. Esto garantiza que el bloque funcione según lo esperado antes de ponerlo en funcionamiento.

## Ejemplos de consultas de bloques anónimas

La siguiente consulta muestra un ejemplo de cómo encadenar sentencias SQL. Consulte la [Sintaxis SQL en Query Service](../sql/syntax.md) documento para obtener más información sobre cualquiera de las sintaxis SQL utilizadas.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

En el ejemplo siguiente, `SET` persiste en el resultado de un `SELECT` en la variable local especificada. La variable tiene un alcance del bloque anónimo.

El ID de la instantánea se almacena como una variable local (`@current_sid`). A continuación, se utiliza en la siguiente consulta para devolver resultados basados en la SNAPSHOT de la misma tabla o conjunto de datos.

Una instantánea de base de datos es una vista estática de sólo lectura de una base de datos de SQL Server. Para obtener más información [información sobre la cláusula de instantánea](../sql/syntax.md#SNAPSHOT-clause) consulte la documentación de sintaxis SQL.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Pasos siguientes

Al leer este documento, ahora tiene una clara comprensión de los bloques anónimos y de cómo están estructurados. [Para obtener más información sobre la ejecución de consultas](../best-practices/writing-queries.md), lea la guía sobre la ejecución de consultas en el servicio de consultas.

También debería leer acerca de [cómo se utiliza el bloque anónimo con el patrón de diseño de carga incremental](./incremental-load.md) para aumentar la eficacia de las consultas.
