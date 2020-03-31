---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Cuantificadores lógicos
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Funciones de cuantificador lógico

Los cuantificadores lógicos pueden utilizarse para afirmar condiciones con matrices en lenguaje de Consulta de Perfil (PQL). Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Existe

La `exists` función determina la existencia de un elemento en una matriz, siempre que cumpla la condición proporcionada.

**Formato**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descripción |
| ---------- | ----------- |
| `{VARIABLE}` | Nombre de una variable. |
| `{EXPRESSION}` | Matriz que se está comprobando. |
| `{CONDITION}` | Una expresión opcional que filtros los valores de la matriz devueltos. |

**Ejemplo**

La siguiente consulta de PQL obtiene todos los eventos que tienen un precio bueno de 50 $ o que tienen un SKU de &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Para todos

La `forall` función determina todos los elementos de una matriz que cumplen todas las condiciones determinadas.

**Formato**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argumento | Descripción |
| ---------- | ----------- |
| `{VARIABLE}` | Nombre de una variable. |
| `{EXPRESSION}` | Matriz que se está comprobando. |
| `{CONDITION}` | Una expresión opcional que filtros los valores de la matriz devueltos. |

**Ejemplo**

La siguiente consulta PQL obtiene todos los eventos que tienen un precio bueno de 50 $ y tiene un SKU de &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Pasos siguientes

Ahora que ha aprendido sobre los cuantificadores lógicos, puede utilizarlos dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
