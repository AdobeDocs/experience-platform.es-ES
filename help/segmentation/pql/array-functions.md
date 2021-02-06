---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones de matriz;matriz;
solution: Experience Platform
title: Matriz, Lista y definición de funciones PQL
topic: developer guide
description: Perfil Consulta Language (PQL) oferta funciones para facilitar la interacción con matrices, listas y cadenas.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---


# Funciones de matriz, lista y conjunto

[!DNL Profile Query Language] (PQL) oferta funciones para facilitar la interacción con matrices, listas y cadenas. Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## En

La función `in` se utiliza para determinar si un elemento es miembro de una matriz o lista.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Ejemplo**

La siguiente consulta de PQL define las personas con cumpleaños en marzo, junio o septiembre.

```sql
person.birthMonth in [3, 6, 9]
```

## No está en

La función `notIn` se utiliza para determinar si un elemento no es miembro de una matriz o lista.

>[!NOTE]
>
>La función `notIn` *también* garantiza que ninguno de los valores sea igual a nulo. Por lo tanto, los resultados no son una negación exacta de la función `in`.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Ejemplo**

La siguiente consulta de PQL define las personas con cumpleaños que no están en marzo, junio o septiembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersecos

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

La función `intersection` se utiliza para determinar los miembros comunes de dos arreglos de discos o listas.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Ejemplo**

La siguiente consulta PQL define si la persona 1 y la persona 2 tienen los colores favoritos rojo, azul y verde.

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

La siguiente consulta de PQL define las personas que han visitado todas sus ciudades favoritas.

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

La función `distinct` se utiliza para quitar valores de duplicado de una matriz o lista.

**Formato**

```sql
{ARRAY}.distinct()
```

**Ejemplo**

La siguiente consulta de PQL especifica las personas que han realizado pedidos en más de una tienda.

```sql
person.orders.storeId.distinct().count() > 1
```

## Agrupar por

La función `groupBy` se utiliza para particionar los valores de una matriz o lista en un grupo según el valor de la expresión.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | Matriz o lista que se va a agrupar. |
| `{EXPRESSION}` | Expresión que asigna cada elemento de la matriz o lista devuelta. |

**Ejemplo**

La siguiente consulta PQL agrupa todos los pedidos en los que se realizó el pedido.

```sql
orders.groupBy(storeId)
```

## Filtro

La función `filter` se utiliza para filtrar una matriz o lista según una expresión.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | Matriz o lista que se va a filtrar. |
| `{EXPRESSION}` | Una expresión por la que filtrar. |

**Ejemplo**

La siguiente consulta de PQL define a todas las personas mayores de 21 años.

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

## Primero `n` en la matriz {#first-n}

La función `topN` se utiliza para devolver los primeros `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | Matriz o lista que se va a ordenar. |
| `{VALUE}` | Propiedad en la que se ordenará la matriz o la lista. |
| `{AMOUNT}` | Número de elementos que se van a devolver. |

**Ejemplo**

La siguiente consulta PQL devuelve los cinco pedidos principales con el precio más alto.

```sql
orders.topN(price, 5)
```

## Última `n` en matriz

La función `bottomN` se utiliza para devolver los últimos `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argumento | Descripción |
| --------- | ----------- | 
| `{ARRAY}` | Matriz o lista que se va a ordenar. |
| `{VALUE}` | Propiedad en la que se ordenará la matriz o la lista. |
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

La siguiente consulta PQL devuelve el primero de los cinco pedidos principales con el precio más alto. Encontrará más información sobre la función `topN` en la sección [primero `n` de la matriz](#first-n).

```sql
orders.topN(price, 5).head()
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de arreglo de discos, lista y configuración, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
