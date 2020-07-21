---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de matriz, lista y conjunto
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 5%

---


# Funciones de matriz, lista y conjunto

[!DNL Profile Query Language] (PQL) oferta funciones para facilitar la interacción con matrices, listas y cadenas. Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## En

La `in` función se utiliza para determinar si un elemento es miembro de una matriz o lista.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Ejemplo**

La siguiente consulta de PQL define las personas con cumpleaños en marzo, junio o septiembre.

```sql
person.birthMonth in [3, 6, 9]
```

## No está en

La `notIn` función se utiliza para determinar si un elemento no es miembro de una matriz o lista.

>[!NOTE]
>
>La `notIn` función *también* garantiza que ninguno de los dos valores sea igual a nulo. Por lo tanto, los resultados no son una negación exacta de la `in` función.

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

La `intersects` función se utiliza para determinar si dos matrices o listas tienen al menos un miembro común.

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

La `intersection` función se utiliza para determinar los miembros comunes de dos matrices o listas.

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

La `subsetOf` función se utiliza para determinar si una matriz específica (matriz A) es un subconjunto de otra matriz (matriz B). En otras palabras, que todos los elementos de la matriz A son elementos de la matriz B.

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

La `supersetOf` función se utiliza para determinar si una matriz específica (matriz A) es un superconjunto de otra matriz (matriz B). En otras palabras, la matriz A contiene todos los elementos de la matriz B.

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

La `includes` función se utiliza para determinar si una matriz o lista contiene un elemento determinado.

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

La `distinct` función se utiliza para quitar valores de duplicado de una matriz o lista.

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

La `groupBy` función se utiliza para dividir los valores de una matriz o lista en un grupo según el valor de la expresión.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argumento | Descripción |
| --------- | ----------- |
| `{ARRAY}` | Matriz o lista que se va a agrupar. |
| `{EXPRESSION}` | expresión que asigna cada elemento de la matriz o lista devuelta. |

**Ejemplo**

La siguiente consulta PQL agrupa todos los pedidos en los que se realizó el pedido.

```sql
orders.groupBy(storeId)
```

## Filtro

La `filter` función se utiliza para filtrar una matriz o lista según una expresión.

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

La `map` función se utiliza para crear una nueva matriz aplicando una expresión a cada elemento de una matriz determinada.

**Formato**

```sql
array.map(expression)
```

**Ejemplo**

La siguiente consulta PQL crea una nueva matriz de números y cuadrados el valor de los números originales.

```sql
numbers.map(square)
```

## Primero `n` en arreglo de discos

La `topN` función se utiliza para devolver los primeros `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

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

## Último `n` en matriz

La `bottomN` función se utiliza para devolver los últimos `N` elementos de una matriz, cuando se ordenan en orden ascendente según la expresión numérica dada.

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

La `head` función se utiliza para devolver el primer elemento de la matriz o lista.

**Formato**

```sql
{ARRAY}.head()
```

**Ejemplo**

La siguiente consulta PQL devuelve el primero de los cinco pedidos principales con el precio más alto. Encontrará más información sobre la `topN` función en la [primera sección `n` de la matriz](#first-n-in-array) .

```sql
orders.topN(price, 5).head()
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de arreglo de discos, lista y configuración, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
