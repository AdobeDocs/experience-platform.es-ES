---
solution: Experience Platform
title: Funciones de comparación de PQL
description: Las funciones de comparación se utilizan para comparar entre diferentes expresiones y valores, devolviendo "true" o "false" en consecuencia.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 7%

---

# Funciones de comparación

Las funciones de comparación se usan para comparar entre diferentes expresiones y valores, devolviendo `true` o `false` según corresponda. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Es igual a

La función `=` (igual) comprueba si un valor o expresión es igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Ejemplo**

La siguiente consulta de PQL comprueba si el país de la dirección postal está en Canadá.

```sql
homeAddress.countryISO = "CA"
```

## Distinto a

La función `!=` (no es igual) comprueba si un valor o expresión es **no** igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Ejemplo**

La siguiente consulta de PQL comprueba si el país de la dirección postal no es Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Mayor que

La función `>` (mayor que) se usa para comprobar si el primer valor es mayor que el segundo valor.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyo cumpleaños no se celebra en enero o febrero.

```sql
person.birthMonth > 2
```

## Mayor o igual que

La función `>=` (mayor o igual que) se usa para comprobar si el primer valor es mayor o igual que el segundo valor.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyo cumpleaños no se celebra en enero o febrero.

```sql
person.birthMonth >= 3
```

## Menor que

La función de comparación `<` (menor que) se usa para comprobar si el primer valor es menor que el segundo valor.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyo cumpleaños es en enero.

```sql
person.birthMonth < 2
```

## Menor o igual que

La función de comparación `<=` (menor o igual que) se usa para comprobar si el primer valor es menor o igual que el segundo valor.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyo cumpleaños es en enero o febrero.

```sql
person.birthMonth <= 2
```

## Pasos siguientes

Ahora que ha aprendido a usar las funciones de comparación, puede usarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
