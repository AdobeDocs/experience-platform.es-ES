---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones booleanas
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 6%

---


# Funciones booleanas

Las funciones booleanas se utilizan para realizar lógica booleana en diferentes elementos en [!DNL Profile Query Language] (PQL).  Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Y

La `and` función se utiliza para crear una conjunción lógica.

**Format**

```sql
{QUERY} and {QUERY}
```

**Ejemplo**

La siguiente consulta de PQL devolverá a todas las personas con el país de origen como Canadá y el año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## O

La `or` función se utiliza para crear una disyunción lógica.

**Format**

```sql
{QUERY} or {QUERY}
```

**Ejemplo**

La siguiente consulta de PQL devolverá a todas las personas con el país de origen como Canadá o el año de nacimiento de 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## No

La `not` (o `!`) función se utiliza para crear una negación lógica.

**Format**

```sql
not ({QUERY})
!({QUERY})
```

**Ejemplo**

La siguiente consulta de PQL devolverá a todas las personas que no tengan su país de origen como Canadá.

```sql
not (homeAddress.countryISO = "CA")
```

## Si

La `if` función se utiliza para resolver una expresión en función de si una condición especificada es verdadera.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | La expresión booleana que se está probando. |
| `{TRUE_EXPRESSION}` | La expresión cuyo valor se utilizará si `{TEST_EXPRESSION}` es true. |
| `{FALSE_EXPRESSION}` | La expresión cuyo valor se utilizará si `{TEST_EXPRESSION}` es false. |

**Ejemplo**

La siguiente consulta de PQL establecerá el valor como `1` si el país de origen fuera Canadá y `2` si el país de origen no fuera Canadá.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones booleanas, puede usarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
