---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de agregación
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Funciones de agregación

Las funciones de agregación se utilizan para agrupar varios valores en matrices de lenguaje de Consulta de Perfil (PQL) para formar un único valor de resumen. Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Recuento

La `count` función devuelve el número de elementos dentro de la matriz dada.

**Formato**

```sql
{ARRAY}.count()
```

**Ejemplo**

La siguiente consulta de PQL devuelve el número de pedidos de la matriz.

```sql
orders.count()
```

## Sum

La `sum` función devuelve la suma de todos los valores seleccionados dentro de la matriz.

**Formato**

```sql
{ARRAY}.sum()
```

**Ejemplo**

La siguiente consulta PQL devuelve la suma de todos los precios de los pedidos.

```sql
orders.sum(order.price)
```

## Average

La `average` función devuelve la media aritmética de todos los valores seleccionados dentro de la matriz.

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

La `min` función devuelve el menor de todos los valores seleccionados dentro de la matriz.

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

La `max` función devuelve el mayor de todos los valores seleccionados dentro de la matriz.

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

Ahora que ha aprendido sobre las funciones de agregación, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
