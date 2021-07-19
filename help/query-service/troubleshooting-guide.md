---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;guía de solución de problemas;preguntas frecuentes;solución de problemas;
solution: Experience Platform
title: Guía de solución de problemas del servicio de consultas
topic-legacy: troubleshooting
description: Este documento contiene información sobre los códigos de error comunes que encuentra y las posibles causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: e3557fe75680153f051b8a864ad8f6aca5f743ee
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

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
WHERE timestamp >= To_timestamp('2021-01-21 12:00:00')
AND timestamp < To_timestamp('2021-01-21 13:00:00')
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

| Código de error y estado de conexión | Descripción | Posible causa |
| ------------------------------- | ----------- | -------------- |
| **28P01** Inicio: autenticación | Contraseña no válida | Token de autenticación no válido |
| **28000** Inicio: autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **42P12** Inicio: autenticación | No se encontraron tablas | No se encontraron tablas para su uso |
| **Consulta 42601**  | Error de sintaxis | Error de sintaxis o comando no válido |
| **Consulta 58000**  | Error del sistema | Fallo interno del sistema |
| **Consulta 42P01**  | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **Consulta 42P07**  | La tabla existe | La tabla ya existe con el mismo nombre (CREATE TABLE) |
| **Consulta 53400**  | El LÍMITE supera el valor máximo | El usuario especificó una cláusula LIMIT superior a 100.000 |
| **Consulta 53400**  | Tiempo de espera de la instrucción | La declaración en directo presentada tardó más de 10 minutos |
| **08P01** N/D | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
