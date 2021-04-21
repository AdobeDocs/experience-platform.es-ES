---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;cuantificadores lógicos;cuantificador lógico;
solution: Experience Platform
title: Cuantificadores lógicos de PQL
topic-legacy: developer guide
description: Los cuantificadores lógicos se pueden utilizar para afirmar condiciones con matrices en el lenguaje de consulta de perfil (PQL).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 5%

---

# Funciones de cuantificador lógico

Los cuantificadores lógicos se pueden usar para afirmar condiciones con matrices en [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

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
| `{EXPRESSION}` | La matriz que se está comprobando. |
| `{CONDITION}` | Expresión opcional que filtra los valores de la matriz devuelta. |

**Ejemplo**

La siguiente consulta PQL obtiene todos los eventos que tienen un precio bueno superior a 50 $ o que tienen un SKU de &quot;PS&quot;.

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
| `{CONDITION}` | Expresión opcional que filtra los valores de la matriz devuelta. |

**Ejemplo**

La siguiente consulta PQL obtiene todos los eventos que tienen un precio bueno de más de 50 $ y tiene un SKU de &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Pasos siguientes

Ahora que ha aprendido sobre los cuantificadores lógicos, puede utilizarlos dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
