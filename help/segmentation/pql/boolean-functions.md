---
solution: Experience Platform
title: Funciones booleanas de PQL
description: Las funciones booleanas se utilizan para realizar lógica booleana en diferentes elementos de Profile Query Language (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 4%

---

# Funciones booleanas

Las funciones booleanas se utilizan para realizar lógica booleana en diferentes elementos de [!DNL Profile Query Language] (PQL).  Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Y

La función `and` se usa para crear una conjunción lógica como booleano.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Ejemplo**

La siguiente consulta de PQL devolverá todas las personas con país de origen como Canadá y año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## O

La función `or` se usa para crear una disyunción lógica como booleano.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Ejemplo**

La siguiente consulta de PQL devolverá todas las personas con país de origen como Canadá o el año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## No

La función `not` (o `!`) se usa para crear una negación lógica.

**Formato**

```sql
not ({QUERY})
!({QUERY})
```

**Ejemplo**

La siguiente consulta de PQL devolverá todas las personas que no tengan su país de origen como Canadá.

```sql
not (homeAddress.countryISO = "CA")
```

## Si

La función `if` se usa para resolver una expresión en función de si una condición especificada es verdadera como valor booleano.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | La expresión booleana que se está probando. |
| `{TRUE_EXPRESSION}` | La expresión cuyo valor se usará si `{TEST_EXPRESSION}` es verdadero. |
| `{FALSE_EXPRESSION}` | La expresión cuyo valor se usará si `{TEST_EXPRESSION}` es falso. |

**Ejemplo**

La siguiente consulta de PQL establecerá el valor como `1` si el país de origen es Canadá y `2` si el país de origen no es Canadá.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones booleanas, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
