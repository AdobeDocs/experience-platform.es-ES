---
solution: Experience Platform
title: Funciones booleanas PQL
description: Las funciones booleanas se utilizan para realizar lógica booleana en diferentes elementos del lenguaje de consulta de perfil (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 6%

---

# Funciones booleanas

Las funciones booleanas se utilizan para realizar lógica booleana en diferentes elementos de [!DNL Profile Query Language] (PQL).  Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Y

El `and` se utiliza para crear una conjunción lógica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Ejemplo**

La siguiente consulta PQL devolverá todas las personas con país de origen como Canadá y año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## O

El `or` se utiliza para crear una disyunción lógica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Ejemplo**

La siguiente consulta PQL devolverá todas las personas con país de origen como Canadá o el año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## No

El `not` (o `!`) se utiliza para crear una negación lógica.

**Formato**

```sql
not ({QUERY})
!({QUERY})
```

**Ejemplo**

La siguiente consulta PQL devolverá todas las personas que no tengan su país de origen como Canadá.

```sql
not (homeAddress.countryISO = "CA")
```

## Si

El `if` se utiliza para resolver una expresión en función de si una condición especificada es verdadera.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | La expresión booleana que se está probando. |
| `{TRUE_EXPRESSION}` | La expresión cuyo valor se utilizará si `{TEST_EXPRESSION}` es verdadero. |
| `{FALSE_EXPRESSION}` | La expresión cuyo valor se utilizará si `{TEST_EXPRESSION}` es false. |

**Ejemplo**

La siguiente consulta PQL establecerá el valor como `1` si el país de origen es Canadá y `2` si el país de origen no es Canadá.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones booleanas, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
