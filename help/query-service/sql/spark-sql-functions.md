---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;spark sql;Spark sql;spark sql function;funciones;
solution: Experience Platform
title: Spark SQL funciones
topic: spark sql functions
description: Esta documentación contiene información sobre las funciones Spark SQL que amplían la funcionalidad SQL.
translation-type: tm+mt
source-git-commit: 019de34c5e4ac53d38887752e893733f843dd22f
workflow-type: tm+mt
source-wordcount: '3890'
ht-degree: 1%

---


# [!DNL Spark] Funciones SQL

El servicio de Consulta de Adobe Experience Platform proporciona varias funciones SQL Spark integradas para ampliar la funcionalidad SQL. Este documento lista las funciones Spark SQL admitidas por el servicio de Consulta.

Para obtener información más detallada sobre las funciones, incluida su sintaxis, uso y ejemplos, lea la [documentación de funciones SQL de Spark](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>No todas las funciones de la documentación externa son compatibles.

## Categorías

- [Funciones y operadores matemáticos y estadísticos](#math)
- [Operadores lógicos](#logical-operators)
- [Funciones de fecha y hora](#datetime-functions)
- [Matrices](#arrays)
- [Funciones de conversión de tipos de datos](#datatype-casting)
- [Funciones de conversión y formato](#conversion)
- [Evaluación de datos](#data-evaluation)
- [Información actual](#current-information)
- [Funciones de orden superior](#higher-order)

## Operadores y funciones matemáticas y estadísticas {#math}

| Operador/Función | Descripción |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_2) | Devuelve el resto de los dos números |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_4) | Multiplica los dos números |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Añade los dos números |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Resta los dos números |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Divide los dos números |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Devuelve el valor absoluto de la entrada |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Devuelve el valor de coseno inverso |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Devuelve la cardinalidad estimada por HyperLogLog++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Devuelve el valor del percentil aproximado en un porcentaje determinado |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Devuelve el valor del seno inverso |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Devuelve el valor de tangente inverso |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Devuelve el ángulo entre el plano positivo del eje X y los puntos dados por las coordenadas |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Devuelve el valor promedio |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Devuelve la raíz del cubo |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) O bien [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Devuelve el entero más pequeño que no es mayor que el valor introducido |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Convertir de una base a otra |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Devuelve el coeficiente de Pearson entre los números |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Devuelve el valor de coseno |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Devuelve el valor de coseno hiperbólico |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Devuelve el valor de cotangente |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Devuelve la clasificación de un valor de un grupo de valores |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Devuelve el número de Euler |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Devuelve e a la potencia del valor |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Devuelve e a la potencia del valor menos 1 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Devuelve el factorial del valor |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Devuelve el mayor entero no menor que el valor |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Devuelve el valor más alto de todos los parámetros |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Devuelve la hipotensión de los dos valores indicados |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Devuelve el valor de kurtosis del grupo |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Devuelve el valor más pequeño de todos los parámetros |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Devuelve el logaritmo natural del valor |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Devuelve el logaritmo del valor |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Devuelve el logaritmo, en la base 10, del valor |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Devuelve el logaritmo del valor más 1 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Devuelve el logaritmo, en la base 2, del valor |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Devuelve el valor máximo de la expresión |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Devuelve la media calculada a partir de los valores |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Devuelve el valor mínimo de la expresión |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Devuelve ID que aumentan monotónicamente |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Devuelve el valor negado |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Devuelve la clasificación porcentual de un valor |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Devuelve el percentil exacto en un porcentaje determinado |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Devuelve el percentil aproximado en un porcentaje determinado |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Devuelve pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Devuelve el módulo positivo entre dos valores |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Devuelve el valor positivo |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Devuelve el primer valor a la potencia del segundo valor |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Convierte el valor en radianes |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Devuelve un número aleatorio entre 0 y 1 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Devuelve un valor aleatorio |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Devuelve el valor de doble más cercano |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Devuelve el valor redondeado más cercano |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign),  [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Devuelve el signo del número |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Devuelve el seno del valor |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Devuelve el seno hiperbólico del valor |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Devuelve la raíz cuadrada del valor |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Devuelve la desviación estándar del valor |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Devuelve la desviación estándar de población del valor |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Devuelve la desviación estándar de muestra del valor |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Devuelve la suma de los valores |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Devuelve tangente del valor |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Devuelve la tangente hiperbólica del valor |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Devuelve la varianza de población calculada |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp),  [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Devuelve la varianza de muestra calculada |

### Operadores lógicos y funciones {#logical-operators}

| Operador/Función | Descripción |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) O bien [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | No lógico |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Less than |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Less than or equal to |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_10) | Equal to |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Greater than |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Greater than or equal to |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Exclusivo en modo bit o |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Bueno mayor o igual que |
| [`|`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | En modo bit o |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitwise not |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Devuelve los elementos comunes |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Afirma si la expresión es verdadera |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Si la expresión se evalúa como verdadera, devuelve la segunda expresión. De lo contrario, devuelva la tercera expresión. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Si la expresión es nula, devuelve la segunda expresión. De lo contrario, devuelve la primera expresión. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Devuelve true si la primera expresión está en cualquiera de las expresiones posteriores. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Devuelve true si el valor no es un número |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Devuelve true si el valor no es nulo |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Devuelve true si el valor es nulo |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Devuelve la primera expresión, si no es un número, y la segunda expresión, en caso contrario |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Lógico o |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Cuándo se puede utilizar para crear condiciones de ramificación para la comparación |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Devuelve true si la expresión XPath se evalúa como true o si se encuentra un nodo coincidente |

### Funciones de fecha y hora {#datetime-functions}

| Función | Descripción |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Añadir meses hasta la fecha |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Añadir días hasta la fecha |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Modificar formato de fecha |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Restar días de la fecha |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Devuelve la fecha truncada a la unidad especificada |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Devuelve la diferencia entre fechas en días |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day),  [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Devuelve el día del mes |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Devuelve el día de la semana (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Devuelve el día del año |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Devuelve la fecha en hora Unix |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Devuelve la fecha en hora UTC |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Devuelve la hora de entrada |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Devuelve el último día del mes al que pertenece la fecha |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Devuelve el minuto de entrada |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Devuelve el mes de la entrada |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Número de meses entre |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Devuelve el primer día después de la entrada |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Devuelve el trimestre de la entrada |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Devuelve el segundo de la cadena |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Convierte la cadena en una fecha |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Convierte la cadena en una marca de tiempo |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Convierte la cadena en una marca de hora Unix |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Convierte la cadena en una marca de hora UTC |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Trunca la fecha |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Devuelve la marca de hora Unix |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Día de la semana (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Devuelve la semana del año de una fecha determinada |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Devuelve el año de la cadena |

### Arreglos {#arrays}

| Función | Descripción |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Crea una matriz con los elementos dados |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Comprueba si la matriz contiene el valor |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Quita los valores de duplicado de la matriz |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Devuelve una matriz de los elementos de la primera matriz, pero no la segunda |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Devuelve la intersección de los dos conjuntos |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Une dos arreglos de discos |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Devuelve el valor máximo de la matriz |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Devuelve el valor mínimo de la matriz |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Devuelve la posición basada en 1 del elemento |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Quita todos los elementos iguales al elemento |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Crea una matriz que contiene el valor de los tiempos contados |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Ordena la matriz |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Une la matriz, sin ningún duplicado |
| [`array_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Código postal |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Devolver el tamaño de la matriz |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Devolver el elemento en la posición |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Separe los elementos de la matriz en varias filas, excluyendo null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Separe los elementos de la matriz en varias filas, incluyendo null |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Devuelve la posición basada en 1 de la matriz |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Acopla una matriz de arreglos de discos |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Matriz separada de estructuras en una tabla, excluyendo null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Matriz separada de estructuras en una tabla, incluyendo null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Separe los elementos de la matriz en varias filas con posiciones, excluyendo null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Separe los elementos de la matriz en varias filas con posiciones, incluyendo nulo |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Invertir elementos de la matriz |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Devolver una permutación aleatoria de la matriz |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Subestablece una matriz |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Ordenar una matriz, según un pedido |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Combina las dos matrices en una sola matriz antes de aplicar una función |

### Funciones de conversión de tipos de datos {#datatype-casting}

| Función | Descripción |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Cambiar el tipo de datos a bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Cambiar el tipo de datos a binario |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Cambiar el tipo de datos a booleano |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Cambiar el tipo de datos al tipo especificado |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Cambiar el tipo de datos a la fecha |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Cambiar el tipo de datos a decimal |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Cambiar el tipo de datos a doble |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Cambiar el tipo de datos a flotante |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Cambiar el tipo de datos a int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Cambiar el tipo de datos a pequeño |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Creación de un mapa a partir de una cadena |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Cambiar el tipo de datos a cadena |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Crear una estructura |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Cambiar el tipo de datos a tinyint |

### Funciones de conversión y formato {#conversion}

| Función | Descripción |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Devolver el valor numérico (ASCII) |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Cambiar el argumento a una cadena base64 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Cambiar el argumento a un valor binario |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Devolver la longitud de bits |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char),  [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Devolver el carácter ASCII |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length),  [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Devolver la longitud de la cadena |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Devuelve el valor de comprobación de redundancia cíclica |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Convertir radianes a grados |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Cambiar el formato del número |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json),  [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Obtener datos de JSON |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Devolver el valor hash |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Convertir el argumento en un valor hexadecimal |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Cambia la cadena a la que se va a escribir en mayúsculas |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase),  [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Cambia la cadena a minúsculas |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Se coloca en el lado izquierdo de una cadena |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Crear un mapa |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Creación de un mapa a partir de una matriz |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Crear un mapa a partir de una matriz de estructuras |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Devolver el valor de md5 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Pads el lado derecho de una cadena |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Elimina los espacios finales |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha),  [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | Devolver el valor SHA1 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | Devolver el valor SHA2 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Devolver el código soundex |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Separar valores en filas |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr),  [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Devolver la subcadena |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Devuelve una cadena JSON |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Reemplazar valores en la cadena |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Eliminar caracteres al inicio y al final |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase),  [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Cambiar la cadena a mayúsculas |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Convertir la cadena base64 en binaria |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Convertir el hexadecimal a binario |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Devolver un UUID |

### Evaluación de datos {#data-evaluation}

| Función | Descripción |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Devolver el primer argumento no nulo |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Devolver una lista de elementos no únicos |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Devolver un conjunto de elementos únicos |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Concatenación |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Concatenación con separador |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Devuelve el recuento total de filas |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Decodificación con un conjunto de caracteres |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Devuelve la entrada [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)th |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Codificación mediante un conjunto de caracteres |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first),  [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Devuelve el primer valor |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Indica si una columna está agrupada |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Devuelve el nivel de agrupación |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Devuelve un índice de incidencia de caracteres basado en 1 |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Devuelve un tupla de una entrada JSON |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag),  [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Devuelve el valor antes del desplazamiento |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last),  [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Devuelve el último valor |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Devuelve los primeros [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) caracteres |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Devuelve la longitud de la cadena |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Devuelve la distancia de Levenshtein entre cadenas |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate),  [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Devuelve la posición de la primera incidencia de una subcadena |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Concatenar un mapa |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Devolver las claves de un mapa |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Devolver los valores de un mapa |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Dividir filas en particiones |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Devuelve nulo si es verdadero |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Devuelve el valor si es nulo |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Devuelve el valor si no es nulo |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extrae parte de una dirección URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Calcula la clasificación de un valor |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extrae algo que coincide con el regex |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Reemplaza algo que coincida con el regex |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Devuelve una cadena que se repite |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Reemplazar todas las instancias de una cadena |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Crear un resumen multidimensional |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Asigna un número de fila único |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Devuelve el esquema del JSON |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Divide la cadena en una matriz de palabras |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Genera una matriz de elementos |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Desplazamiento hacia la izquierda en modo bit firmado |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Desplazamiento a la derecha en modo bit firmado |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Desplazamiento a la derecha en modo bit sin signo |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Devolver el tamaño de la matriz |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Devolver una cadena con [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) espacios |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Dividir cadena |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Índice de devolución de subcadena |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Ventana |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Analizar nodos XML |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double),  [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Analizar nodos XML para doble |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Analizar nodos XML para float |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Analizar nodos XML para enteros |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Analizar nodos XML durante mucho tiempo |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | Analizar nodos XML para número entero corto |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Analizar nodos XML para la cadena |

### Información actual {#current-information}

| Función | Descripción |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Devuelve la base de datos actual |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Devuelve la fecha actual |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp),  [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Devuelve la marca de tiempo actual |

### Funciones de orden más alto {#higher-order}

| Función | Descripción |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Transformar elementos en una matriz |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Comprobar si el elemento existe |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtrar la matriz de entrada |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Aplicar un operador binario a todos los elementos |