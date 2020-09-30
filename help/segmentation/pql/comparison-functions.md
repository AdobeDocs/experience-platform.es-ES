---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;comparison functions;comparison;
solution: Experience Platform
title: Funciones de comparación
topic: developer guide
description: Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, devolviendo "true" o "false" en consecuencia.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 10%

---


# Funciones de comparación

Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, regresando `true` o `false` en consecuencia. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Es igual a

La función `=` (es igual a) comprueba si un valor o expresión es igual a otro valor o expresión.

**Format**

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

**Format**

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

**Format**

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

**Format**

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

**Format**

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

**Format**

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
