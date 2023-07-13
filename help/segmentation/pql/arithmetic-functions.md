---
solution: Experience Platform
title: Funciones aritméticas PAL
description: Las funciones aritméticas se utilizan para realizar cálculos básicos sobre los valores en el lenguaje de consulta de perfil (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 6%

---

# Funciones aritméticas

Las funciones aritméticas se utilizan para realizar cálculos básicos sobre los valores de [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Add

El `+` (suma) se utiliza para encontrar la suma de dos expresiones de argumento.

**Formato**

```sql
{NUMBER} + {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL suma el precio de dos productos diferentes.

```sql
product1.price + product2.price
```

## Multiplicar

El `*` (multiplicación) se utiliza para encontrar el producto de dos expresiones de argumento.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL encuentra el producto del inventario y el precio de un producto para encontrar el valor bruto del producto.

```sql
product.inventory * product.price
```

## Restar

El `-` (resta) se utiliza para encontrar la diferencia de dos expresiones de argumento.

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

El `/` (división) se utiliza para encontrar el cociente de dos expresiones de argumento.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Ejemplo**

La siguiente consulta PQL encuentra el cociente entre el total de productos vendidos y el total de dinero ganado para ver el coste promedio por artículo.

```sql
totalProduct.price / totalProduct.sold
```

## Resto

El `%` (módulo/resto) se utiliza para encontrar el resto después de dividir las dos expresiones de argumento.

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

Ahora que ha aprendido acerca de las funciones aritméticas, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
