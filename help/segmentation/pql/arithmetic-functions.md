---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones aritméticas;aritmética;
solution: Experience Platform
title: Funciones aritméticas PAL
topic-legacy: developer guide
description: Las funciones aritméticas se utilizan para realizar cálculos básicos de los valores en el lenguaje de consulta de perfil (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# Funciones aritméticas

Las funciones aritméticas se utilizan para realizar cálculos básicos de los valores de [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

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

La función `*` (multiplicación) se utiliza para encontrar el producto de dos expresiones de argumento.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL encuentra el producto del inventario y el precio de un producto para encontrar el valor bruto del producto.

```sql
product.inventory * product.price
```

## Sustraer

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

La siguiente consulta PQL encuentra el cociente entre el total de productos vendidos y el total de dinero ganado para ver el coste promedio por artículo.

```sql
totalProduct.price / totalProduct.sold
```

## Remainte

La función `%` (módulo/resto) se utiliza para encontrar el resto después de dividir las dos expresiones de argumento.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL comprueba si la edad de la persona es divisible entre cinco.

```sql
person.age % 5 = 0
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones aritméticas, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
