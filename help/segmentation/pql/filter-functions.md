---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Idioma de consulta de perfil;funciones de filtro;filtro;
solution: Experience Platform
title: Funciones de filtro PQL
topic-legacy: developer guide
description: Las funciones de filtro se utilizan para filtrar datos dentro de matrices en el lenguaje de consulta de perfil (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# Filtrar funciones

Las funciones de filtro se utilizan para filtrar datos dentro de matrices en [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Filtro

La función `[]` (filtro) permite aplicar filtros a una matriz y devolver un subconjunto de la matriz que coincida con la condición especificada.

**Format**

```sql
{ARRAY}[filter]
```

**Ejemplo**

La siguiente consulta PQL obtiene todos los eventos que tienen al menos un artículo de producto con un SKU igual a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operador Up

El operador `^` (arriba) permite hacer referencia a propiedades en niveles superiores de filtros.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argumento | Descripción |
| -------- | ----------- |
| `{ARRAY}` | La matriz que se está filtrando. |
| `{FILTER_1}` | La capa exterior del filtro. |
| `{FILTER_2}` | La capa interior del filtrado |
| `^{PROPERTY}` | La propiedad en la que también se está filtrando. Debido a `^`, está comprobando una propiedad basada en filter1. |

**Ejemplo**

La siguiente consulta PQL obtiene todos los eventos que tienen al menos un elemento de producto con un SKU igual a &quot;PS&quot; **o** tienen una persona cuyo sexo es femenino.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de filtro, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
