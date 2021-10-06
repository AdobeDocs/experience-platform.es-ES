---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;guía de solución de problemas;preguntas frecuentes;solución de problemas;
solution: Experience Platform
title: Guía de solución de problemas del servicio de consultas
topic-legacy: troubleshooting
description: Este documento contiene información sobre los códigos de error comunes que encuentra y las posibles causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 42288ae7db6fb19bc0a0ee8e4ecfa50b7d63d017
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 4%

---

# [!DNL Query Service] guía de solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes sobre el servicio de consultas y proporciona una lista de códigos de error que se ven con más frecuencia al utilizar el servicio de consultas. Para preguntas y solución de problemas relacionados con otros servicios de Adobe Experience Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

## Preguntas frecuentes

A continuación se ofrece una lista de respuestas a las preguntas más frecuentes sobre el servicio de consultas.

### ¿Cómo puedo obtener solo los metadatos de una consulta?

Para obtener solo los metadatos de una consulta, puede ejecutar una consulta que devuelva cero filas, de la siguiente manera:

```sql
SELECT * FROM <table> WHERE 1=0
```

Esta consulta solo devuelve los metadatos de la tabla especificada.

### ¿Cómo puedo iterar rápidamente en una consulta CTAS (Crear tabla como selección) sin materializarla?

Puede crear tablas temporales para iterar y experimentar rápidamente en una consulta antes de materializarla para utilizarla. También puede utilizar tablas temporales para validar si una consulta funciona.

Por ejemplo, puede crear una tabla temporal:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

A continuación, puede utilizar la tabla temporal de la siguiente manera:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### ¿Cómo debo filtrar mis datos de series temporales?

Al consultar los datos de series temporales, debe utilizar el filtro de marcas de tiempo siempre que sea posible para realizar un análisis más preciso.

>[!NOTE]
>
> La cadena de fecha **debe** tener el formato `yyyy-mm-ddTHH24:MM:SS`.

A continuación se puede ver un ejemplo del uso del filtro de marca de tiempo:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### ¿Debo usar caracteres comodín, como *, para obtener todas las filas de mis conjuntos de datos?

No puede utilizar caracteres comodín para obtener todos los datos de las filas, ya que el servicio de consulta debe tratarse como **almacén de columnas** en lugar de como sistema de almacén tradicional basado en filas.

### ¿Debería utilizar `NOT IN` en mi consulta SQL?

El operador `NOT IN` se utiliza a menudo para recuperar filas que no se encuentran en otra tabla o instrucción SQL. Este operador puede ralentizar el rendimiento y devolver resultados inesperados si las columnas que se comparan aceptan `NOT NULL` o si tiene un gran número de registros.

En lugar de utilizar `NOT IN`, puede utilizar `NOT EXISTS` o `LEFT OUTER JOIN`.

Por ejemplo, si tiene creadas las tablas siguientes:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Si utiliza el operador `NOT EXISTS` , puede duplicar con el operador `NOT IN` mediante la siguiente consulta:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Alternativamente, si está utilizando el operador `LEFT OUTER JOIN`, puede replicar utilizando el operador `NOT IN` utilizando la siguiente consulta:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### ¿Cuál es el uso correcto de los operadores `OR` y `UNION`?

### ¿Cómo utilizo correctamente el operador `CAST` para convertir mis marcas de hora en consultas SQL?

Al utilizar el operador `CAST` para convertir una marca de tiempo, debe incluir la fecha **y la hora**.

Por ejemplo, si falta el componente de tiempo, como se muestra a continuación, se producirá un error:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

A continuación se muestra un uso correcto del operador `CAST`:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

## Errores de API de REST

| Código de estado HTTP | Descripción | Posibles causas |
| ---------------- | ----------- | --------------- |
| 400 | Solicitud incorrecta | Consulta no formada o no válida |
| 401 | Error de autenticación | Token de autenticación no válido |
| 500 | Error interno del servidor | Fallo interno del sistema |

## Errores de API PostgreSQL

| Código de error | Estado de la conexión | Descripción | Posible causa |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | N/D | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
| **28P01** | Inicio: autenticación | Contraseña no válida | Token de autenticación no válido |
| **28000** | Inicio: autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **42P12** | Inicio: autenticación | No se encontraron tablas | No se encontraron tablas para su uso |
| **42601** | Consulta | Error de sintaxis | Error de sintaxis o comando no válido |
| **42P01** | Consulta | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **42P07** | Consulta | La tabla existe | Ya existe una tabla con el mismo nombre (CREATE TABLE) |
| **53400** | Consulta | El LÍMITE supera el valor máximo | El usuario especificó una cláusula LIMIT superior a 100.000 |
| **53400** | Consulta | Tiempo de espera de la instrucción | La declaración en directo presentada tardó más de 10 minutos |
| **58000** | Consulta | Error del sistema | Fallo interno del sistema |
| **0A000** | Consulta/Comando | No admitido | La función/funcionalidad de la consulta/comando no es compatible |
| **42501** | Consulta de TABLA DE COLOCACIÓN | El servicio de consulta no crea la tabla de pérdidas | El servicio de consultas no creó la tabla que se está quitando con la instrucción `CREATE TABLE` |
| **42501** | Consulta de TABLA DE COLOCACIÓN | Tabla no creada por el usuario autenticado | El usuario que ha iniciado sesión actualmente no ha creado la tabla que se está quitando |
| **42P01** | Consulta de TABLA DE COLOCACIÓN | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **42P12** | Consulta de TABLA DE COLOCACIÓN | No se encontró ninguna tabla para `dbName`: compruebe el `dbName` | No se encontraron tablas en la base de datos actual |
