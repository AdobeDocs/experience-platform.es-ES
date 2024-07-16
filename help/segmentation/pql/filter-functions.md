---
solution: Experience Platform
title: Funciones de filtro de PQL
description: Las funciones de filtro se utilizan para filtrar datos dentro de matrices en Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---

# Funciones de filtro

Las funciones de filtro se utilizan para filtrar datos dentro de matrices en [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Filtro

La función `[]` (filtro) permite aplicar filtros a una matriz y devolver un subconjunto de la matriz que coincida con la condición especificada.

**Formato**

```sql
{ARRAY}[filter]
```

**Ejemplo**

La siguiente consulta de PQL obtiene todos los eventos que tienen al menos un elemento de producto con un SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador Up

El operador `^` (arriba) le permite hacer referencia a las propiedades de los niveles superiores de los filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descripción |
| -------- | ----------- |
| `{ARRAY}` | Matriz que se está filtrando. |
| `{FILTER_1}` | La capa exterior del filtrado. |
| `{FILTER_2}` | La capa interna de filtrado |
| `^{PROPERTY}` | La propiedad en la que también se está filtrando. Debido a `^`, está comprobando una propiedad basada en filter1. |

**Ejemplo**

La siguiente consulta de PQL obtiene todos los eventos que tienen al menos un elemento de producto con un SKU igual a &quot;PS&quot; **o** que tiene una persona cuyo sexo es femenino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Pasos siguientes

Ahora que ha aprendido a filtrar funciones, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
