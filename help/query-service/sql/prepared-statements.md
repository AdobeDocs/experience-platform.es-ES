---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;instrucciones preparadas;preparado;sql;
solution: Experience Platform
title: Sentencias preparadas en el servicio de Consulta
topic: prepared statements
description: En SQL, las instrucciones preparadas se utilizan para crear plantillas de consultas o actualizaciones similares. El servicio de Consulta de Adobe Experience Platform admite las declaraciones preparadas mediante una consulta parametrizada.
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---


# Declaraciones preparadas

En SQL, las sentencias preparadas se utilizan para crear plantillas de consultas o actualizaciones similares. Adobe Experience Platform [!DNL Query Service] admite instrucciones preparadas mediante una consulta parametrizada. Esto se puede utilizar para optimizar el rendimiento, ya que ya no tendrá que volver a analizar una consulta una y otra vez.

## Uso de declaraciones preparadas

Al utilizar instrucciones preparadas, se admiten las siguientes sintaxis:

- [PREPARAR](#prepare)
- [EJECUTAR](#execute)
- [DESASIGNAR](#deallocate)

### Preparar una declaración preparada {#prepare}

Esta consulta SQL guarda la consulta SELECT escrita con el nombre dado como `PLAN_NAME`. Puede utilizar variables como `$1` en lugar de valores reales. Esta declaración preparada se guardará durante la sesión actual. Tenga en cuenta que los nombres de los planes **no distinguen entre mayúsculas y minúsculas**.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### SQL de muestra

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Ejecutar una instrucción preparada {#execute}

Esta consulta SQL utiliza la instrucción preparada que se creó anteriormente.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### SQL de muestra

```sql
EXECUTE test('canada', 'vancouver');
```

### Desasignar una instrucción preparada {#deallocate}

Esta consulta SQL se utiliza para eliminar la instrucción preparada con nombre.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### SQL de muestra

```sql
DEALLOCATE test;
```

## Flujo de ejemplo con afirmaciones preparadas

Inicialmente, puede tener una consulta SQL, como la siguiente:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

La consulta SQL anterior devolverá la siguiente respuesta:

| id | firstname | lastname | fecha de nacimiento | email | city | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | París | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokio | Japón |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Estocolmo | Suecia |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Esta consulta SQL se puede parametrizar mediante la siguiente instrucción preparada:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Ahora, la instrucción preparada se puede ejecutar mediante la siguiente llamada:

```sql
EXECUTE getIdRange(10000, 10005);
```

Cuando se llame a esto, verá exactamente los mismos resultados que antes:

| id | firstname | lastname | fecha de nacimiento | correo electrónico | ciudad | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | París | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokio | Japón |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Estocolmo | Suecia |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Una vez que haya terminado de utilizar la instrucción preparada, puede deslocalizarla mediante la siguiente llamada:

```sql
DEALLOCATE getIdRange;
```
