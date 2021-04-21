---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones de agregación;agregación;
solution: Experience Platform
title: Funciones de agregación de PQL
topic-legacy: developer guide
description: Las funciones de agregación se utilizan para agrupar varios valores dentro de matrices de lenguajes de consulta de perfil (PQL) para formar un único valor de resumen.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---

# Funciones de agregación

Las funciones de agregación se utilizan para agrupar varios valores dentro de matrices [!DNL Profile Query Language] (PQL) para formar un único valor de resumen. Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Recuento

La función `count` devuelve el número de elementos dentro de la matriz dada.

**Format**

```sql
{ARRAY}.count()
```

**Ejemplo**

La siguiente consulta PQL devuelve el número de pedidos de la matriz.

```sql
orders.count()
```

## Sum

La función `sum` devuelve la suma de todos los valores seleccionados dentro de la matriz.

**Formato**

```sql
{ARRAY}.sum()
```

**Ejemplo**

La siguiente consulta PQL devuelve la suma de todos los precios de los pedidos.

```sql
orders.sum(order.price)
```

## Promedio

La función `average` devuelve la media aritmética de todos los valores seleccionados dentro de la matriz.

**Formato**

```sql
{ARRAY}.average()
```

**Ejemplo**

La siguiente consulta PQL devuelve el precio promedio de todos los pedidos.

```sql
orders.average(order.price)
```

## Mínimo

La función `min` devuelve el menor de todos los valores seleccionados dentro de la matriz.

**Formato**

```sql
{ARRAY}.min()
```

**Ejemplo**

La siguiente consulta PQL devuelve el precio más bajo de todos los pedidos.

```sql
orders.min(order.price)
```

## Máximo

La función `max` devuelve el mayor de todos los valores seleccionados dentro de la matriz.

**Formato**

```sql
{ARRAY}.max()
```

**Ejemplo**

La siguiente consulta PQL devuelve el precio más alto de todos los pedidos.

```sql
orders.max(order.price)
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de agregación, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
