---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de consulta de perfil;funciones de filtrado;filter;
solution: Experience Platform
title: Funciones de filtro PQL
description: Las funciones de filtro se utilizan para filtrar datos dentro de matrices en el lenguaje de consulta de perfil (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# Funciones de filtro

Las funciones de filtro se utilizan para filtrar datos dentro de matrices en [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Filtro

El `[]` La función (filter) permite aplicar filtros a una matriz y devolver un subconjunto de la matriz que coincida con la condición especificada.

**Formato**

```sql
{ARRAY}[filter]
```

**Ejemplo**

La siguiente consulta PQL obtiene todos los eventos que tienen al menos un elemento de producto con un SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador Up

El `^` El operador (up) permite hacer referencia a propiedades en niveles superiores de filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descripción |
| -------- | ----------- |
| `{ARRAY}` | Matriz que se está filtrando. |
| `{FILTER_1}` | La capa exterior del filtrado. |
| `{FILTER_2}` | La capa interna de filtrado |
| `^{PROPERTY}` | La propiedad en la que también se está filtrando. Debido a la `^`, está comprobando una propiedad basada en filter1. |

**Ejemplo**

La siguiente consulta PQL obtiene todos los eventos que tienen al menos un elemento de producto con un SKU igual a &quot;PS&quot; **o** tener una persona cuyo sexo sea femenino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de filtro, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
