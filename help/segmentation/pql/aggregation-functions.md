---
solution: Experience Platform
title: Funciones de agregación PQL
description: Las funciones de agregación se utilizan para agrupar varios valores en matrices de Lenguaje de consulta de perfil (PQL) para formar un único valor de resumen.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 8%

---

# Funciones de agregación

Las funciones de agregación se utilizan para agrupar varios valores dentro de [!DNL Profile Query Language] (PQL) para formar un único valor de resumen. Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Count

El `count` función devuelve el número de elementos dentro de la matriz determinada.

**Formato**

```sql
{ARRAY}.count()
```

**Ejemplo**

La siguiente consulta PQL devuelve el número de pedidos de la matriz.

```sql
orders.count()
```

## Sum

El `sum` función devuelve la suma de todos los valores seleccionados dentro de la matriz.

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

El `average` función devuelve la media aritmética de todos los valores seleccionados dentro de la matriz.

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

El `min` función devuelve el menor de todos los valores seleccionados dentro de la matriz.

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

El `max` función devuelve el mayor de todos los valores seleccionados dentro de la matriz.

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

Ahora que ha aprendido acerca de las funciones de agregación, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
