---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones de comparación;comparación;
solution: Experience Platform
title: Funciones de comparación de PQL
topic-legacy: developer guide
description: Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, devolviendo "true" o "false" en consecuencia.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# Funciones de comparación

Las funciones de comparación se utilizan para comparar diferentes expresiones y valores, devolviendo `true` o `false` según corresponda. Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Es igual a

La función `=` (es igual que) comprueba si un valor o expresión es igual a otro valor o expresión.

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Ejemplo**

La siguiente consulta PQL comprueba si el país de la dirección principal está en Canadá.

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

La siguiente consulta PQL comprueba si el país de la dirección principal no está en Canadá.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

La función `>` (buena que) se utiliza para comprobar si el primer valor es bueno que el segundo valor.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo cumpleaños no cae en enero o febrero.

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

La siguiente consulta PQL define las personas cuyo cumpleaños no cae en enero o febrero.

```sql
person.birthMonth >= 3
```

## Less than

La función de comparación `<` (menor que) se utiliza para comprobar si el primer valor es menor que el segundo valor.

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

La función de comparación `<=` (menor o igual que) se utiliza para comprobar si el primer valor es menor o igual que el segundo valor.

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

Ahora que ha aprendido sobre las funciones de comparación, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
