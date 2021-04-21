---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones de matriz;matriz;matriz
solution: Experience Platform
title: Matriz, lista y definir funciones PQL
topic-legacy: developer guide
description: El lenguaje de consulta de perfil (PQL) ofrece funciones para facilitar la interacción con matrices, listas y cadenas.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# Funciones de matriz, lista y conjunto

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con matrices, listas y cadenas. Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## En

La función `in` se utiliza para determinar si un elemento es miembro de una matriz o lista.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Ejemplo**

La siguiente consulta PQL define las personas con cumpleaños en marzo, junio o septiembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Not in

La función `notIn` se utiliza para determinar si un elemento no es miembro de una matriz o lista.

>[!NOTE]
>
>La función `notIn` *también* garantiza que ninguno de los valores sea igual a nulo. Por lo tanto, los resultados no son una negación exacta de la función `in`.

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

La función `intersects` se utiliza para determinar si dos matrices o listas tienen al menos un miembro común.

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

La función `intersection` se utiliza para determinar los miembros comunes de dos matrices o listas.

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

La función `subsetOf` se utiliza para determinar si una matriz específica (matriz A) es un subconjunto de otra matriz (matriz B). En otras palabras, que todos los elementos de la matriz A son elementos de la matriz B.

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

La función `supersetOf` se utiliza para determinar si una matriz específica (matriz A) es un superconjunto de otra matriz (matriz B). En otras palabras, la matriz A contiene todos los elementos de la matriz B.

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

La función `includes` se utiliza para determinar si una matriz o lista contiene un elemento determinado.

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

La función `distinct` se utiliza para eliminar valores duplicados de una matriz o lista.

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

La función `groupBy` se utiliza para particionar los valores de una matriz o lista en un grupo en función del valor de la expresión.

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

La función `filter` se utiliza para filtrar una matriz o lista basada en una expresión.

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

La función `map` se utiliza para crear una nueva matriz aplicando una expresión a cada elemento de una matriz determinada.

**Formato**

```sql
array.map(expression)
```

**Ejemplo**

La siguiente consulta PQL crea una nueva matriz de números y cuadrados el valor de los números originales.

```sql
numbers.map(square)
```

## Primera `n` en la matriz {#first-n}

La función `topN` se utiliza para devolver los primeros `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

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

## Última `n` en la matriz

La función `bottomN` se utiliza para devolver los últimos `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

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

La función `head` se utiliza para devolver el primer elemento de la matriz o lista.

**Formato**

```sql
{ARRAY}.head()
```

**Ejemplo**

La siguiente consulta PQL devuelve el primero de los cinco pedidos principales con el precio más alto. Puede encontrar más información sobre la función `topN` en la sección [first `n` en array](#first-n).

```sql
orders.topN(price, 5).head()
```

## Pasos siguientes

Ahora que ha aprendido sobre la matriz, la lista y las funciones definidas, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
