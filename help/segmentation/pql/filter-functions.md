---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;filter functions;filter;
solution: Experience Platform
title: Funciones de filtro
topic: developer guide
description: Las funciones de filtro se utilizan para filtrar datos dentro de matrices en el lenguaje de Consulta de Perfil (PQL).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 4%

---


# Funciones de filtro

Las funciones de filtro se utilizan para filtrar datos dentro de matrices en [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Filtro

La función `[]` (filter) permite aplicar filtros a una matriz y devolver un subconjunto de la matriz que coincida con la condición especificada.

**Format**

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

**Format**

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
