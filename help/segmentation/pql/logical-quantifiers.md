---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;cuantificadores lógicos;cuantificador lógico;
solution: Experience Platform
title: Cuantificadores lógicos de PQL
topic: developer guide
description: Los cuantificadores lógicos pueden utilizarse para afirmar condiciones con matrices en lenguaje de Consulta de Perfil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 5%

---


# Funciones de cuantificador lógico

Los cuantificadores lógicos pueden utilizarse para afirmar condiciones con matrices en [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Existe

La función `exists` determina la existencia de un elemento en una matriz, siempre que cumpla la condición proporcionada.

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

La función `forall` determina todos los elementos de una matriz que cumplen todas las condiciones especificadas.

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

Ahora que ha aprendido sobre los cuantificadores lógicos, puede utilizarlos dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
