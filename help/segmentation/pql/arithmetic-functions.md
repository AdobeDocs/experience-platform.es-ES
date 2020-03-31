---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones aritméticas
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Funciones aritméticas

Las funciones aritméticas se utilizan para realizar cálculos básicos de valores en el lenguaje de Consulta de Perfil (PQL). Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Add

La función `+` (suma) se utiliza para encontrar la suma de dos expresiones de argumento.

**Formato**

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

La función `%` (modulo/resto) se utiliza para encontrar el resto después de dividir las dos expresiones de argumento.

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

Ahora que ha aprendido sobre las funciones aritméticas, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
