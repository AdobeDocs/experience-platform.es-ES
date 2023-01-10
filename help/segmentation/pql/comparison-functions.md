---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones de comparación;comparación;
solution: Experience Platform
title: Funciones de comparación de PQL
description: Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, devolviendo "true" o "false" en consecuencia.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# Funciones de comparación

Las funciones de comparación se utilizan para comparar entre diferentes expresiones y valores y para devolver `true` o `false` en consecuencia. Puede encontrar más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] información general](./overview.md).

## Es igual a

La variable `=` (es igual que) comprueba si un valor o expresión es igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Ejemplo**

La siguiente consulta PQL comprueba si el país de la dirección principal está en Canadá.

```sql
homeAddress.countryISO = "CA"
```

## Distinto a

La variable `!=` función (no igual) comprueba si hay un valor o expresión **not** igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Ejemplo**

La siguiente consulta PQL comprueba si el país de la dirección principal no está en Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

La variable `>` (bueno que) se utiliza para comprobar si el primer valor es bueno que el segundo valor.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños no cae en enero o febrero.

```sql
person.birthMonth > 2
```

## Mayor o igual que

La variable `>=` (buena o igual que) se utiliza para comprobar si el primer valor es bueno o igual al segundo valor.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños no cae en enero o febrero.

```sql
person.birthMonth >= 3
```

## Menos de

La variable `<` (menor que) para comprobar si el primer valor es menor que el segundo valor.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños es en enero.

```sql
person.birthMonth < 2
```

## Less than or equal to

La variable `<=` (menor o igual que) se utiliza la función de comparación para comprobar si el primer valor es menor o igual que el segundo valor.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños es enero o febrero.

```sql
person.birthMonth <= 2
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de comparación, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [Información general sobre el lenguaje de consulta de perfil](./overview.md).
