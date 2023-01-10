---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;instrucciones preparadas;preparado;sql;
solution: Experience Platform
title: Instrucciones preparadas en el servicio de consultas
description: En SQL, las instrucciones preparadas se utilizan para crear plantillas de consultas o actualizaciones similares. El servicio de consulta de Adobe Experience Platform admite instrucciones preparadas mediante una consulta parametrizada.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 11%

---

# Declaraciones preparadas

En SQL, las instrucciones preparadas se utilizan para crear plantillas de consultas o actualizaciones similares. Adobe Experience Platform [!DNL Query Service] admite instrucciones preparadas mediante una consulta parametrizada. Esto puede optimizar el rendimiento, ya que ya no es necesario volver a analizar una consulta de forma repetida.

## Uso de instrucciones preparadas

Cuando se utilizan instrucciones preparadas, se admiten las siguientes sintaxis:

- [PREPARAR](#prepare)
- [EJECUTAR](#execute)
- [DESASIGNAR](#deallocate)

### Preparar una declaración preparada {#prepare}

Esta consulta SQL guarda la consulta SELECT escrita con el nombre dado como `PLAN_NAME`. Puede utilizar variables como `$1` en lugar de valores reales. Esta declaración preparada se guardará durante la sesión actual. Tenga en cuenta que los nombres de plan son **not** distingue entre mayúsculas y minúsculas.

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

### Desasignar una declaración preparada {#deallocate}

Esta consulta SQL se utiliza para eliminar la instrucción preparada con nombre.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### SQL de muestra

```sql
DEALLOCATE test;
```

## Flujo de ejemplo utilizando instrucciones preparadas

Inicialmente, puede tener una consulta SQL, como la que se muestra a continuación:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

La consulta SQL anterior devolverá la siguiente respuesta:

| id | firstname | lastname | cumpleaños | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10 000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | París | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokio | Japón |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Estocolmo | Suecia |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Esta consulta SQL se puede parametrizar utilizando la siguiente instrucción preparada:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Ahora, la instrucción preparada se puede ejecutar utilizando la siguiente llamada:

```sql
EXECUTE getIdRange(10000, 10005);
```

Cuando se llame a esto, verá exactamente los mismos resultados que antes:

| id | firstname | lastname | cumpleaños | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10 000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canadá |
| 10001 | antoína | dubois | 1967-03-14 | example2@example.com | París | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokio | Japón |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Estocolmo | Suecia |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Una vez que haya terminado de usar la instrucción preparada, puede desasignarla usando la siguiente llamada:

```sql
DEALLOCATE getIdRange;
```
