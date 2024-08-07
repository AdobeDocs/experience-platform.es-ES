---
title: Administrar tipos de datos de matriz y asignación con funciones de orden superior
description: Obtenga información sobre cómo administrar tipos de datos de matrices y asignaciones con funciones de orden superior en el servicio de consultas. Se proporcionan ejemplos con casos de uso comunes.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: d2bc580ba1cacdfab45bdc6356c630a63e7d0f6e
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Administrar tipos de datos de matriz y asignación con funciones de orden superior

Utilice esta guía para conocer cómo las funciones de orden superior pueden procesar tipos de datos complejos, como matrices y mapas. Estas funciones eliminan la necesidad de explotar la matriz, realizar una función y, a continuación, combinar el resultado. Las funciones de orden superior son especialmente útiles para analizar o procesar conjuntos de datos y análisis de series temporales, que a menudo incluyen estructuras anidadas complejas, matrices, mapas y casos de uso diversos.

La siguiente lista de casos de uso contiene ejemplos de funciones de manipulación de mapas y matrices de orden superior.

## Utilizar la transformación para ajustar el total del precio en n {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

El fragmento anterior aplica una función a cada elemento de la matriz y devuelve una nueva matriz de elementos transformados. Específicamente, la función `transform` toma una matriz de tipo T y convierte cada elemento del tipo T al tipo U. A continuación, devuelve una matriz de tipo U. Los tipos reales T y U dependen del uso específico de la función de transformación.

`transform(array<T>, function<T, Int, U>): array<U>`

Esta función de transformación de matriz es similar al ejemplo anterior, pero hay dos argumentos para la función. El segundo argumento de esta función también recibe el índice del elemento en la matriz, además de transformarse.

**Ejemplo**

El ejemplo de SQL siguiente muestra este caso de uso. La consulta recupera un conjunto limitado de filas de la tabla especificada, transformando la matriz `productListItems` al multiplicar el atributo `priceTotal` de cada elemento por 73. El resultado incluye las columnas `_id`, `productListItems` y `price_in_inr` transformadas. La selección se basa en un intervalo de marca de tiempo específico.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## Utilizar existe para descubrir si existe un producto con un SKU específico {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

En el fragmento anterior, la función `exists` se aplica a cada elemento de la matriz y devuelve un valor booleano. El valor booleano indica si hay uno o más elementos en la matriz que cumplen una condición especificada. En este caso, confirma si existe un producto con un SKU específico.

**Ejemplo**

En el siguiente ejemplo de SQL, la consulta recupera `productListItems` de la tabla `geometrixxx_999_xdm_pqs_1batch_10k_rows` y evalúa si existe un elemento con un SKU igual a `123679` en la matriz `productListItems`. A continuación, filtra los resultados en función de un intervalo específico de marcas de tiempo y limita los resultados finales a diez filas.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## Utilice el filtro para buscar productos donde el SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

Esta función filtra una matriz de elementos en función de una condición determinada que evalúa cada elemento como un valor booleano. A continuación, devuelve una nueva matriz que solo incluye elementos donde la condición devolvió un valor verdadero.

**Ejemplo**

La consulta siguiente selecciona la columna `productListItems`, aplica un filtro para incluir solo elementos con SKU mayor que 100000 y restringe el conjunto de resultados a filas dentro de un intervalo de marca de tiempo específico. A continuación, la matriz filtrada se alias como `_filter` en la salida.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## Utilice el acumulado para sumar los SKU de todos los elementos de la lista de productos asociados con un ID específico y duplicar el total resultante {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

Esta operación de agregado aplica un operador binario a un estado inicial y a todos los elementos de la matriz. También reduce varios valores a un solo estado. Después de esta reducción, el estado final se convierte en el resultado final mediante una función finish. La función finish toma el último estado obtenido después de aplicar el operador binario a todos los elementos de la matriz y hace algo con él para producir el resultado final.

**Ejemplo**

Este ejemplo de consulta calcula el valor de SKU máximo de la matriz `productListItems` dentro del intervalo de marca de tiempo especificado y duplica el resultado. La salida incluye la matriz `productListItems` original y la matriz `max_value` calculada.

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## Utilice zip_with para asignar un número de secuencia a todos los elementos de la lista de productos {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

Este fragmento combina los elementos de dos matrices en una única matriz nueva. La operación se realiza de forma independiente en cada elemento de la matriz y genera pares de valores. Si una matriz es más corta, se agregan valores nulos para que coincidan con la longitud de la matriz más larga. Esto sucede antes de que se aplique la función.

**Ejemplo**

