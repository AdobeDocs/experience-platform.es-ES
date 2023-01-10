---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones de matriz;matriz;matriz
solution: Experience Platform
title: Matriz, lista y definir funciones PQL
description: El lenguaje de consulta de perfil (PQL) ofrece funciones para facilitar la interacción con matrices, listas y cadenas.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# Funciones de matriz, lista y conjunto

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con matrices, listas y cadenas. Puede encontrar más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] información general](./overview.md).

## En

La variable `in` para determinar si un elemento es miembro de una matriz o lista.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Ejemplo**

La siguiente consulta PQL define las personas con cumpleaños en marzo, junio o septiembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Not in

La variable `notIn` para determinar si un elemento no es miembro de una matriz o lista.

>[!NOTE]
>
>La variable `notIn` function *also* garantiza que ninguno de los dos valores sea igual a nulo. Por lo tanto, los resultados no son una negación exacta del `in` función.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Ejemplo**

La siguiente consulta PQL define las personas con cumpleaños que no están en marzo, junio o septiembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersecciones

La variable `intersects` se utiliza para determinar si dos matrices o listas tienen al menos un miembro común.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyos colores favoritos incluyen al menos uno de rojo, azul o verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersección

La variable `intersection` se utiliza para determinar los miembros comunes de dos matrices o listas.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Ejemplo**

La siguiente consulta PQL define si la persona 1 y la persona 2 tienen los colores favoritos de rojo, azul y verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subconjunto de

La variable `subsetOf` para determinar si una matriz específica (matriz A) es un subconjunto de otra matriz (matriz B). En otras palabras, que todos los elementos de la matriz A son elementos de la matriz B.

**Formato**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Ejemplo**

La siguiente consulta PQL define las personas que han visitado todas sus ciudades favoritas.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superconjunto de

La variable `supersetOf` para determinar si una matriz específica (matriz A) es un superconjunto de otra matriz (matriz B). En otras palabras, la matriz A contiene todos los elementos de la matriz B.

**Formato**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Ejemplo**

La siguiente consulta PQL define a las personas que han comido sushi y pizza al menos una vez.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Incluye

La variable `includes` para determinar si una matriz o lista contiene un elemento determinado.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Ejemplo**

La siguiente consulta PQL define las personas cuyo color favorito incluye el rojo.

```sql
person.favoriteColors.includes("red")
```

## Distinct

La variable `distinct` se utiliza para eliminar valores duplicados de una matriz o lista.

**Formato**

```sql
{ARRAY}.distinct()
```

**Ejemplo**

La siguiente consulta PQL especifica las personas que han realizado pedidos en más de un almacén.

```sql
person.orders.storeId.distinct().count() > 1
```

## Agrupar por

La variable `groupBy` se utiliza para particionar los valores de una matriz o lista en un grupo en función del valor de la expresión.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | La matriz o lista que se va a agrupar. |
| `{EXPRESSION}` | Expresión que asigna cada elemento de la matriz o lista devuelta. |

**Ejemplo**

La siguiente consulta PQL agrupa todos los pedidos en los que se ha colocado el pedido.

```sql
orders.groupBy(storeId)
```

## Filtro

La variable `filter` se utiliza para filtrar una matriz o lista basada en una expresión.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | La matriz o lista que se va a filtrar. |
| `{EXPRESSION}` | Expresión por la que filtrar. |

**Ejemplo**

La siguiente consulta PQL define todas las personas mayores de 21 años.

```sql
person.filter(age >= 21)
```

## Mapa

La variable `map` se utiliza para crear una nueva matriz aplicando una expresión a cada elemento de una matriz determinada.

**Formato**

```sql
array.map(expression)
```

**Ejemplo**

La siguiente consulta PQL crea una nueva matriz de números y cuadrados el valor de los números originales.

```sql
numbers.map(square)
```

## First `n` en matriz {#first-n}

La variable `topN` se utiliza para devolver la primera función `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | Matriz o lista que se va a ordenar. |
| `{VALUE}` | La propiedad en la que se va a ordenar la matriz o la lista. |
| `{AMOUNT}` | Número de elementos que se van a devolver. |

**Ejemplo**

La siguiente consulta PQL devuelve los cinco pedidos principales con el precio más alto.

```sql
orders.topN(price, 5)
```

## Última `n` en matriz

La variable `bottomN` se utiliza para devolver el último `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argumento | Descripción |
| --------- | ----------- | 
| `{ARRAY}` | Matriz o lista que se va a ordenar. |
| `{VALUE}` | La propiedad en la que se va a ordenar la matriz o la lista. |
| `{AMOUNT}` | Número de elementos que se van a devolver. |

**Ejemplo**

La siguiente consulta PQL devuelve los cinco pedidos principales con el precio más bajo.

```sql
orders.bottomN(price, 5)
```

## Primer elemento

La variable `head` se utiliza para devolver el primer elemento de la matriz o lista.

**Formato**

```sql
{ARRAY}.head()
```

**Ejemplo**

La siguiente consulta PQL devuelve el primero de los cinco pedidos principales con el precio más alto. Más información sobre `topN` se puede encontrar en la variable [first `n` en matriz](#first-n) para obtener más información.

```sql
orders.topN(price, 5).head()
```

## Pasos siguientes

Ahora que ha aprendido sobre la matriz, la lista y las funciones definidas, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [Información general sobre el lenguaje de consulta de perfil](./overview.md).
