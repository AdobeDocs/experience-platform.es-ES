---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones de filtro;filtro;
solution: Experience Platform
title: Funciones de filtro PQL
topic: developer guide
description: Las funciones de filtro se utilizan para filtrar datos dentro de matrices en el lenguaje de Consulta de Perfil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---


# Funciones de filtro

Las funciones de filtro se utilizan para filtrar datos dentro de matrices en [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

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

El operador `^` (arriba) permite hacer referencia a las propiedades en los niveles superiores de filtros.

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

La siguiente consulta de PQL obtiene todos los eventos que tienen al menos un elemento de producto con un SKU igual a &quot;PS&quot; **o** tienen una persona cuyo sexo es femenino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de filtro, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
