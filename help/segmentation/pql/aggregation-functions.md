---
solution: Experience Platform
title: Funciones de agregación de PQL
description: Las funciones de agregación se utilizan para agrupar varios valores dentro de matrices de Profile Query Language (PQL) para formar un único valor de resumen.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# Funciones de agregación

Las funciones de agregación se utilizan para agrupar varios valores en matrices de [!DNL Profile Query Language] (PQL) para formar un único valor de resumen. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Cuenta

La función `count` devuelve el número de elementos dentro de la matriz determinada en forma de número.

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

La función `sum` devuelve la suma de todos los valores seleccionados dentro de la matriz como un número.

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

La función `average` devuelve la media aritmética de todos los valores seleccionados dentro de la matriz como un número.

**Formato**

```sql
{ARRAY}.average()
```

**Ejemplo**

La siguiente consulta de PQL devuelve el precio promedio de todos los pedidos.

```sql
orders.average(order.price)
```

## Mínimo

La función `min` devuelve como número el menor de todos los valores seleccionados dentro de la matriz.

**Formato**

```sql
{ARRAY}.min()
```

**Ejemplo**

La siguiente consulta de PQL devuelve el precio más bajo de todos los pedidos.

```sql
orders.min(order.price)
```

## Máximo

La función `max` devuelve como número el mayor de todos los valores seleccionados dentro de la matriz.

**Formato**

```sql
{ARRAY}.max()
```

**Ejemplo**

La siguiente consulta de PQL devuelve el precio más alto de todos los pedidos.

```sql
orders.max(order.price)
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de agregación, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
