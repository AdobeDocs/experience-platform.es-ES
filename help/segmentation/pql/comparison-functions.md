---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones de comparación;comparación;
solution: Experience Platform
title: Funciones de comparación de PQL
topic: developer guide
description: Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, devolviendo "true" o "false" en consecuencia.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---


# Funciones de comparación

Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, devolviendo `true` o `false` en consecuencia. Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Es igual a

La función `=` (igual a) comprueba si un valor o expresión es igual a otro valor o expresión.

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

La función `!=` (no igual) comprueba si un valor o expresión es **no** igual a otro valor o expresión.

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

La función `>=` (buena o igual a) se utiliza para comprobar si el primer valor es bueno o igual al segundo valor.

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

Ahora que ha aprendido sobre las funciones de comparación, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