La siguiente consulta utiliza la función `zip_with` para crear pares de valores a partir de dos matrices. Para ello, agrega los valores SKU de la matriz `productListItems` a una secuencia de números enteros que se generó mediante la función `Sequence`. El resultado se selecciona junto con la columna `productListItems` original y está limitado según un intervalo de marca de tiempo.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## Utilice map_from_entries para asignar un número de secuencia a cada elemento de la lista de productos y obtener el resultado final como un mapa {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

Este fragmento convierte una matriz de pares clave-valor en un mapa. Resulta útil cuando se tratan datos de pares de clave-valor que podrían beneficiarse de una estructura más organizada y eficiente.

**Ejemplo**

La siguiente consulta crea pares de valores a partir de una secuencia y la matriz productListItems, convierte estos pares en un mapa mediante map_from_entries y, a continuación, selecciona la columna productListItems original junto con la columna map_from_entries recién creada. El resultado se filtra y limita en función del intervalo de marca de tiempo especificado.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilice map_form_array para asignar números de secuencia a elementos de la lista de productos y devolver el resultado como un mapa {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

La función `map_form_arrays` crea un mapa con valores emparejados de dos matrices.

>[!IMPORTANT]
>
>No debe haber elementos nulos en las claves.

**Ejemplo**

El siguiente SQL crea un mapa donde las claves son números de secuencia generados mediante la función `Sequence` y los valores son elementos de la matriz `productListItems`. La consulta selecciona la columna `productListItems` y utiliza la función `Map_from_arrays` para crear el mapa en función de la secuencia de números generada y los elementos de la matriz. El resultado está limitado a diez filas y se filtra en función de un intervalo de marca de tiempo.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilice map_concat para concatenar dos asignaciones en como una sola asignación {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

La función `map_concat` del fragmento anterior toma varias asignaciones como argumentos y devuelve una nueva asignación que combina todos los pares clave-valor de las asignaciones de entrada. La función concatena varias asignaciones en una sola, y la asignación resultante incluye todos los pares clave-valor de los mapas de entrada.

**Ejemplo**

El SQL siguiente crea un mapa donde cada elemento de `productListItems` está asociado con un número de secuencia, que luego se concatenará con otro mapa donde las claves se generan en un intervalo de secuencia específico.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilice element_at para recuperar un valor correspondiente a &quot;AAID&quot; en el mapa de identidad para un cálculo posterior {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

En el caso de las matrices, el fragmento devuelve el elemento en un índice especificado (basado en 1) o el valor asociado a una clave en un mapa. Si el índice es &lt; 0, tiene acceso a los elementos del último al primero y devuelve null si el índice supera la longitud de la matriz.

Para los mapas, devuelve un valor para la clave dada o nulo si la clave no está en el mapa.

**Ejemplo**

La consulta selecciona la columna `identitymap` de la tabla `geometrixxx_999_xdm_pqs_1batch_10k_rows` y extrae el valor asociado con la clave `AAID` para cada fila. Los resultados están restringidos a filas que se encuentran dentro del rango de marca de tiempo especificado y la consulta limita el resultado a diez filas.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## Utilice la cardinalidad para encontrar el número de identidades en el mapa de identidad {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

Este fragmento devuelve el tamaño de una matriz o mapa determinados y proporciona un alias. Devuelve -1 si el valor es nulo.

**Ejemplo**

La consulta siguiente recupera la columna `identitymap` y la función `Cardinality` calcula el número de elementos de cada mapa dentro de `identitymap`. Los resultados están limitados a diez filas y se filtran según un intervalo de marca de tiempo especificado.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## Utilice array_distinct para buscar los distintos elementos en productListItems {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

El fragmento anterior elimina los valores duplicados de la matriz determinada.

**Ejemplo**

La consulta siguiente selecciona la columna `productListItems`, quita los elementos duplicados de las matrices y limita el resultado a diez filas en función de un intervalo de marca de tiempo especificado.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultado**

Los resultados de este SQL aparecerían similares a los que se ven a continuación.

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### Funciones adicionales de orden superior {#additional-higher-order-functions}

Los siguientes ejemplos de funciones de orden superior se explican como parte del caso de uso recuperar registros similares. En la sección correspondiente de ese documento se proporciona un ejemplo y una explicación del uso de cada función.

El ejemplo de función [`transform` ](../use-cases/retrieve-similar-records.md#length-adjustment) cubre la tokenización de una lista de productos.

El ejemplo de la función [`filter` ](../use-cases/retrieve-similar-records.md#filter-results) muestra una extracción más refinada y precisa de información relevante de los datos de texto.

La función [`reduce`](../use-cases/retrieve-similar-records.md#higher-order-function-solutions) proporciona una forma de derivar valores acumulativos o agregados, que pueden ser fundamentales en varios procesos analíticos y de planificación.
