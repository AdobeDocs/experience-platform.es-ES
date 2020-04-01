---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de comparación
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Funciones de comparación

Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, regresando `true` o `false` en consecuencia. Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Es igual a

La función `=` (es igual a) comprueba si un valor o expresión es igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Ejemplo**

La siguiente consulta de PQL comprueba si el país de la dirección está en Canadá.

```sql
homeAddress.countryISO = "CA"
```

## Distinto a

La función `!=` (no igual) comprueba si un valor o expresión **no es** igual a otro valor o expresión.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Ejemplo**

La siguiente consulta PQL comprueba si el país de la dirección doméstica no está en Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

La función `>` (buena que) se utiliza para comprobar si el primer valor es bueno que el segundo.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyos cumpleaños no se cumplen en enero o febrero.

```sql
person.birthMonth > 2
```

## Greater than or equal to

La función `>=` (buena o igual que) se utiliza para comprobar si el primer valor es bueno o igual al segundo valor.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyos cumpleaños no se cumplen en enero o febrero.

```sql
person.birthMonth >= 3
```

## Less than

La función de comparación `<` (menor que) se utiliza para comprobar si el primer valor es menor que el segundo.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyo cumpleaños es enero.

```sql
person.birthMonth < 2
```

## Less than or equal to

La función de comparación `<=` (menor o igual que) se utiliza para comprobar si el primer valor es menor o igual que el segundo.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta de PQL define las personas cuyo cumpleaños es enero o febrero.

```sql
person.birthMonth <= 2
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de comparación, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
