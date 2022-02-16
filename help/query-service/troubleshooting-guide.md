---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;guía de solución de problemas;preguntas frecuentes;solución de problemas;
solution: Experience Platform
title: Guía de solución de problemas del servicio de consultas
topic-legacy: troubleshooting
description: Este documento contiene información sobre los códigos de error comunes que encuentra y las posibles causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 03cd013e35872bcc30c68508d9418cb888d9e260
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 3%

---

# [!DNL Query Service] guía de solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes sobre el servicio de consultas y proporciona una lista de códigos de error que se ven con más frecuencia al utilizar el servicio de consultas. Para preguntas y solución de problemas relacionados con otros servicios de Adobe Experience Platform, consulte la [Guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

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

### ¿Cómo puedo cambiar la zona horaria a y desde una marca de tiempo UTC?

Adobe Experience Platform mantiene los datos en formato UTC (hora universal coordinada). Un ejemplo del formato UTC es `2021-12-22T19:52:05Z`

El servicio de consulta admite funciones SQL integradas para convertir una marca de tiempo determinada a formato UTC y desde él. Ambas `to_utc_timestamp()` y `from_utc_timestamp()` Los métodos emplean dos parámetros: marca de tiempo y zona horaria.

| Parámetro | Descripción |
|---|---|
| Marca de tiempo | La marca de tiempo puede escribirse en formato UTC o en formato simple `{year-month-day}` formato. Si no se proporciona ninguna hora, el valor predeterminado es la medianoche de la mañana de un día determinado. |
| Zona horaria | La zona horaria se escribe en un `{continent/city})` formato. Debe ser uno de los códigos de zona horaria reconocidos, tal como se encuentran en la variable [base de datos TZ de dominio público](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Convertir a la marca de tiempo UTC

La variable `to_utc_timestamp()` interpreta los parámetros dados y los convierte **a la marca de tiempo de su zona horaria local** en formato UTC. Por ejemplo, la zona horaria de Seúl, Corea del Sur, es UTC/GMT +9 horas. Al proporcionar una marca de hora de solo fecha, el método utiliza un valor predeterminado de medianoche por la mañana. La marca de tiempo y la zona horaria se convierten al formato UTC desde la hora de esa región hasta la marca de tiempo UTC de su región local.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

La consulta devuelve una marca de tiempo en la hora local del usuario. En este caso, las 3 pm del día anterior, ya que Seúl tiene nueve horas de anticipación.

```
2021-08-30 15:00:00
```

Otro ejemplo: si la marca de tiempo dada era `2021-07-14 12:40:00.0` para el `Asia/Seoul` zona horaria, la marca de tiempo UTC devuelta sería `2021-07-14 03:40:00.0`

El resultado de la consola que se proporciona en la interfaz de usuario del servicio de consulta es un formato más legible por el ser humano:

```
8/30/2021, 3:00 PM
```

### Convertir desde la marca de tiempo UTC

La variable `from_utc_timestamp()` interpreta los parámetros dados **desde la marca de tiempo de su zona horaria local** y proporciona la marca de tiempo equivalente de la región deseada en formato UTC. En el siguiente ejemplo, la hora es las 2:40 p.m. en la zona horaria local del usuario. La zona horaria de Seúl que se pasa como variable supera las nueve horas de la zona horaria local.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La consulta devuelve una marca de tiempo en formato UTC para la zona horaria transferida como parámetro. El resultado es nueve horas antes de la zona horaria que ejecutó la consulta.

```
8/31/2021, 11:40 PM
```

### ¿Cómo debo filtrar mis datos de series temporales?

Al consultar los datos de series temporales, debe utilizar el filtro de marcas de tiempo siempre que sea posible para realizar un análisis más preciso.

>[!NOTE]
>
> La cadena de fecha **must** estar en formato `yyyy-mm-ddTHH24:MM:SS`.

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

No puede utilizar comodines para obtener todos los datos de las filas, ya que el servicio de consultas debe tratarse como un **almacén de columnas** en lugar de un sistema de tienda tradicional basado en filas.

### ¿Debería usar `NOT IN` en mi consulta SQL?

La variable `NOT IN` se utiliza a menudo para recuperar filas que no se encuentran en otra tabla o instrucción SQL. Este operador puede ralentizar el rendimiento y devolver resultados inesperados si las columnas que se comparan aceptan `NOT NULL`o tiene un gran número de registros.

En lugar de usar `NOT IN`, puede usar una de las opciones siguientes: `NOT EXISTS` o `LEFT OUTER JOIN`.

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

Si está utilizando la variable `NOT EXISTS` operador, puede replicar utilizando la variable `NOT IN` mediante la siguiente consulta:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Alternativamente, si está utilizando la variable `LEFT OUTER JOIN` operador, puede replicar utilizando el `NOT IN` mediante la siguiente consulta:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### ¿Cuál es el uso correcto de la variable `OR` y `UNION` operadores?

### ¿Cómo utilizo correctamente el `CAST` operador para convertir mis marcas de hora en consultas SQL?

Al usar la variable `CAST` para convertir una marca de tiempo, debe incluir ambas fechas **y** tiempo.

Por ejemplo, si falta el componente de tiempo, como se muestra a continuación, se producirá un error:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Un uso correcto de la variable `CAST` se muestra a continuación:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### ¿Cómo puedo descargar los resultados de mi consulta como archivo CSV?

Esta no es una función que el servicio de consulta ofrezca directamente. Sin embargo, si la variable [!DNL PostgreSQL] cliente utilizado para conectarse al servidor de base de datos tiene la capacidad , la respuesta de una consulta SELECT se puede escribir y descargar como archivo CSV. Consulte la documentación de la utilidad o herramienta de terceros que está utilizando para obtener aclaraciones sobre este proceso.

## Errores de API de REST

| Código de estado HTTP | Descripción | Posibles causas |
| ---------------- | ----------- | --------------- |
| 400 | Solicitud incorrecta | Consulta no formada o no válida |
| 401 | Error de autenticación | Token de autenticación no válido |
| 500 | Error interno del servidor | Fallo interno del sistema |

## Errores de API PostgreSQL

| Código de error | Estado de la conexión | Descripción | Posible causa |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | N/A | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
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
| **42501** | Consulta de TABLA DE COLOCACIÓN | El servicio de consulta no crea la tabla de pérdidas | El servicio de consultas no creó la tabla que se está soltando mediante el `CREATE TABLE` statement |
| **42501** | Consulta de TABLA DE COLOCACIÓN | Tabla no creada por el usuario autenticado | El usuario que ha iniciado sesión actualmente no ha creado la tabla que se está quitando |
| **42P01** | Consulta de TABLA DE COLOCACIÓN | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **42P12** | Consulta de TABLA DE COLOCACIÓN | No se encontró ninguna tabla para `dbName`: compruebe el `dbName` | No se encontraron tablas en la base de datos actual |
