---
solution: Experience Platform
title: Funciones de comparación PQL
description: Las funciones de comparación se utilizan para comparar entre diferentes expresiones y valores, devolviendo "true" o "false" en consecuencia.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 10%

---

# Funciones de comparación

Las funciones de comparación se utilizan para comparar entre diferentes expresiones y valores, lo que devuelve `true` o `false` en consecuencia. Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Es igual a

El `=` La función (es igual que) comprueba si un valor o expresión es igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Ejemplo**

La siguiente consulta PQL comprueba si el país de la dirección postal está en Canadá.

```sql
homeAddress.countryISO = "CA"
```

## Distinto a

El `!=` La función (no es igual) comprueba si un valor o expresión es **no** es igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Ejemplo**

La siguiente consulta PQL comprueba si el país de la dirección postal no está en Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

El `>` (mayor que) se utiliza para comprobar si el primer valor es mayor que el segundo valor.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños no se celebra en enero o febrero.

```sql
person.birthMonth > 2
```

## Mayor o igual que

El `>=` (mayor o igual que) se utiliza para comprobar si el primer valor es mayor o igual que el segundo valor.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños no se celebra en enero o febrero.

```sql
person.birthMonth >= 3
```

## Menos de

El `<` (menor que) se utiliza la función de comparación para comprobar si el primer valor es menor que el segundo valor.

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

El `<=` (menor o igual que) se utiliza para comprobar si el primer valor es menor o igual que el segundo valor.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños es en enero o febrero.

```sql
person.birthMonth <= 2
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de comparación, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
