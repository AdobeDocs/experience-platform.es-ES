---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;instrucciones preparadas;preparado;sql;
solution: Experience Platform
title: Instrucciones preparadas en el servicio de consultas
description: En SQL, las instrucciones preparadas se utilizan para crear plantillas de consultas o actualizaciones similares. El servicio de consulta de Adobe Experience Platform admite instrucciones preparadas mediante una consulta parametrizada.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 5%

---

# Instrucciones preparadas

En SQL, las instrucciones preparadas se utilizan para crear plantillas de consultas o actualizaciones similares. Adobe Experience Platform [!DNL Query Service] admite instrucciones preparadas mediante una consulta parametrizada. Esto puede optimizar el rendimiento, ya que ya no necesita volver a analizar repetidamente una consulta.

## Uso de instrucciones preparadas

Cuando se utilizan instrucciones preparadas, se admiten las siguientes sintaxis:

- [PREPARAR](#prepare)
- [EJECUTAR](#execute)
- [DESASIGNAR](#deallocate)

### Preparar una instrucción preparada {#prepare}

Esta consulta SQL guarda la consulta SELECT escrita con el nombre dado como `PLAN_NAME`. Puede usar variables, como `$1` en lugar de valores reales. Esta instrucción preparada se guardará durante la sesión actual. Tenga en cuenta que los nombres de plan **no** distinguen entre mayúsculas y minúsculas.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### SQL de ejemplo

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Ejecutar una instrucción preparada {#execute}

Esta consulta SQL utiliza la instrucción preparada que se creó anteriormente.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### SQL de ejemplo

```sql
EXECUTE test('canada', 'vancouver');
```

### Anular la asignación de una instrucción preparada {#deallocate}

Esta consulta SQL se utiliza para eliminar la instrucción preparada con nombre.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### SQL de ejemplo

```sql
DEALLOCATE test;
```

## Flujo de ejemplo con instrucciones preparadas

Inicialmente, puede tener una consulta SQL, como la siguiente:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

La consulta SQL anterior devolverá la siguiente respuesta:

| Identificación | firstname | apellido | fecha de nacimiento | email | ciudad | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alejandro | Davis | 15-09-1993 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 14-03-1967 | example2@example.com | París | Francia |
| 10002 | kyoko | sakura | 26-11-1999 | example3@example.com | Tokio | Japón |
| 10003 | lino | pettersson | 03-06-1982 | example4@example.com | Estocolmo | Suecia |
| 10004 | aasir | waithaka | 17-12-1976 | example5@example.com | Nairobi | Kenia |
| 10005 | Fernando | ríos | 30-07-2002 | example6@example.com | Santiago | Chile |

Esta consulta SQL se puede parametrizar mediante la siguiente instrucción preparada:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Ahora, la instrucción preparada se puede ejecutar utilizando la llamada siguiente:

```sql
EXECUTE getIdRange(10000, 10005);
```

Cuando se realice esta llamada, verá exactamente los mismos resultados que antes:

| Identificación | firstname | apellido | fecha de nacimiento | email | ciudad | país |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alejandro | Davis | 15-09-1993 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 14-03-1967 | example2@example.com | París | Francia |
| 10002 | kyoko | sakura | 26-11-1999 | example3@example.com | Tokio | Japón |
| 10003 | lino | pettersson | 03-06-1982 | example4@example.com | Estocolmo | Suecia |
| 10004 | aasir | waithaka | 17-12-1976 | example5@example.com | Nairobi | Kenia |
| 10005 | Fernando | ríos | 30-07-2002 | example6@example.com | Santiago | Chile |

Una vez que haya terminado de utilizar la instrucción preparada, puede desasignarla mediante la llamada siguiente:

```sql
DEALLOCATE getIdRange;
```
