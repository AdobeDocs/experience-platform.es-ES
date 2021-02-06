---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones de agregación;agregación;
solution: Experience Platform
title: Funciones de agregación PQL
topic: developer guide
description: 'Las funciones de agregación se utilizan para agrupar varios valores en matrices de lenguaje de Consulta de Perfil (PQL) para formar un único valor de resumen. '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---


# Funciones de agregación

Las funciones de agregación se utilizan para agrupar varios valores dentro de [!DNL Profile Query Language] arreglos de discos (PQL) para formar un único valor de resumen. Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Recuento

La función `count` devuelve el número de elementos dentro de la matriz dada.

**Format**

```sql
{ARRAY}.count()
```

**Ejemplo**

La siguiente consulta de PQL devuelve el número de pedidos de la matriz.

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

Ahora que ha aprendido sobre las funciones de agregación, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
