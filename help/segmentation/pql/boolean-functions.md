---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Idioma de consulta de perfil;funciones booleanas;booleano;
solution: Experience Platform
title: Funciones booleanas de PQL
topic-legacy: developer guide
description: Las funciones booleanas se utilizan para realizar lógica booleana en diferentes elementos del lenguaje de consulta de perfil (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# Funciones booleanas

Las funciones booleanas se utilizan para realizar lógica booleana en diferentes elementos en [!DNL Profile Query Language] (PQL).  Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Y

La función `and` se utiliza para crear una conjunción lógica.

**Format**

```sql
{QUERY} and {QUERY}
```

**Ejemplo**

La siguiente consulta PQL devolverá todas las personas con el país de origen como Canadá y el año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## O

La función `or` se utiliza para crear una disyunción lógica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Ejemplo**

La siguiente consulta PQL devolverá a todas las personas con el país de origen como Canadá o año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## No

La función `not` (o `!`) se utiliza para crear una negación lógica.

**Formato**

```sql
not ({QUERY})
!({QUERY})
```

**Ejemplo**

La siguiente consulta PQL devolverá a todas las personas que no tengan su país de origen como Canadá.

```sql
not (homeAddress.countryISO = "CA")
```

## Si

La función `if` se utiliza para resolver una expresión en función de si una condición especificada es verdadera.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | La expresión booleana que se está probando. |
| `{TRUE_EXPRESSION}` | La expresión cuyo valor se utilizará si `{TEST_EXPRESSION}` es verdadera. |
| `{FALSE_EXPRESSION}` | La expresión cuyo valor se utilizará si `{TEST_EXPRESSION}` es false. |

**Ejemplo**

La siguiente consulta PQL establecerá el valor como `1` si el país de origen es Canadá y `2` si el país de origen no es Canadá.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones booleanas, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
