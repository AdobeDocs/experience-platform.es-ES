---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;spark sql;spark sql;spark sql funciones;funciones;
solution: Experience Platform
title: Funciones SQL de Spark en el servicio de consultas
description: Obtenga información acerca de las funciones compatibles de Spark SQL que amplían la funcionalidad de SQL.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 7ac1521adb916313c8b53fe2a095821d756480be
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 1%

---

# [!DNL Spark] Funciones SQL

Puede utilizar varias funciones SQL de Spark integradas para ampliar la funcionalidad SQL con Adobe Experience Platform Query Service. Este documento enumera las funciones SQL de Spark que admite el servicio de consultas.

Para obtener información más detallada sobre las funciones, incluida su sintaxis, uso y ejemplos, lea la [Documentación de la función Spark SQL](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>No se admiten todas las funciones de la documentación externa.

## Operadores y funciones matemáticos y estadísticos {#math}

| Operador/Función | Descripción |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | Devuelve el resto de los dos números |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Multiplica los dos números |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Suma los dos números |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Resta los dos números |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Divide los dos números |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Devuelve el valor absoluto de la entrada |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Devuelve el valor del coseno inverso |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Devuelve la cardinalidad estimada por HyperLogLog++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Devuelve el valor de percentil aproximado en un porcentaje determinado |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Devuelve el valor del seno inverso |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Devuelve el valor de tangente inverso |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Devuelve el ángulo entre el plano positivo del eje x y los puntos dados por las coordenadas |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Devuelve el valor promedio |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Devuelve la raíz de cubo |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) o [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Devuelve el menor entero igual o menor al valor introducido |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Convertir de una base a otra |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Devuelve el coeficiente de Pearson entre los números |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Devuelve el valor del coseno |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Devuelve el valor del coseno hiperbólico |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Devuelve el valor de la cotangente |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Devuelve la clasificación de un valor en un grupo de valores |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Devuelve el número de Euler |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Devuelve e a la potencia del valor |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Devuelve e a la potencia del valor menos 1 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Devuelve el factorial del valor |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Devuelve el mayor entero igual o menor al valor |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Devuelve el mayor valor de todos los parámetros |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Devuelve la hipotenusa de los dos valores dados |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Devuelve el valor de curtosis del grupo |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Devuelve el menor valor de todos los parámetros |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Devuelve el logaritmo natural del valor |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Devuelve el logaritmo del valor |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Devuelve el logaritmo en base 10 del valor |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Devuelve el logaritmo del valor más 1 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Devuelve el logaritmo, en base 2, del valor |
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
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Devuelve un número aleatorio del 0 al 1 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Devuelve un valor aleatorio |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Devuelve el valor doble más cercano |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Devuelve el valor redondeado más cercano |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Devuelve el signo del número |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Devuelve el seno del valor |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Devuelve el seno hiperbólico del valor |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Devuelve la raíz cuadrada del valor |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Devuelve la desviación estándar del valor |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Devuelve la desviación estándar de la población del valor |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Devuelve la desviación estándar de muestra del valor |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Devuelve la suma de los valores |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Devuelve la tangente del valor |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Devuelve la tangente hiperbólica del valor |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Devuelve la varianza de población calculada |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Devuelve la varianza de muestra calculada |

### Operadores lógicos y funciones {#logical-operators}

| Operador/Función | Descripción |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) o [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | No lógico |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Menor que |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | Menor o igual que |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Igual a |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Mayor que |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Mayor o igual que |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Exclusivo o bit a bit |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | OR bit a bit |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | No bit a bit |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Devuelve los elementos comunes |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Afirma si la expresión es verdadera |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Si la expresión se evalúa como verdadera, devuelva la segunda expresión. De lo contrario, devuelva la tercera expresión. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Si la expresión es nula, devuelve la segunda expresión. De lo contrario, devuelve la primera expresión. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Devuelve true si la primera expresión se encuentra en cualquiera de las expresiones siguientes. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Devuelve verdadero si el valor no es un número |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Devuelve verdadero si el valor no es nulo |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Devuelve verdadero si el valor es nulo |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Devuelve la primera expresión si no es un número; en caso contrario, devuelve la segunda expresión |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Lógico o |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Cuándo se puede utilizar para crear condiciones de rama para la comparación |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Devuelve true si la expresión XPath se evalúa como true o si se encuentra un nodo coincidente |

### Funciones de fecha y hora {#datetime-functions}

| Función | Descripción |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Agregar meses a la fecha |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Añadir días a la fecha |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Modificar formato de fecha |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Restar días de la fecha |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#date_trunc) | Devuelve la fecha truncada a la unidad especificada |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Devuelve la diferencia entre fechas en días |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Devuelve el día del mes |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#dayofweek) | Devuelve el día de la semana (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#dayofyear) | Devuelve el día del año |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Devuelve la fecha en UNIX® hora |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Devuelve la fecha en hora UTC |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#hour) | Devuelve la hora de la entrada |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Devuelve el último día del mes al que pertenece la fecha |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#minute) | Devuelve el minuto de la entrada |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#month) | Devuelve el mes de la entrada |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Número de meses entre |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Devuelve el primer día después de la entrada |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#quarter) | Devuelve el trimestre de la entrada |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Devuelve el segundo de la cadena |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#to_date) | Convierte la cadena en una fecha. **Nota:** La cadena **debe** estar en el formato `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#to_timestamp) | Convierte la cadena en una marca de tiempo. **Nota:** La cadena **debe** estar en el formato `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Convierte la cadena en una marca de tiempo UNIX® |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Convierte la cadena en una marca de tiempo UTC |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Trunca la fecha |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Devuelve la marca de tiempo UNIX® |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Día de la semana (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Devuelve la semana del año de una fecha determinada |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#year) | Devuelve el año de la cadena |

### Matrices {#arrays}

| Función | Descripción |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Crea una matriz con los elementos dados |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Comprueba si la matriz contiene el valor |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Quita los valores duplicados de la matriz |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Devuelve una matriz de los elementos de la primera matriz, pero no la segunda |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Devuelve la intersección de las dos matrices |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Une dos conjuntos |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Devuelve el valor máximo de la matriz |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Devuelve el valor mínimo de la matriz |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Devuelve la posición basada en 1 del elemento |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Quita todos los elementos iguales al elemento |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Crea una matriz que contiene el valor contabilizado veces |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Ordena la matriz |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Une la matriz, sin duplicados |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Combina los valores de matrices dadas con los valores de la colección original en un índice determinado |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Devuelve el tamaño de la matriz |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Devolver el elemento en la posición |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Separar elementos de una matriz en varias filas, excluyendo nulo |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Separe los elementos de la matriz en varias filas, incluido el valor nulo |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Devuelve la posición basada en 1 de la matriz |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Acople una matriz de matrices |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Separar matriz de estructuras en una tabla, excluyendo nulo |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Separe la matriz de estructuras en una tabla, incluido el cero |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | Separar elementos de una matriz en varias filas con posiciones, excluyendo nulo |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Invertir elementos de la matriz |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Devuelve una permutación aleatoria de la matriz |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Subconjuntos de una matriz |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Ordenar una matriz, dado un orden |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Combina las dos matrices en una sola matriz, antes de aplicar una función |

### Funciones de conversión de tipos de datos {#datatype-casting}

| Función | Descripción |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Cambie el tipo de datos a bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Cambiar el tipo de datos a binario |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Cambiar el tipo de datos a booleano |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Cambiar el tipo de datos al tipo especificado |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#date) | Cambiar el tipo de datos a fecha |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Cambiar el tipo de datos a decimal |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Cambiar el tipo de datos a doble |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Cambiar el tipo de datos a flotante |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Cambie el tipo de datos a int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Cambie el tipo de datos a smallint |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Creación de un mapa a partir de una cadena |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Cambiar el tipo de datos a cadena |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Creación de una estructura |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Cambiar el tipo de datos a tinyint |

### Funciones de conversión y formato {#conversion}

| Función | Descripción |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Devuelve el valor numérico (ASCII) |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Cambie el argumento a una cadena base64 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Cambie el argumento a un valor binario |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Devolver la longitud de bits |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Devuelve el carácter ASCII |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Devuelve la longitud de la cadena |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Devuelve el valor de comprobación de redundancia cíclica |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Convertir radianes a grados |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Cambiar el formato del número |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Obtener datos de JSON |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Devolver el valor hash |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Convertir el argumento en un valor hexadecimal |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Cambia la cadena para que sea un caso de título |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html?lang=es#lower) | Cambia la cadena para que esté en minúscula |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Rellena el lado izquierdo de una cadena |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Creación de un mapa |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Creación de un mapa a partir de una matriz |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Creación de un mapa a partir de una matriz de estructuras |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Devuelve el valor md5 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Rellena el lado derecho de una cadena |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Elimina los espacios finales |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | Devuelve el valor SHA1 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | Devuelve el valor SHA2 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Devolver el código soundex |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Separe los valores en filas |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Devuelve la subcadena |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Devuelve una cadena JSON |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Reemplazar valores dentro de una cadena |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Eliminar caracteres iniciales y finales |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Cambie la cadena para que esté en mayúsculas |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Convertir la cadena base64 en binaria |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Convertir el hexadecimal en binario |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Devolver un UUID |

### Evaluación de datos {#data-evaluation}

| Función | Descripción |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Devolver el primer argumento no nulo |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Devuelve una lista de elementos no únicos |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Devuelve un conjunto de elementos únicos |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Concatenación |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Concatenación con separador |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Devuelve el recuento total de filas |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Descodificar mediante un conjunto de caracteres |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Devuelva el [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)la entrada |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Codificar con un conjunto de caracteres |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Devuelve el primer valor |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Indica si una columna está agrupada |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Devuelve el nivel de agrupación |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Devuelve un índice de ocurrencia de caracteres basado en 1 |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Devuelve una tupla desde una entrada JSON |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Devuelve el valor antes del desplazamiento |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Devuelve el último valor |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Devuelve el primero [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) caracteres |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Devuelve la longitud de la cadena |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Devuelve la distancia entre cadenas de Levenshtein |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Devuelve la posición de la primera aparición de una subcadena |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Concatenación de un mapa |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Devolver las claves de un mapa |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Devolver los valores de un mapa |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Dividir filas en particiones |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Devuelve nulo si es verdadero |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Devuelve el valor si es nulo |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Devuelve un valor si no es nulo |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extrae parte de una dirección URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Calcula la clasificación de un valor |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extrae algo que coincide con la regex |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Reemplaza algo que coincide con la regex |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Devuelve una cadena que se repite |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Reemplazar todas las instancias de una cadena |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Creación de un resumen multidimensional |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Asigna un número de fila único |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Devuelve el esquema del JSON |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Divide una cadena en una matriz de palabras |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Genera una matriz de elementos |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Desplazamiento hacia la izquierda bit firmado |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Desplazamiento hacia la derecha bit firmado |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Desplazamiento hacia la derecha bit sin signo |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Devuelve el tamaño de la matriz |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Devuelve una cadena con [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) espacios |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Cadena dividida |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Devolver índice de subcadena |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Ventana |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Analizar nodos XML |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Analizar nodos XML para el doble |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Analizar nodos XML para float |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Analizar nodos XML para enteros |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Analizar nodos XML durante mucho tiempo |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | Analizar nodos XML para entero corto |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Analizar nodos XML para la cadena |

### Información actual {#current-information}

| Función | Descripción |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Devuelve la base de datos actual |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Devuelve fecha actual |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Devuelve la marca de tiempo actual |

### Funciones de orden superior {#higher-order}

| Función | Descripción |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Transformación de elementos en una matriz |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Comprobar si el elemento existe |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtrado de la matriz de entrada |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Aplicar un operador binario a todos los elementos |
