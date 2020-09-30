---
keywords: Experience Platform;home;popular topics;query service;Query service;spark sql;Spark sql;spark;spark sql functions;functions;
solution: Experience Platform
title: Spark SQL funciones
topic: spark sql functions
description: Esta documentación contiene información sobre los ayudantes de Spark SQL que proporcionan las funciones integradas de Spark SQL para ampliar la funcionalidad de SQL.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '5009'
ht-degree: 5%

---


# [!DNL Spark] Funciones SQL

Los asistentes [!DNL Spark] SQL proporcionan funciones [!DNL Spark] SQL integradas para ampliar la funcionalidad SQL.

Referencia: [Documentación de la función Spark SQL](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE]
>
>No todas las funciones de la documentación externa son compatibles.

## Categorías

- [Funciones y operadores matemáticos y estadísticos](#math)
- [Operadores lógicos](#logical-operators)
- [Funciones de fecha y hora](#datetime-functions)
- [Funciones acumuladas](#aggregate-functions)
- [Matrices](#arrays)
- [Funciones de conversión de tipos de datos](#datatype-casting)
- [Funciones de conversión y formato](#conversion)
- [Evaluación de datos](#data-evaluation)
- [Información actual](#current-information)
- [Funciones de orden superior](#higher-order)

### Funciones y operadores matemáticos y estadísticos {#math}

#### Módulo

`expr1 % expr2`:: Devuelve el resto después `expr1`/`expr2`.

Ejemplos:

```sql
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Multiplicar

`expr1 * expr2`: Devuelve `expr1`*`expr2`.

Ejemplo:

```sql
> SELECT 2 * 3;
 6
```

#### Add

`expr1 + expr2`: Devuelve `expr1`+`expr2`.

Ejemplo:

```sql
> SELECT 1 + 2;
 3
```

#### Restar

`expr1 - expr2`: Devuelve `expr1`-`expr2`.

Ejemplo:

```sql
> SELECT 2 - 1;
 1
```

#### Dividir

`expr1 / expr2`: Devuelve `expr1`/`expr2`. Siempre realiza una división de punto flotante.

Ejemplos:

```sql
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`:: Devuelve el valor absoluto del valor numérico.

Ejemplo:

```sql
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`:: Devuelve el coseno inverso (también conocido como coseno de arco) de `expr`, como si se hubiera calculado mediante `java.lang.Math.acos`.

Ejemplos:

```sql
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### aprox_percentile

`approx_percentile(col, percentage [, accuracy])`:: Devuelve el valor del percentil aproximado de la columna numérica `col` en el porcentaje determinado. El valor del porcentaje debe estar entre 0,0 y 1,0. El `accuracy` parámetro (predeterminado: 10000) es un literal numérico positivo que controla la precisión de aproximación al costo de la memoria. Un valor mayor de `accuracy` produce una mayor precisión, `1.0/accuracy` es el error relativo de la aproximación. Cuando `percentage` es una matriz, cada valor de la matriz de porcentajes debe estar entre 0,0 y 1,0. En este caso, se devuelve la matriz de percentil aproximada de la columna `col` en la matriz de porcentaje dada.

Ejemplos:

```sql
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`:: Devuelve el seno inverso (también conocido como arco seno), el seno arco de `expr`, como si se hubiera calculado mediante `java.lang.Math.asin`.

Ejemplos:

```sql
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`:: Devuelve la tangente inversa (también conocida como tangente de arco) de `expr`, como si se computara mediante `java.lang.Math.atan`

Ejemplo:

```sql
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`:: Devuelve el ángulo en radianes entre el eje x positivo de un plano y el punto proporcionado por las coordenadas (`exprX`, `exprY`), como si se calculara mediante `java.lang.Math.atan2`.

Argumentos:

`exprY`:: Coordenadas en el eje`exprX`Y: Coordenadas en eje x

Ejemplo:

```sql
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`:: Devuelve la media calculada a partir de los valores de un grupo.

#### cardinalidad

`cardinality(expr)`:: Devuelve el tamaño de una matriz o un mapa. La función devuelve -1 si su entrada es nula y `spark.sql.legacy.sizeOfNull` se establece en true (valor predeterminado). Si `spark.sql.legacy.sizeOfNull` se establece en false, la función devuelve null para la entrada null.

Ejemplos:

```sql
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`:: Devuelve la raíz de cubo de `expr`.

Ejemplo:

```sql
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`:: Devuelve el entero más pequeño que no sea menor que `expr`.

Ejemplos:

```sql
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### techo

`ceiling(expr)`:: Devuelve el entero más pequeño que no sea menor que `expr`.

Ejemplos:

```sql
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`:: Convertir `num` de `from_base` a `to_base`

Ejemplos:

```sql
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`:: Devuelve el coeficiente Pearson de la correlación entre un conjunto de pares de números.

#### cos

`cos(expr)`:: Devuelve el coseno de `expr`, como si se hubiera calculado mediante `java.lang.Math.cos`.

Ejemplo:

```sql
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`:: Devuelve el coseno hiperbólico de `expr`, como si se hubiera calculado mediante `java.lang.Math.cosh`.

Argumentos:
- `expr`:: Ángulo hiperbólico

Ejemplo:

```
> SELECT cosh(0);
 1.0
```

#### cuna

`cot(expr)`:: Devuelve la cotangente de `expr`, como si se hubiera calculado mediante `1/java.lang.Math.cot`.

Argumentos:
- `expr`:: Ángulo en radianes

Ejemplo:

```sql
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`:: Calcula la clasificación de un valor en un grupo de valores. El resultado es uno más el valor de clasificación asignado anteriormente. A diferencia de la función `rank`, `dense_rank` no produce espacios en la secuencia de clasificación.

#### e

`e()`:: Devuelve el número de Euler, e.

Ejemplo:

```sql
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`:: Devuelve e a la potencia de `expr`.

Ejemplo:

```sql
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`:: Devuelve exp(`expr`) - 1.

Ejemplo:

```sql
> SELECT expm1(0);
 0.0
```

#### factorial

`factorial(expr)`:: Devuelve el factorial de `expr`. `expr` es [0.20]. En caso contrario, null.

Ejemplo:

```
> SELECT factorial(5);
 120
```

#### floor

`floor(expr)`:: Devuelve el mayor entero no bueno que `expr`.

Ejemplos:

```sql
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### bueno

`greatest(expr, ...)`:: Devuelve el valor bueno de todos los parámetros, omitiendo valores nulos.

Ejemplo:

```sql
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypot

`hypot(expr1, expr2)`:: Devuelve sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>).

Ejemplo:

```sql
> SELECT hypot(3, 4);
 5.0
```

#### kurtosis

`kurtosis(expr)`:: Devuelve el valor de kurtosis calculado a partir de los valores de un grupo.


#### least

`least(expr, ...)`:: Devuelve el valor mínimo de todos los parámetros, omitiendo valores nulos.

Ejemplo:

```sql
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)`:: Devuelve la distancia de Levenshtein entre las dos cadenas dadas.

Ejemplos:

```sql
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`:: Devuelve el logaritmo natural (base e) de `expr`.

Ejemplo:

```sql
> SELECT ln(1);
 0.0
```

#### registro

`log(base, expr)`:: Devuelve el logaritmo de `expr` with `base`.

Ejemplo:

```sql
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`:: Devuelve el logaritmo de `expr` con base 10.

Ejemplo:

```sql
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Devuelve `log(1 + expr)`.

Ejemplo:

```sql
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`:: Devuelve el logaritmo de `expr` con base 2.

Ejemplo:

```sql
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`:: Devuelve el valor máximo de `expr`.

#### media

`mean(expr)`:: Devuelve la media calculada a partir de los valores de un grupo.

#### min

`min(expr)`:: Devuelve el valor mínimo de `expr`.

#### monotonical_creciente_id

`monotonically_increasing_id()`:: Devuelve enteros de 64 bits que aumentan monotónicamente. La ID generada está garantizada para aumentar monotónicamente y ser única, pero no consecutiva. La implementación actual coloca el ID de partición en los 31 bits superiores y los 33 bits inferiores representan el número de registro dentro de cada partición. Se supone que el marco de datos tiene menos de mil millones de particiones y cada partición tiene menos de 8 mil millones de registros. La función no es determinística porque su resultado depende de los ID de partición.

#### negative

`negative(expr)`:: Devuelve el valor negado de `expr`.

Ejemplo:

```sql
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`:: Calcula la clasificación porcentual de un valor en un grupo de valores.

#### percentil

`percentile(col, percentage [, frequency])`:: Devuelve el valor del percentil exacto de la columna numérica `col` en el porcentaje determinado. El valor de `percentage` debe estar entre 0,0 y 1,0. El valor de `frequency` debe ser una parte integral positiva.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`:: Devuelve la matriz de valores del percentil exacto de la columna numérica `col` en los porcentajes determinados. Cada valor de la matriz de porcentajes debe estar entre 0,0 y 1,0. El valor de `frequency` debe ser una parte integral positiva.

#### percentile_aprox

`percentile_approx(col, percentage [, accuracy])`:: Devuelve el valor del percentil aproximado de la columna numérica `col` en el porcentaje determinado. El valor de `percentage` debe estar entre 0,0 y 1,0. El `accuracy` parámetro (predeterminado: 10000) es un literal numérico positivo que controla la precisión de aproximación al costo de la memoria. Un valor mayor de `accuracy` produce una mayor precisión, `1.0/accuracy` es el error relativo de la aproximación. Cuando `percentage` es una matriz, cada valor de la matriz de porcentajes debe estar entre 0,0 y 1,0. En este caso, devuelve la matriz de percentil aproximada de la columna `col` en la matriz de porcentaje dada.

Ejemplos:

```sql
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`:: Devuelve pi.

Ejemplo:

```sql
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`:: Devuelve el valor positivo de `expr1` mod `expr2`.

Ejemplos:

```sql
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positivo

`positive(expr)`:: Devuelve el valor positivo de `expr`

#### pow

`pow(expr1, expr2)`:: Se eleva `expr1` al poder de `expr2`.

Ejemplo:

```sql
> SELECT pow(2, 3);
 8.0
```

#### power

`power(expr1, expr2)`:: Se eleva `expr1` al poder de `expr2`.

Ejemplos:

```sql
> SELECT power(2, 3);
 8.0
```

#### radianes

`radians(expr)`:: Convierte los grados en radianes.

Argumentos:

- `expr`:: Ángulo en grados

Ejemplo:

```sql
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`:: Devuelve un valor aleatorio con valores distribuidos uniformemente independientes e idénticamente distribuidos (i.i.d.) en (0, 1).

Ejemplos:

```sql
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE]
>
>Esta función no es determinística en el caso general.

#### randn

`randn([seed])`:: Devuelve un valor aleatorio con valores independientes y distribuidos de forma idéntica (i.i.d.) extraídos de la distribución normal estándar.

Ejemplos:

```sql
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE]
>
>Esta función no es determinística en el caso general.

#### imprimir

`rint(expr)`:: Devuelve el valor de doble más cercano en valor al argumento y es igual a un entero matemático.

Ejemplos:

```sql
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`:: Devuelve `expr` redondeado a `d` decimales utilizando el modo de redondeo HALF_UP.

Ejemplo:

```sql
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)`:: Devuelve -1.0, 0.0 o 1.0, ya que `expr` es negativo, 0 o positivo.

Ejemplo:

```sql
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`:: Devuelve -1.0, 0.0 o 1.0, ya que `expr` es negativo, 0 o positivo.

Ejemplo:

```sql
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`:: Devuelve el seno de `expr`, como si se hubiera calculado mediante `java.lang.Math.sin`.

Argumentos:

- `expr`:: Ángulo en radianes

Ejemplo:

```sql
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`:: Devuelve el seno hiperbólico de `expr`, como si se hubiera calculado mediante `java.lang.Math.sinh`.

Argumentos:

- `expr`:: Ángulo hiperbólico

Ejemplo:

```sql
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`:: Devuelve la raíz cuadrada de `expr`.

Ejemplo:

```sql
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`:: Devuelve la desviación estándar de muestra calculada a partir de los valores de un grupo.

#### stddev_pop

`sttdev_pop(expr)`:: Devuelve la desviación estándar de población calculada a partir de los valores de un grupo.

#### stddev_samp

`stddev_samp(expr)`:: Devuelve la desviación estándar de muestra calculada a partir de los valores de un grupo.

#### sum

`sum(expr)`:: Devuelve la suma calculada a partir de los valores de un grupo.

#### than

`tan(expr)`:: Devuelve la tangente de `expr`, como si se hubiera calculado mediante `java.lang.Math.tan`.

Argumentos:

- `expr`:: Ángulo en radianes

Ejemplo:

```sql
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`:: Devuelve la tangente hiperbólica de `expr`, como si se hubiera calculado mediante `java.lang.Math.tanh`.

Argumentos:

- `expr`:: Ángulo hiperbólico

Ejemplo:

```sql
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`:: Devuelve la varianza de población calculada a partir de los valores de un grupo.

#### Var_samp

`var_samp(expr)`:: Devuelve la varianza de muestra calculada a partir de los valores de un grupo.

#### varianza

`variance(expr)`:: Devuelve la varianza de muestra calculada a partir de los valores de un grupo.

### Operadores lógicos {#logical-operators}

#### No lógico

`! expr`:: No lógico.

#### Less than

`expr1 < expr2`:: Devuelve true si `expr1` es menor que `expr2`.

Argumentos:

- `expr1, expr2`:: Las dos expresiones deben ser del mismo tipo o se pueden convertir en un tipo común y deben ser un tipo que se pueda ordenar. Por ejemplo, el tipo de mapa no se puede ordenar, por lo que no se admite. Para tipos complejos como matriz/estructura, los tipos de datos de los campos deben poder pedirse.

Ejemplos:

```sql
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### Less than or equal to

`expr1 <= expr2`:: Devuelve true si `expr1` es menor o igual que `expr2`.

Argumentos:

- `expr1, expr2`:: Las dos expresiones deben ser del mismo tipo o pueden convertirse en un tipo común, y deben ser un tipo que se pueda ordenar. Por ejemplo, el tipo de mapa no se puede ordenar, por lo que no se admite. Para tipos complejos como matriz/estructura, los tipos de datos de los campos deben poder pedirse.

Ejemplos:

```sql
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### Equal to

`expr1 = expr2`:: Devuelve true si `expr1` es igual a `expr2`, o false en caso contrario.

Argumentos:

- `expr1, expr2`:: Las dos expresiones deben ser del mismo tipo o se pueden convertir en un tipo común y deben ser un tipo que se pueda utilizar en comparación de igualdad. No se admite el tipo de mapa. Para tipos complejos como matriz/estructura, los tipos de datos de los campos deben poder pedirse.

Ejemplos:

```sql
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### Greater than

`expr1 > expr2`:: Devuelve true si `expr1` es bueno que `expr2`.

Argumentos:

- `expr1, expr2`:: Las dos expresiones deben ser del mismo tipo o se pueden convertir en un tipo común y deben ser un tipo que se pueda ordenar. Por ejemplo, el tipo de mapa no se puede ordenar, por lo que no se admite. Para tipos complejos como matriz/estructura, los tipos de datos de los campos deben poder pedirse.

Ejemplos:

```sql
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### Greater than or equal to

`expr1 >= expr2`:: Devuelve true si `expr1` es bueno o igual a `expr2`.

Argumentos:

- `expr1, expr2`:: Las dos expresiones deben ser del mismo tipo o se pueden convertir en un tipo común y deben ser un tipo que se pueda ordenar. Por ejemplo, el tipo de mapa no se puede ordenar, por lo que no se admite. Para tipos complejos como matriz/estructura, los tipos de datos de los campos deben poder pedirse.

Ejemplos:

```sql
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Exclusivo en modo bit o

`expr1 ^ expr2`:: Devuelve el resultado de OR exclusivo en modo bit de `expr1` y `expr2`.

Ejemplo:

```sql
> SELECT 3 ^ 5;
 2
```

#### y

`expr1 and expr2`:: AND lógico.

#### array_superposición

`arrays_overlap(a1, a2)`:: Devuelve true si a1 contiene al menos un elemento no nulo presente también en a2. Si las matrices no tienen un elemento común y no están vacías y cualquiera de ellas contiene un elemento nulo, se devuelve nulo. De lo contrario, se devuelve false.

Ejemplo:

```sql
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Desde: 2.4.0

#### assert_true

`assert_true(expr)`:: Emite una excepción si `expr` no es true.

Ejemplo:

```sql
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`:: Si `expr1` se evalúa como true, devuelve `expr2`; en caso contrario, devuelve `expr3`.

Ejemplo:

```sql
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`:: Devuelve `expr2` si `expr1` es nulo o `expr1` no.

Ejemplo:

```sql
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`:: Devuelve true si `expr` es igual a cualquier valN.

Argumentos:
- `expr1, expr2, expr3, ...`:: Los argumentos deben ser del mismo tipo.

Ejemplos:

```sql
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`:: Devuelve true si `expr` es NaN o false en caso contrario.

Ejemplo:

```sql
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`:: Devuelve true si `expr` no es nulo o false en caso contrario.

Ejemplos:

```sql
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`:: Devuelve true si `expr` es nulo o false en caso contrario.

Ejemplo:

```sql
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`:: Devuelve `expr1` si no es NaN o `expr2` no es así.

Ejemplo:

```sql
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`:: No lógico.

#### O bien

`expr1 or expr2`:: O lógico.

#### xpath_boolean

`xpath_boolean(xml, xpath)`:: Devuelve true si la expresión XPath se evalúa como true o si se encuentra un nodo coincidente.

Ejemplo:

```sql
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Funciones de fecha y hora {#datetime-functions}

#### add_month

`add_months(start_date, num_months)`:: Devuelve la fecha que sigue `num_months` a `start_date`.

Ejemplo:

```sql
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Desde: 1.5.0

#### date_add

`date_add(start_date, num_days)`:: Devuelve la fecha que sigue `num_days` a `start_date`.

Ejemplo:

```sql
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Desde: 1.5.0

#### date_format

`date_format(timestamp, fmt)`:: Convierte `timestamp` a un valor de cadena en el formato especificado por el formato de fecha `fmt`.

Ejemplo:

```sql
> SELECT date_format('2016-04-08', 'y');
 2016
```

Desde: 1.5.0

#### date_sub

`date_sub(start_date, num_days)`:: Devuelve la fecha que es `num_days` anterior a `start_date`.

Ejemplo:

```sql
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Desde: 1.5.0

#### date_trunc

`date_trunc(fmt, ts)`:: Devuelve las marcas de hora truncadas a la unidad especificada por el modelo de formato `fmt`. `fmt` debe ser uno de [&quot;AÑO&quot;, &quot;AÑO&quot;, &quot;AÑO&quot;, &quot;AÑO&quot;, &quot;MÓN&quot;, &quot;MES&quot;, &quot;MM&quot;, &quot;DÍA&quot;, &quot;DD&quot;, &quot;HORA&quot;, &quot;MINUTO&quot;, &quot;SEGUNDO&quot;, &quot;SEMANA&quot;, &quot;TRIMESTRE&quot;]

Ejemplos:

```sql
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

Desde: 2.3.0

#### datediff

`datediff(endDate, startDate)`:: Devuelve el número de días del `startDate` al `endDate`.

Ejemplos:

```sql
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Desde: 1.5.0

#### día

`day(date)`:: Devuelve el día del mes de la fecha/marca de hora.

Ejemplo:

```sql
> SELECT day('2009-07-30');
 30
```

Desde: 1.5.0

#### dayofmonth

`dayofmonth(date)`:: Devuelve el día del mes de la fecha/marca de hora.

Ejemplo:

```sql
> SELECT dayofmonth('2009-07-30');
 30
```

Desde: 1.5.0

#### dayofweek

`dayofweek(date)`:: Devuelve el día de la semana para fecha/marca de hora (1 = domingo, 2 = lunes, ..., 7 = sábado).

Ejemplo:

```sql
> SELECT dayofweek('2009-07-30');
 5
```

Desde: 2.3.0

#### dayofyear

`dayofyear(date)`:: Devuelve el día del año de la fecha/marca de hora.

Ejemplo:

```sql
> SELECT dayofyear('2016-04-09');
 100
```

Desde: 1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`:: Devuelve `unix_time` el valor especificado `format`.

Ejemplo:

```sql
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Desde: 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`:: Interpreta una marca de tiempo como &#39;2017-07-14 02:40:00.0&#39; como una hora en UTC y representa esa hora como una marca de tiempo en el huso horario determinado. Por ejemplo, &#39;GMT+1&#39; daría como resultado &#39;2017-07-14 03:40:00.0&#39;.

Ejemplo:

```sql
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Desde: 1.5.0

#### hora

`hour(timestamp)`:: Devuelve el componente de hora de la cadena/marca de hora.

Ejemplo:

```sql
> SELECT hour('2009-07-30 12:58:59');
 12
```

Desde: 1.5.0

#### last_day

`last_day(date):` Devuelve el último día del mes al que pertenece la fecha.

Ejemplo:

```sql
> SELECT last_day('2009-01-12');
 2009-01-31
```

Desde: 1.5.0

#### minuto

`minute(timestamp)`:: Devuelve el componente de minuto de la cadena/marca de tiempo.

Ejemplo:

```sql
> SELECT minute('2009-07-30 12:58:59');
 58
```

Desde: 1.5.0

#### mes

`month(date)` Devuelve el componente de mes de la fecha y la marca de hora.

Ejemplo:

```sql
> SELECT month('2016-07-30');
 7
```

Desde: 1.5.0

#### month_between

`months_between(timestamp1, timestamp2[, roundOff])`:: Si `timestamp1` es posterior a `timestamp2`, el resultado es positivo. Si `timestamp1` y `timestamp2` son el mismo día del mes, o ambos son el último día del mes, se ignorará la hora del día. De lo contrario, la diferencia se calcula en función de 31 días al mes y se redondea a 8 dígitos a menos que `roundOff=false`.

Ejemplos:

```sql
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Desde: 1.5.0

#### next_day

`next_day(start_date, day_of_week)`:: Devuelve la primera fecha posterior a la `start_date` y con el nombre indicado.

Ejemplo:

```sql
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Desde: 1.5.0

#### trimestre

`quarter(date)`:: Devuelve el trimestre del año para la fecha, en el rango de 1 a 4.

Ejemplo:

```sql
> SELECT quarter('2016-08-31');
 3
```

Desde: 1.5.0

#### segundo

`second(timestamp)`:: Devuelve el segundo componente de la cadena/marca de tiempo.

Ejemplo:

```sql
> SELECT second('2009-07-30 12:58:59');
 59
```

Desde: 1.5.0

#### to_date

`to_date(date_str[, fmt])`:: Analiza la `date_str` expresión con la `fmt` expresión a una fecha. Devuelve nulo con entrada no válida. De forma predeterminada, sigue las reglas de conversión a una fecha si `fmt` se omite.

Ejemplos:

```sql
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Desde: 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`:: Analiza la `timestamp` expresión con la `fmt` expresión a una marca de tiempo. Devuelve nulo con entrada no válida. De forma predeterminada, sigue las reglas de conversión a una marca de tiempo si se omite `fmt` .

Ejemplos:

```sql
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Desde: 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`:: Devuelve la marca de tiempo UNIX de un tiempo determinado.

Ejemplo:

```sql
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Desde: 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`:: Interpreta una marca de tiempo como &#39;2017-07-14 02:40:00.0&#39; como una hora en el huso horario determinado y la procesa como una marca de tiempo en UTC. Por ejemplo, &#39;GMT+1&#39; daría como resultado &#39;2017-07-14 01:40:00.0&#39;.

Ejemplo:

```sql
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Desde: 1.5.0

#### trunc

`trunc(date, fmt)`:: Devuelve la fecha con la parte de tiempo del día truncada a la unidad especificada por el modelo de formato `fmt`. `fmt` es uno de [&quot;año&quot;, &quot;aaaa&quot;, &quot;aa&quot;, &quot;mon&quot;, &quot;mes&quot;, &quot;mm&quot;]

Ejemplos:

```sql
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Desde: 1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`:: Devuelve la marca de tiempo UNIX del tiempo actual o especificado.

Ejemplos:

```sql
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Desde: 1.5.0

#### día laborable

`weekday(date)`:: Devuelve el día de la semana para fecha/marca de hora (0 = lunes, 1 = martes, ..., 6 = domingo).

Ejemplo:

```sql
> SELECT weekday('2009-07-30');
 3
```

Desde: 2.4.0

#### week_of_year

`weekofyear(date)`:: Devuelve la semana del año de la fecha dada. Una semana se considera inicio en un lunes y la semana 1 es la primera semana con >3 días.

Ejemplo:

```sql
> SELECT weekofyear('2008-02-20');
 8
```

Desde: 1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`:: When `expr1` = true, devuelve `expr2`; else when `expr3` = true, devuelve `expr4`; else devuelve `expr5`.

Argumentos:

- `expr1`, `expr3`: Las expresiones de condición de rama deben ser de tipo booleano.
- `expr2`, `expr4`, `expr5`: Las expresiones de valor de rama y la expresión de valor de else deben ser del mismo tipo o coercitivas a un tipo común.

Ejemplos:

```sql
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### año

`year(date)`:: Devuelve el componente de año de la marca de fecha y hora.

Ejemplo:

```sql
> SELECT year('2016-07-30');
 2016
```

Desde: 1.5.0

### Funciones acumuladas {#aggregate-functions}

#### aprox_count_different

`approx_count_distinct(expr[, relativeSD])`:: Devuelve la cardinalidad estimada por HyperLogLog++. `relativeSD` define el error máximo de estimación permitido.

### Matrices {#arrays}

#### array

`array(expr, ...)`:: Devuelve una matriz con los elementos dados.

Ejemplo:

```sql
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`:: Devuelve true si la matriz contiene el valor.

Ejemplo:

```sql
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_different

`array_distinct(array)`:: Quita los valores de duplicado de la matriz.

Ejemplo:

```sql
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Desde: 2.4.0

#### array_exclude

`array_except(array1, array2)`:: Devuelve una matriz de los elementos en `array1` pero no en `array2`, sin duplicados.

Ejemplo:

```sql
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Desde: 2.4.0

#### array_intersect

`array_intersect(array1, array2)`:: Devuelve una matriz de los elementos en la intersección de `array1` y `array2`, sin duplicados.

Ejemplo:

```sql
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Desde: 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`:: Concatena los elementos de una matriz determinada mediante el delimitador y una cadena opcional para reemplazar los valores NULL. Si no se establece ningún valor para `nullReplacement`, se filtra cualquier valor nulo.

Ejemplos:

```sql
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Desde: 2.4.0

#### array_max

`array_max(array)`:: Devuelve el valor máximo de la matriz. Se omiten los elementos nulos.

Ejemplo:

```sql
> SELECT array_max(array(1, 20, null, 3));
 20
```

Desde: 2.4.0

#### array_min

`array_min(array)`:: Devuelve el valor mínimo de la matriz. Se omiten los elementos nulos.

Ejemplo:

```sql
> SELECT array_min(array(1, 20, null, 3));
 1
```

Desde: 2.4.0

#### array_position

`array_position(array, element)`:: Devuelve el índice (basado en 1) del primer elemento de la matriz tanto como largo.

Ejemplo:

```sql
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Desde: 2.4.0

#### array_remove

`array_remove(array, element)`:: Elimine de la matriz todos los elementos iguales a elementos.

Ejemplo:

```sql
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Desde: 2.4.0

#### array_repeat

`array_repeat(element, count)`:: Devuelve la matriz que contiene tiempos de recuento de elementos.

Ejemplo:

```sql
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Desde: 2.4.0

#### array_sort

`array_sort(array)`:: Ordena la matriz de entrada en orden ascendente. Los elementos de la matriz de entrada deben poder pedirse. Los elementos nulos se colocan al final de la matriz devuelta.

Ejemplo:

```sql
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Desde: 2.4.0

#### array_unión

`array_union(array1, array2)`:: Devuelve una matriz de los elementos en la unión de `array1` y `array2`, sin duplicados.

Ejemplo:

```sql
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Desde: 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`:: Devuelve una matriz combinada de estructuras en la que la estructura N-th contiene todos los valores N-th de matrices de entrada.

Ejemplos:

```sql
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Desde: 2.4.0

#### element_at

`element_at(array, index)`:: Devuelve el elemento de matriz en un índice determinado (basado en 1). Si `index < 0`, accede a los elementos desde el último hasta el primero. Devuelve NULL si el índice supera la longitud de la matriz.

`element_at(map, key)`:: Devuelve el valor de una clave determinada o NULL si la clave no está contenida en el mapa

Ejemplos:

```sql
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Desde: 2.4.0

#### explosionar

`explode(expr)`:: Separa los elementos de la matriz `expr` en varias filas o los elementos de la asignación `expr` en varias filas y columnas.

Ejemplos:

```sql
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_exterior

`explode_outer(expr)`:: Separa los elementos de la matriz `expr` en varias filas o los elementos de la asignación `expr` en varias filas y columnas.

Ejemplo:

```sql
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`:: Devuelve el índice (basado en 1) de la cadena dada (`str`) en la lista delimitada por comas (`str_array`). Devuelve 0, si no se encontró la cadena o si la cadena dada (`str`) contiene una coma.

Ejemplo:

```sql
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### acoplar

`flatten(arrayOfArrays)`:: Transforma una matriz de matrices en una única matriz.

Ejemplo:

```sql
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Desde: 2.4.0

#### inline

`inline(expr)`:: Explota una matriz de estructuras en una tabla.

Ejemplo:

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inilne_exterior

`inline_outer(expr)`:: Explota una matriz de estructuras en una tabla.

Ejemplo:

```sql
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### posexplote

`posexplode(expr)`:: Separa los elementos de la matriz `expr` en varias filas con posiciones o los elementos de asignación `expr` en varias filas y columnas con posiciones.

Ejemplo:

```sql
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_exterior

`posexplode_outer(expr)`:: Separa los elementos de la matriz `expr` en varias filas con posiciones o los elementos de asignación `expr` en varias filas y columnas con posiciones.

Ejemplo:

```sql
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### invertir

`reverse(array)`:: Devuelve una cadena invertida o una matriz con orden inverso de elementos.

Ejemplos:

```sql
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Desde: 1.5.0

>[!NOTE]
>
>La lógica de aumento para matrices está disponible desde la versión 2.4.0.

#### barrido

`shuffle(array)`:: Devuelve una permutación aleatoria de la matriz dada.

Ejemplos:

```sql
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Desde: 2.4.0

>[!NOTE]
>
>no es determinística.

#### slice

`slice(x, start, length)`:: La matriz de subconjuntos x comienza a partir del inicio de índice (o a partir del final si el inicio es negativo) con la longitud especificada.

Ejemplos:

```sql
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Desde: 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`:: Ordena la matriz de entrada en orden ascendente o descendente según el orden natural de los elementos de la matriz. Los elementos nulos se colocan al principio de la matriz devuelta en orden ascendente o al final de la matriz devuelta en orden descendente.

Ejemplos:

```sql
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`:: Combina las dos matrices dadas, por elemento, en una única matriz mediante una función. Si una matriz es más corta, se anexan los valores nulos al final para que coincidan con la longitud de la matriz más larga, antes de aplicar la función.

Ejemplos:

```sql
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Desde: 2.4.0

### Funciones de conversión de tipos de datos {#datatype-casting}

#### bigint

`bigint(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `bigint`.

#### binario

`binary(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `binary`.

#### Booleano

`boolean(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `boolean`.

#### cast

`cast(expr AS type)`:: Transmite el valor `expr` al tipo de datos de destinatario `type`.

Ejemplo:

```sql
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `date`.

#### decimal

`decimal(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `decimal`.

#### doble

`double(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `double`.

#### float

`float(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `float`.

#### int

`int(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `int`.

#### map

`map(key0, value0, key1, value1, ...)`:: Crea un mapa con los pares de clave/valor determinados.

Ejemplo:

```sql
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### viruela

`smallint(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`:: Crea un mapa después de dividir el texto en pares clave/valor mediante delimitadores. Los delimitadores predeterminados son &#39;,&#39; para `pairDelim` y &#39;:&#39; para `keyValueDelim`.

Ejemplos:

```sql
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### string

`string(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `string`.

#### struct

`struct(col1, col2, col3, ...)`:: Crea una estructura con los valores de campo dados.

#### tinyint

`tinyint(expr)`:: Transmite el valor `expr` al tipo de datos de destinatario `tinyint`.

### Funciones de conversión y formato {#conversion}

#### ascii

`ascii(str)`:: Devuelve el valor numérico del primer carácter de `str`.

Ejemplos:

```sql
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`:: Convierte el argumento de un binario `bin` a una cadena base 64.

Ejemplo:

```sql
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`:: Devuelve la representación de cadena del valor largo `expr` representado en binario.

Ejemplos:

```sql
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`:: Devuelve la longitud de bits de los datos de cadena o el número de bits de los datos binarios.

Ejemplo:

```sql
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`:: Devuelve el carácter ASCII que tiene el equivalente binario a `expr`. Si n es mayor que 256, el resultado es equivalente a `chr(n % 256)`.

Ejemplo:

```sql
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`:: Devuelve la longitud de carácter de los datos de cadena o el número de bytes de los datos binarios. La longitud de los datos de cadena incluye los espacios finales. La longitud de los datos binarios incluye ceros binarios.

Ejemplos:

```sql
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`:: Devuelve la longitud de carácter de los datos de cadena o el número de bytes de los datos binarios. La longitud de los datos de cadena incluye los espacios finales. La longitud de los datos binarios incluye ceros binarios.

Ejemplos:

```sql
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`:: Devuelve el carácter ASCII que tiene el equivalente binario de expr. Si n es mayor que 256, el resultado es equivalente a `chr(n % 256)`

Ejemplo:

```sql
> SELECT chr(65);
 A
```

#### grados

`degrees(expr)`:: Convierte los radianes en grados.

Argumentos:
- `expr`:: Ángulo en radianes

Ejemplo:

```sql
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`:: Da formato al número `expr1` como &#39;#,###,##.##&#39;, redondeado a `expr2` decimales. Si `expr2` es 0, el resultado no tiene punto decimal ni parte fraccionada. `expr2` también acepta un formato especificado por el usuario. Esto está pensado para funcionar como el de MySQL `FORMAT`.

Ejemplos:

```sql
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`:: Devuelve un valor struct con el `jsonStr` y `schema`.

Ejemplos:

```sql
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Desde: 2.2.0

#### hash

`hash(expr1, expr2, ...)`:: Devuelve un valor hash de los argumentos.

Ejemplo:

```sql
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hex

`hex(expr)`:: Convierte `expr` a hexadecimal.

Ejemplos:

```sql
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`:: Devuelve `str` con la primera letra de cada palabra en mayúsculas. Todas las demás letras están en minúsculas. Las palabras están delimitadas por espacios en blanco.

Ejemplo:

```sql
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`:: Devuelve `str` con todos los caracteres cambiados a minúsculas.

Ejemplo:

```sql
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`:: Devuelve `str` con todos los caracteres cambiados a minúsculas.

Ejemplo:

```sql
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`:: Devuelve `str`, con `pad` un relleno a la izquierda con una longitud de `len`. Si `str` es mayor que `len`, el valor devuelto se acorta a `len` caracteres.

Ejemplos:

```sql
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)`:: Crea un mapa con los pares de clave/valor determinados.

Ejemplo:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_array

`map_from_arrays(keys, values)`:: Crea un mapa con un par de matrices de clave/valor dadas. Los elementos de las claves no pueden ser nulos.

Ejemplo:

```sql
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Desde: 2.4.0

#### map_from_Entries

`map_from_entries(arrayOfEntries)`:: Devuelve un mapa creado a partir de una matriz de entradas determinada.

Ejemplo:

```sql
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Desde: 2.4.0

#### md5

`md5(expr)`:: Devuelve una suma de comprobación MD5 de 128 bits como una cadena hexadecimal de `expr`.

Ejemplo:

```sql
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`:: Devuelve `str`, con `pad` el botón derecho añadido a una longitud de `len`. Si `str` es mayor que `len`, el valor devuelto se acorta a `len` caracteres.

Ejemplos:

```sql
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`:: Quita los caracteres de espacio al final de `str`.

`rtrim(trimStr, str)`:: Quita la cadena final, que contiene los caracteres de la cadena de recorte del `str`.

Argumentos:
- `str`:: Una expresión de cadena
- `trimStr`:: Caracteres de la cadena de corte que se van a recortar. El valor predeterminado es un espacio único

Ejemplos:

```sql
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`:: Devuelve un valor `sha1` hash como una cadena hexadecimal del `expr`.

Ejemplo:

```sql
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`:: Devuelve un valor `sha1` hash como una cadena hexadecimal del `expr`.

Ejemplo:

```sql
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`:: Devuelve una suma de comprobación de la familia SHA-2 como una cadena hexadecimal de `expr`. Se admiten SHA-224, SHA-256, SHA-384 y SHA-512. La longitud de bits de 0 equivale a 256.

Ejemplo:

```sql
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`:: Devuelve el código Soundex de la cadena.

Ejemplo:

```sql
> SELECT soundex('Miller');
 M460
```

#### pila

`stack(n, expr1, ..., exprk)`:: Separa `expr1`, ..., `exprk` en `n` filas.

Ejemplo:

```sql
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`:: Devuelve la subcadena de `str` esos inicios en `pos` y es de longitud `len`, o la fracción de matriz de bytes que inicio en `pos` y es de longitud `len`.

Ejemplos:

```sql
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### subcadena

`substring(str, pos[, len])`:: Devuelve la subcadena de `str` esos inicios en `pos` y es de longitud `len`, o la fracción de matriz de bytes que inicio en `pos` y es de longitud `len`.

Ejemplos:

```sql
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`:: Devuelve una cadena JSON con un valor de estructura determinado.

Ejemplos:

```sql
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Desde: 2.2.0

#### traducir

`translate(input, from, to)`:: Traduce la `input` cadena reemplazando los caracteres presentes en la `from` cadena por los caracteres correspondientes en la `to` cadena.

Ejemplo:

```sql
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`:: Quita los caracteres de espacio inicial y final de `str`.

`trim(BOTH trimStr FROM str)`:: Elimine los caracteres al inicio y al final `trimStr` de `str`.

`trim(LEADING trimStr FROM str)`:: Elimine los `trimStr` caracteres iniciales de `str`.

`trim(TRAILING trimStr FROM str)`:: Elimine los caracteres finales `trimStr` de `str`.

Argumentos:
- `str`:: Una expresión de cadena
- `trimStr`:: Los caracteres de la cadena de corte que se van a recortar; el valor predeterminado es un espacio único
- `BOTH`, `FROM`: Son palabras clave para especificar caracteres de cadena de recorte de ambos extremos de la cadena
- `LEADING`, `FROM`: Son palabras clave para especificar caracteres de cadena de recorte desde el extremo izquierdo de la cadena
- `TRAILING`, `FROM`: Son palabras clave para especificar caracteres de cadena de recorte desde el extremo derecho de la cadena

Ejemplos:

```sql
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### ucase

`ucase(str)`:: Devuelve `str` con todos los caracteres cambiados a mayúsculas.

Ejemplo:

```sql
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`:: Convierte el argumento de una cadena base 64 `str` a un binario.

Ejemplo:

```sql
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`:: Convierte hexadecimal `expr` en binario.

Ejemplo:

```sql
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`:: Devuelve `str` con todos los caracteres cambiados a mayúsculas.

Ejemplo:

```sql
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`:: Devuelve una cadena de identificador único universal (UUID). El valor se devuelve como una cadena canónica UUID de 36 caracteres.

Ejemplo:

```sql
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE]
>
>La función no es determinística.

### Evaluación de datos {#data-evaluation}

#### fusionarse

`coalesce(expr1, expr2, ...)`:: Devuelve el primer argumento no nulo si existe. En caso contrario, null.

Ejemplo:

```sql
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_lista

`collect_list(expr)`:: Recopila y devuelve una lista de elementos no únicos.

#### collect_set

`collect_set(expr)`:: Recopila y devuelve un conjunto de elementos únicos.

#### concat

`concat(col1, col2, ..., colN)`:: Devuelve la concatenación de col1, col2, ..., colN.

Ejemplos:

```sql
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE]
>
>`concat` lógica para matrices está disponible desde 2.4.0.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`:: Devuelve la concatenación de las cadenas separadas por `sep`.

Ejemplo:

```sql
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`:: Devuelve el número total de filas recuperadas, incluidas las filas que contienen null.

`count(expr[, expr...])`:: Devuelve el número de filas para las que todas las expresiones suministradas no son nulas.

`count(DISTINCT expr[, expr...])`:: Devuelve el número de filas para las que las expresiones suministradas son únicas y no nulas.

#### crc32

`crc32(expr)`:: Devuelve un valor de comprobación de redundancia cíclica del `expr` como un valor de detalle.

Ejemplo:

```sql
> SELECT crc32('Spark');
 1557323817
```

#### decode

`decode(bin, charset)`:: Descodifica el primer argumento usando el segundo conjunto de caracteres del argumento.

Ejemplo:

```sql
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`:: Devuelve la `n`entrada Nº, por ejemplo, devuelve `input2` cuando `n` es 2.

Ejemplo:

```sql
> SELECT elt(1, 'scala', 'java');
 scala
```

#### encode

`encode(str, charset)`:: Codifica el primer argumento con el segundo conjunto de caracteres de argumento.

Ejemplo:

```sql
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`:: Devuelve el primer valor de `expr` para un grupo de filas. Si `isIgnoreNull` es true, solo devuelve valores no nulos.

#### first_value

`first_value(expr[, isIgnoreNull])`:: Devuelve el primer valor de `expr` para un grupo de filas. Si `isIgnoreNull` es true, solo devuelve valores no nulos.

#### get_json_object

`get_json_object(json_txt, path)`:: Extrae un objeto json de `path`.

Ejemplo:

```sql
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### agrupar

<!-- was blank -->

#### group_id

<!-- was blank -->

#### instr

`instr(str, substr)`:: Devuelve el índice (basado en 1) de la primera incidencia de `substr` en `str`.

Ejemplo:

```sql
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`:: Devuelve un tupla como la función `get_json_object`, pero toma varios nombres. Todos los parámetros de entrada y tipos de columnas de salida son cadenas.

Ejemplo:

```sql
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### lag

`lag(input[, offset[, default]])`:: Devuelve el valor de `input` en la `offset`fila anterior a la fila actual de la ventana. El valor predeterminado de `offset` es 1 y el valor predeterminado de `default` es null. Si el valor de `input` en la `offset`fila es nulo, se devuelve nulo. Si no hay tal fila de desplazamiento (por ejemplo, cuando el desplazamiento es 1, la primera fila de la ventana no tiene ninguna fila anterior) y `default` se devuelve.

#### last

`last(expr[, isIgnoreNull])`:: Devuelve el último valor de `expr` para un grupo de filas. Si `isIgnoreNull` es true, solo devuelve valores no nulos.

#### last_value

`last_value(expr[, isIgnoreNull])`:: Devuelve el último valor de `expr` para un grupo de filas. Si `isIgnoreNull` es true, solo devuelve valores no nulos.

#### lead

`lead(input[, offset[, default]])`:: Devuelve el valor de `input` en la `offset`fila después de la fila actual en la ventana. El valor predeterminado de `offset` es 1 y el valor predeterminado de `default` es null. Si el valor de `input` en la `offset`fila es nulo, se devuelve nulo. Si no hay tal fila de desplazamiento (por ejemplo, cuando el desplazamiento es 1, la última fila de la ventana no tiene ninguna fila posterior) y `default` se devuelve.


#### left

`left(str, len)`:: Devuelve los caracteres más a la izquierda `len` (`len` puede ser de tipo cadena) de la cadena `str`. Si `len` es menor o igual que 0, el resultado es una cadena vacía.

Ejemplo:

```sql
> SELECT left('Spark SQL', 3);
 Spa
```

#### length

`length(expr)`:: Devuelve la longitud de carácter de los datos de cadena o el número de bytes de los datos binarios. La longitud de los datos de cadena incluye los espacios finales. La longitud de los datos binarios incluye ceros binarios.

Ejemplos:

```sql
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### localizar

`locate(substr, str[, pos])`:: Devuelve la posición de la primera incidencia de `substr` en `str` después de la posición `pos`. El valor dado `pos` y devuelto están basados en 1.

Ejemplos:

```sql
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`:: Devuelve la unión de todos los mapas dados.

Ejemplo:

```sql
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Desde: 2.4.0

#### map_keys

`map_keys(map)`:: Devuelve una matriz sin ordenar que contiene las claves del mapa.

Ejemplo:

```sql
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`:: Devuelve una matriz sin ordenar que contiene los valores del mapa.

Ejemplo:

```sql
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`:: Divide las filas de cada partición de ventana en `n` bloques de 1 a `n`.

#### nullif

`nullif(expr1, expr2)`:: Devuelve null si `expr1` es igual a `expr2`, o `expr1` de otro modo.

Ejemplo:

```sql
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`:: Devuelve `expr2` si `expr1` es nulo o `expr1` no.

Ejemplo:

```sql
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`:: Devuelve `expr2` si `expr1` no es nulo o `expr3` no lo es.

Ejemplo:

```sql
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`:: Extrae una parte de una dirección URL.

Ejemplos:

```sql
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`:: Devuelve la posición de la primera incidencia de `substr` en `str` después de la posición `pos`. El valor dado `pos` y devuelto están basados en 1.

Ejemplos:

```sql
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### clasificación

`rank()`:: Calcula la clasificación de un valor en un grupo de valores. El resultado es uno más el número de filas que preceden o son iguales a la fila actual en el orden de la partición. Los valores producen huecos en la secuencia.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`:: Extrae un grupo que coincide con `regexp`.

Ejemplo:

```sql
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`:: Reemplaza todas las subcadenas de `str` que coincidan `regexp` con `rep`.

Ejemplo:

```sql
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### repetir

`repeat(str, n)`:: Devuelve la cadena que repite el valor de cadena dado n veces.

Ejemplo:

```sql
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`:: Reemplaza todas las incidencias de `search` por `replace`.

Argumentos:
- `str`:: Una expresión de cadena
- `search`:: Una expresión de cadena. Si no `search` se encuentra en `str`, `str` se devuelve sin cambios.
- `replace`:: Una expresión de cadena. Si no `replace` se especifica o es una cadena vacía, nada reemplaza a la cadena que se elimina de `str`.

Ejemplo:

```sql
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### rollup

<!-- was blank -->

#### row_number

`row_number()`:: Asigna un número único y secuencial a cada fila, empezando por uno, según el orden de las filas dentro de la partición de ventana.

#### esquema_de_json

`schema_of_json(json[, options])`:: Devuelve el esquema en formato DDL de la cadena JSON.

Ejemplo:

```sql
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Desde: 2.4.0

#### oraciones

`sentences(str[, lang, country])`:: Se divide `str` en una matriz de palabras.

Ejemplo:

```sql
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### secuencia

`sequence(start, stop, step)`:: Genera una matriz de elementos desde el inicio hasta la parada (incluido), que se incrementa por pasos. El tipo de los elementos devueltos es el mismo que el tipo de expresiones de argumento.

Los tipos admitidos son: byte, short, integer, long, date, timestamp.

Las `start` expresiones y `stop` deben resolverse en el mismo tipo. Si `start` y `stop` las expresiones se resuelven en el tipo &#39;date&#39; o &#39;timestamp&#39;, la `step` expresión debe resolverse en el tipo &#39;range&#39;; de lo contrario, se resuelve en el mismo tipo que las `start` expresiones y `stop` .

Argumentos:
- `start`:: Una expresión. El inicio del rango.
- `stop`:: Una expresión. El final del intervalo (incluido).
- `step`:: Una expresión opcional. Paso del rango. De forma predeterminada `step` es 1 si `start` es menor o igual que `stop`; en caso contrario, -1. Para las secuencias temporales es 1 día y -1 día respectivamente. Si `start` es bueno que `stop`, el `step` valor debe ser negativo y viceversa.

Ejemplos:

```sql
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Desde: 2.4.0

#### desplazar a la izquierda

`shiftleft(base, expr)`:: Desplazamiento a la izquierda en modo bit.

Ejemplo:

```sql
> SELECT shiftleft(2, 1);
 4
```

#### desplazar hacia abajo

`shiftright(base, expr)`:: Desplazamiento a la derecha en modo bit (con signo).

Ejemplo:

```sql
> SELECT shiftright(4, 1);
 2
```

#### shift trightunsigned

`shiftrightunsigned(base, expr)`:: Desplazamiento a la derecha en modo bit sin signo.

Ejemplo:

```sql
> SELECT shiftrightunsigned(4, 1);
 2
```

#### size

`size(expr)`:: Devuelve el tamaño de una matriz o un mapa. La función devuelve -1 si su entrada es nula y `spark.sql.legacy.sizeOfNull` se establece en true. Si `spark.sql.legacy.sizeOfNull` se establece en false, la función devuelve null para la entrada null. By default, the `spark.sql.legacy.sizeOfNull` parameter is set to true.

Ejemplos:

```sql
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### espacio

`space(n)`:: Devuelve una cadena formada por `n` espacios.

Ejemplo:

```sql
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)`:: Divide `str` las incidencias que coinciden `regex`.

Ejemplo:

```sql
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`:: Devuelve la subcadena desde `str` antes de `count` que aparezca el delimitador `delim`. Si `count` es positivo, se devuelve todo lo que se encuentra a la izquierda del delimitador final (contando desde la izquierda). Si `count` es negativo, se devuelve todo a la derecha del delimitador final (contando desde la derecha). La función `substring_index` realiza una coincidencia que distingue entre mayúsculas y minúsculas al buscar `delim`.

Ejemplo:

```sql
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### window

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`:: Devuelve una matriz de cadenas de valores dentro de los nodos de xml que coinciden con la expresión XPath.

Ejemplo:

```sql
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_doble

`xpath_double(xml, xpath)`:: Devuelve un valor de doble, el valor cero si no se encuentra ninguna coincidencia o NaN si se encuentra una coincidencia pero el valor no es numérico.

Ejemplo:

```sql
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`:: Devuelve un valor flotante, el valor cero si no se encuentra ninguna coincidencia o NaN si se encuentra una coincidencia pero el valor no es numérico.

Ejemplo:

```sql
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`:: Devuelve un valor entero, o el valor cero si no se encuentra ninguna coincidencia, o bien se encuentra una coincidencia pero el valor no es numérico.

Ejemplo:

```sql
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`:: Devuelve un valor entero largo o el valor cero si no se encuentra ninguna coincidencia, o bien se encuentra una coincidencia pero el valor no es numérico.

Ejemplo:

```sql
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`:: Devuelve un valor de doble, el valor cero si no se encuentra ninguna coincidencia o NaN si se encuentra una coincidencia pero el valor no es numérico.

Ejemplo:

```sql
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`:: Devuelve un valor entero corto, o el valor cero si no se encuentra ninguna coincidencia, o bien se encuentra una coincidencia pero el valor no es numérico.

Ejemplo:

```sql
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`:: Devuelve el contenido de texto del primer nodo xml que coincide con la expresión XPath.

Ejemplo:

```sql
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Información actual {#current-information}

#### current_database

`current_database()`:: Devuelve la base de datos actual.

Ejemplo:

```sql
> SELECT current_database();
 default
```

#### current_date

`current_date()`:: Devuelve la fecha actual en el inicio de la evaluación de consultas.

Desde: 1.5.0

#### current_timestamp

`current_timestamp()`:: Devuelve la marca de tiempo actual en el inicio de la evaluación de consultas.

Desde: 1.5.0

#### now

`now()`:: Devuelve la marca de tiempo actual en el inicio de la evaluación de consultas.

Desde: 1.5.0

### Funciones de orden superior {#higher-order}

#### transformar

`transform(array, lambdaExpression): array`

Transforme los elementos de una matriz mediante la función .

Si hay dos argumentos para la función lambda, el segundo argumento significa el índice del elemento.

Ejemplo:

```sql
> SELECT transform(array(1, 2, 3), x -> x + 1);
  [2,3,4]
> SELECT transform(array(1, 2, 3), (x, i) -> x + i);
  [1,3,5]
```


#### existe

`exists(array, lambdaExpression returning Boolean): Boolean`

Compruebe si un predicado contiene uno o varios elementos de la matriz.

Ejemplo:

```sql
> SELECT exists(array(1, 2, 3), x -> x % 2 == 0);
  true
```

#### filter

`filter(array, lambdaExpression returning Boolean): array`

Filtre la matriz de entrada utilizando el predicado determinado.

Ejemplo:

```sql
> SELECT filter(array(1, 2, 3), x -> x % 2 == 1);
 [1,3]
```


#### acumulado

`aggregate(array, <initial accumulator value>, lambdaExpression to accumulate the value): array`

Aplique un operador binario a un estado inicial y a todos los elementos de la matriz y lo reduzca a un solo estado. El estado final se convierte en el resultado final aplicando una función de finalización.

Ejemplo:

```sql
> SELECT aggregate(array(1, 2, 3), 0, (acc, x) -> acc + x);
  6
> SELECT aggregate(array(1, 2, 3), 0, (acc, x) -> acc + x, acc -> acc * 10);
  60
```
