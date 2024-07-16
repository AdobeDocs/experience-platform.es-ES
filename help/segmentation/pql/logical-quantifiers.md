---
solution: Experience Platform
title: Cuantificadores lógicos de PQL
description: Los cuantificadores lógicos se pueden utilizar para afirmar condiciones con matrices en Profile Query Language (PQL).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 3%

---

# Funciones de cuantificador lógico

Los cuantificadores lógicos se pueden usar para afirmar condiciones con matrices en [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Existe

La función `exists` determina la existencia de un elemento en una matriz, siempre que cumpla la condición proporcionada.

**Formato**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descripción |
| ---------- | ----------- |
| `{VARIABLE}` | Nombre de una variable. |
| `{EXPRESSION}` | La matriz que se está comprobando. |
| `{CONDITION}` | Una expresión opcional que filtra los valores de la matriz devuelta. |

**Ejemplo**

La siguiente consulta de PQL obtiene todos los eventos que tienen un precio mayor que 50 $ o que tienen un SKU de &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Para todos

La función `forall` determina todos los elementos de una matriz que cumplen todas las condiciones dadas.

**Formato**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descripción |
| ---------- | ----------- |
| `{VARIABLE}` | Nombre de una variable. |
| `{EXPRESSION}` | La matriz que se está comprobando. |
| `{CONDITION}` | Una expresión opcional que filtra los valores de la matriz devuelta. |

**Ejemplo**

La siguiente consulta de PQL obtiene todos los eventos con un precio superior a 50 $ y un SKU de &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Pasos siguientes

Ahora que ha aprendido a usar cuantificadores lógicos, puede usarlos en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
