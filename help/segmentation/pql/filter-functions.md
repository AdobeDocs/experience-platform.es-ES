---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de filtro
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Funciones de filtro

Las funciones de filtro se utilizan para filtrar datos dentro de matrices en el lenguaje de Consulta de Perfil (PQL). Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Filtro

La función `[]` (filter) permite aplicar filtros a una matriz y devolver un subconjunto de la matriz que coincida con la condición especificada.

**Formato**

```sql
{ARRAY}[filter]
```

**Ejemplo**

La siguiente consulta de PQL obtiene todos los eventos que tienen al menos un elemento de producto con un SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador de arriba

El operador `^` (arriba) permite hacer referencia a las propiedades de los niveles superiores de filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descripción |
| -------- | ----------- |
| `{ARRAY}` | Matriz que se está filtrando. |
| `{FILTER_1}` | La capa exterior del filtro. |
| `{FILTER_2}` | La capa interior del filtro |
| `^{PROPERTY}` | Propiedad en la que también se está filtrando. Debido al `^`, está comprobando una propiedad basada en filter1. |

**Ejemplo**

La siguiente consulta de PQL obtiene todos los eventos que tienen al menos un elemento de producto con una SKU igual a &quot;PS&quot; **o que** tienen una persona de sexo femenino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de filtro, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
