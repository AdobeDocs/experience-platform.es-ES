---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;aggregation functions;aggregation;
solution: Experience Platform
title: Funciones de agregación
topic: developer guide
description: 'Las funciones de agregación se utilizan para agrupar varios valores en matrices de lenguaje de Consulta de Perfil (PQL) para formar un único valor de resumen. '
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 7%

---


# Funciones de agregación

Las funciones de agregación se utilizan para agrupar varios valores dentro de matrices [!DNL Profile Query Language] (PQL) para formar un único valor de resumen. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Recuento

La `count` función devuelve el número de elementos dentro de la matriz dada.

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

La `sum` función devuelve la suma de todos los valores seleccionados dentro de la matriz.

**Format**

```sql
{ARRAY}.sum()
```

**Ejemplo**

La siguiente consulta PQL devuelve la suma de todos los precios de los pedidos.

```sql
orders.sum(order.price)
```

## Promedio

La `average` función devuelve la media aritmética de todos los valores seleccionados dentro de la matriz.

**Format**

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

**Format**

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

**Format**

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
