---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;guía de solución de problemas;preguntas frecuentes;solución de problemas;
solution: Experience Platform
title: Guía de solución de problemas del servicio de consultas
topic-legacy: troubleshooting
description: Este documento contiene información sobre los códigos de error comunes que encuentra y las posibles causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 2b118228473a5f07ab7e2c744b799f33a4c44c98
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 6%

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
