---
solution: Experience Platform
title: Funciones de matriz, lista y conjunto de PQL
description: Profile Query Language (PQL) ofrece funciones para facilitar la interacción con matrices, listas y cadenas.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 4%

---

# Funciones de matriz, lista y conjunto

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con matrices, listas y cadenas. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## En

La función `in` se usa para determinar si un elemento es miembro de una matriz o lista.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Ejemplo**

La siguiente consulta de PQL define a las personas con cumpleaños en marzo, junio o septiembre.

```sql
person.birthMonth in [3, 6, 9]
```

## No en

La función `notIn` se usa para determinar si un elemento no es miembro de una matriz o lista.

>[!NOTE]
>
>La función *also* de `notIn` garantiza que ninguno de los valores es igual a nulo. Por lo tanto, los resultados no son una negación exacta de la función `in`.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Ejemplo**

La siguiente consulta de PQL define a las personas con cumpleaños que no se celebran en marzo, junio o septiembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Interseca

La función `intersects` se usa para determinar si dos matrices o listas tienen al menos un miembro común.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Ejemplo**

La siguiente consulta de PQL define a las personas cuyos colores favoritos incluyen al menos uno de rojo, azul o verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersección

La función `intersection` se usa para determinar los miembros comunes de dos matrices o listas.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Ejemplo**

La siguiente consulta de PQL define si la persona 1 y la persona 2 tienen ambos colores favoritos de rojo, azul y verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subconjunto de

La función `subsetOf` se usa para determinar si una matriz específica (matriz A) es un subconjunto de otra matriz (matriz B). En otras palabras, que todos los elementos de la matriz A son elementos de la matriz B.

**Formato**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Ejemplo**

La siguiente consulta de PQL define a las personas que han visitado todas sus ciudades favoritas.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superconjunto de

La función `supersetOf` se usa para determinar si una matriz específica (matriz A) es un superconjunto de otra matriz (matriz B). En otras palabras, esa matriz A contiene todos los elementos de la matriz B.

**Formato**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Ejemplo**

La siguiente consulta de PQL define a las personas que han comido sushi y pizza al menos una vez.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Incluye

La función `includes` se usa para determinar si una matriz o lista contiene un elemento determinado.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Ejemplo**

La siguiente consulta de PQL define a las personas cuyo color favorito incluye el rojo.

```sql
person.favoriteColors.includes("red")
```

## Distinto

La función `distinct` se usa para quitar valores duplicados de una matriz o lista.

**Formato**

```sql
{ARRAY}.distinct()
```

**Ejemplo**

La siguiente consulta de PQL especifica las personas que han realizado pedidos en más de un almacén.

```sql
person.orders.storeId.distinct().count() > 1
```

## Agrupar por

La función `groupBy` se usa para dividir los valores de una matriz o lista en un grupo en función del valor de la expresión.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | La matriz o lista que se va a agrupar. |
| `{EXPRESSION}` | Expresión que asigna cada elemento de la matriz o lista devuelta. |

**Ejemplo**

La siguiente consulta de PQL agrupa todos los pedidos en los que se almacena el pedido.

```sql
orders.groupBy(storeId)
```

## Filtro

La función `filter` se usa para filtrar una matriz o lista basada en una expresión.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | La matriz o lista que se va a filtrar. |
| `{EXPRESSION}` | Una expresión por la que filtrar. |

**Ejemplo**

La siguiente consulta de PQL define todas las personas de 21 años o más.

```sql
person.filter(age >= 21)
```

## Mapa

La función `map` se usa para crear una nueva matriz aplicando una expresión a cada elemento de una matriz determinada.

**Formato**

```sql
array.map(expression)
```

**Ejemplo**

La siguiente consulta PQL crea una nueva matriz de números y ajusta al cuadrado el valor de los números originales.

```sql
numbers.map(square)
```

## Primer `n` en matriz {#first-n}

La función `topN` se usa para devolver los primeros `N` elementos de una matriz, cuando se ordenan en orden ascendente en función de la expresión numérica dada.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | La matriz o lista que se va a ordenar. |
| `{VALUE}` | Propiedad en la que se ordena la matriz o lista. |
| `{AMOUNT}` | Número de elementos que se van a devolver. |

**Ejemplo**

La siguiente consulta de PQL devuelve los cinco pedidos con el precio más alto.

```sql
orders.topN(price, 5)
```

## Últimos `n` en matriz

La función `bottomN` se usa para devolver los últimos `N` elementos de una matriz, cuando se ordenan en orden ascendente en función de la expresión numérica dada.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argumento | Descripción |
| --------- | ----------- | 
| `{ARRAY}` | La matriz o lista que se va a ordenar. |
| `{VALUE}` | Propiedad en la que se ordena la matriz o lista. |
| `{AMOUNT}` | Número de elementos que se van a devolver. |

**Ejemplo**

La siguiente consulta de PQL devuelve los cinco pedidos principales con el precio más bajo.

```sql
orders.bottomN(price, 5)
```

## Primer elemento

La función `head` se usa para devolver el primer elemento de la matriz o lista.

**Formato**

```sql
{ARRAY}.head()
```

**Ejemplo**

La siguiente consulta de PQL devuelve el primero de los cinco pedidos con el precio más alto. Encontrará más información sobre la función `topN` en la sección [primeros `n` de la matriz](#first-n).

```sql
orders.topN(price, 5).head()
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de matriz, lista y conjunto, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
