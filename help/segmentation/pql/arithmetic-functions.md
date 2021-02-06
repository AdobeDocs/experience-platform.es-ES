---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones aritméticas;aritmética;
solution: Experience Platform
title: Funciones aritméticas PAL
topic: developer guide
description: Las funciones aritméticas se utilizan para realizar cálculos básicos sobre los valores en el lenguaje de Consulta de Perfil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---


# Funciones aritméticas

Las funciones aritméticas se utilizan para realizar cálculos básicos en valores en [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Add

La función `+` (suma) se utiliza para encontrar la suma de dos expresiones de argumento.

**Format**

```sql
{NUMBER} + {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL resume el precio de dos productos diferentes.

```sql
product1.price + product2.price
```

## Multiplicar

La función `*` (multiplicación) se utiliza para encontrar el producto de dos expresiones de argumentos.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL encuentra el producto del inventario y el precio de un producto para determinar el valor bruto del producto.

```sql
product.inventory * product.price
```

## Restar

La función `-` (resta) se utiliza para encontrar la diferencia de dos expresiones de argumento.

**Formato**

```sql
{NUMBER} - {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL encuentra la diferencia de precio entre dos productos diferentes.

```sql
product1.price - product2.price
```

## Dividir

La función `/` (división) se utiliza para encontrar el cociente de dos expresiones de argumento.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Ejemplo**

La siguiente consulta de PQL encuentra el cociente entre el total de productos vendidos y el total de dinero ganado para ver el costo promedio por artículo.

```sql
totalProduct.price / totalProduct.sold
```

## Resto

La función `%` (módulo/resto) se utiliza para encontrar el resto después de dividir las dos expresiones de argumentos.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Ejemplo**

La siguiente consulta de PQL comprueba si la edad de la persona es divisible por cinco.

```sql
person.age % 5 = 0
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones aritméticas, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
