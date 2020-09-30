---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: Cuantificadores lógicos
topic: developer guide
description: Los cuantificadores lógicos pueden utilizarse para afirmar condiciones con matrices en lenguaje de Consulta de Perfil (PQL).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 5%

---


# Funciones de cuantificador lógico

Los cuantificadores lógicos pueden utilizarse para afirmar condiciones con matrices en [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Existe

La `exists` función determina la existencia de un elemento en una matriz, siempre que cumpla la condición proporcionada.

**Format**

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

**Format**

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
