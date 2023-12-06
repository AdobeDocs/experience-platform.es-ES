---
title: 'Ejemplo de función Lambda: recuperar registros similares'
description: Aprenda a identificar y recuperar registros similares o relacionados de uno o más conjuntos de datos en función de una métrica de similitud y un umbral de similitud. Este flujo de trabajo puede resaltar relaciones significativas o superposiciones entre conjuntos de datos dispares.
source-git-commit: 55af6c8de72e9b60eb9423dda568681e7c84245f
workflow-type: tm+mt
source-wordcount: '4011'
ht-degree: 3%

---

# Ejemplo de función Lambda: recuperar registros similares

Resuelva varios casos de uso comunes utilizando las funciones lambda de Data Distiller para identificar y recuperar registros similares o relacionados de uno o más conjuntos de datos. Puede utilizar esta guía para identificar productos de diferentes conjuntos de datos que tienen una similitud significativa en sus características o atributos. La metodología de este documento proporciona soluciones para: deduplicación de datos, vinculación de registros, sistemas de recomendación, recuperación de información y análisis de texto, entre otros.

En el documento se describe el proceso de implementación de una unión de similitud y, a continuación, se utilizan las funciones lambda de Data Distiller para calcular la similitud entre conjuntos de datos y filtrarlos en función de los atributos seleccionados. Se proporcionan fragmentos de código SQL y explicaciones para cada paso del proceso. El flujo de trabajo implementa las uniones de similitud mediante la medida de similitud de Jaccard y la tokenización mediante las funciones lambda de Data Distiller. A continuación, estos métodos se utilizan para identificar y recuperar registros similares o relacionados de uno o varios conjuntos de datos en función de una métrica de similitud. Las secciones clave del proceso incluyen las siguientes: [tokenización mediante funciones lambda](#data-transformation), el [combinación cruzada de elementos únicos](#cross-join-unique-elements), el [Cálculo de similitud de Jaccard](#compute-the-jaccard-similarity-measure), y el [filtrado basado en umbrales](#similarity-threshold-filter).

## Requisitos previos

Antes de continuar con este documento, debe estar familiarizado con los siguientes conceptos:

- A **unión por similitud** es una operación que identifica y recupera pares de registros de una o varias tablas basándose en una medida de similitud entre los registros. Los requisitos clave para una unión de similitud son los siguientes:
   - **Métrica de similitud**: una unión de similitud se basa en una métrica o medida de similitud predefinida. Estas métricas incluyen: similitud de Jaccard, similitud de coseno, distancia de edición, etc. La métrica depende de la naturaleza de los datos y del caso de uso. Esta métrica cuantifica la similitud o diferencia entre dos registros.
   - **Umbral**: se utiliza un umbral de similitud para determinar cuándo se considera que los dos registros son lo suficientemente similares como para incluirse en el resultado de la unión. Los registros con una puntuación de similitud por encima del umbral se consideran coincidencias.
- El **Similitud de Jaccard** index, o medida de similitud de Jaccard, es una estadística utilizada para medir la similitud y diversidad de los conjuntos de muestras. Se define como el tamaño de la intersección dividido por el tamaño de la unión de los conjuntos de muestras. La medición de similitud de Jaccard varía de cero a uno. Una similitud de Jaccard de cero indica que no hay similitud entre los conjuntos, y una similitud de Jaccard de uno indica que los conjuntos son idénticos.
  ![Diagrama de Venn para ilustrar la medición de similitud de Jaccard.](../images/use-cases/jaccard-similarity.png)
- **Funciones lambda** en Data Distiller son funciones en línea anónimas que se pueden definir y utilizar dentro de instrucciones SQL. Se utilizan con frecuencia con funciones de orden superior debido a su capacidad para crear funciones concisas y sobre la marcha que se pueden pasar como datos. Las funciones lambda suelen emplearse con funciones de orden superior como `transform`, `filter`, y `array_sort`. Las funciones lambda son especialmente útiles en situaciones en las que no es necesario definir una función completa y se puede utilizar una función breve y única en línea.

## Introducción

El SKU de Data Distiller es necesario para realizar las funciones lambda en los datos de Adobe Experience Platform. Si no tiene el SKU de Distiller de datos, póngase en contacto con el representante del servicio de atención al cliente de Adobe para obtener más información.

## Establecer similitud {#establish-similarity}

Este caso de uso requiere una medida de similitud entre cadenas de texto que se puede utilizar más adelante para establecer un umbral de filtrado. En este ejemplo, los productos de los conjuntos A y B representan las palabras de dos documentos.

La medida de similitud de Jaccard se puede aplicar a una amplia gama de tipos de datos, incluidos datos de texto, datos categóricos y datos binarios. También es adecuado para el procesamiento en tiempo real o por lotes, ya que puede ser computacionalmente eficiente para calcular conjuntos de datos grandes.

Los conjuntos de productos A y B contienen los datos de prueba para este flujo de trabajo.

- Conjunto de productos A: `{iPhone, iPad, iWatch, iPad Mini}`
- Conjunto de productos B: `{iPhone, iPad, Macbook Pro}`

Para calcular la similitud de Jaccard entre los conjuntos de productos A y B, busque primero la variable **intersección** (elementos comunes) de los conjuntos de productos. En este caso, `{iPhone, iPad}`. A continuación, busque la **unión** (todos los elementos únicos) de ambos conjuntos de productos. En este ejemplo, `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Finalmente, utilice la fórmula de similitud de Jaccard: `J(A,B) = A∪B / A∩B` para calcular la similitud.

J = distancia Jaccard A = juego 1 B = juego 2

La similitud de Jaccard entre los conjuntos de productos A y B es de 0,4. Esto indica un grado moderado de similitud entre las palabras utilizadas en los dos documentos. Esta similitud entre los dos conjuntos define las columnas de la unión de similitud. Estas columnas representan fragmentos de información o características asociadas con los datos, que se almacenan en una tabla y se utilizan para realizar cálculos de similitud.

### Cálculo de Jaccard por pares con similitud de cadena {#pairwise-similarity}

Para comparar con mayor precisión las similitudes entre cadenas, se debe calcular la similitud entre pares. La similitud por pares divide los objetos altamente dimensionales en objetos dimensionales más pequeños para la comparación y el análisis. Para ello, una cadena de texto se divide en partes o unidades más pequeñas (tokens). Pueden ser letras individuales, grupos de letras (como sílabas) o palabras completas. La similitud se calcula para cada par de tokens entre cada elemento del conjunto A y cada elemento del conjunto B. Esta tokenización proporciona una base para comparaciones, relaciones y perspectivas analíticas y computacionales que se extraerán de los datos.

Para el cálculo de similitud por pares, este ejemplo utiliza bi-gramas de caracteres (dos tokens de caracteres) para comparar una coincidencia de similitud entre las cadenas de texto de los productos de los conjuntos A y B. Un bi-grama es una secuencia consecutiva de dos elementos o elementos en una secuencia o texto determinados. Puede generalizar esto a n-gramas.

En este ejemplo se supone que el caso no importa y que no se deben contabilizar los espacios. Según estos criterios, el conjunto A y el conjunto B tienen los siguientes bi-gramas:

Conjunto de productos A bi-gramos:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- iWatch (5): &quot;iw&quot;, &quot;wa&quot;, &quot;at&quot;, &quot;tc&quot;, &quot;ch&quot;
- iPad Mini (7): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;, &quot;dm&quot;, &quot;mi&quot;, &quot;in&quot;, &quot;ni&quot;

Conjunto de productos B bi-gramos:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- Macbook Pro (9): &quot;Ma&quot;, &quot;ac&quot;, &quot;cb&quot;, &quot;bo&quot;, &quot;oo&quot;, &quot;ok&quot;, &quot;kp&quot;, &quot;pr&quot;, &quot;ro&quot;

A continuación, calcule el coeficiente de similitud de Jaccard para cada par:

|                   | iPhone (Conjunto B) | iPad (Conjunto B) | Macbook Pro (Juego B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (Juego A) | (Intersección: 5, Unión: 5) = 5 / 5 = 1 | (Intersección: 1, Unión: 7) =1 / 7 ≈ 0,14 | (Intersección: 0, Unión: 14) = 0 / 14 = 0 |
| iPad (Juego A) | (Intersección: 1, Unión: 7) = 1 / 7 ≈ 0,14 | (Intersección: 3, Unión: 3) = 3 / 3 = 1 | (Intersección: 0, Unión: 12) = 0 / 12 = 0 |
| iWatch (Juego A) | (Intersección: 0, Unión: 8) = 0 / 8 = 0 | (Intersección: 0, Unión: 8) = 0 / 8 = 0 | (Intersección: 0, Unión: 8) = 0 / 8 =0 |
| iPad Mini (Juego A) | (Intersección: 1, Unión: 11) = 1 / 11 ≈ 0,09 | (Intersección: 3, Unión: 7) = 3 / 7 ≈ 0,43 | (Intersección: 0, Unión: 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Creación de los datos de prueba con SQL {#create-test-data}

Para crear manualmente una tabla de prueba para los conjuntos de productos, utilice la instrucción SQL CREATE TABLE.

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

Las siguientes descripciones proporcionan un desglose del bloque de código SQL anterior:

- Línea 1: `CREATE TEMP TABLE featurevector1 AS`: Esta instrucción crea una tabla temporal denominada `featurevector1`. Las tablas temporales solo suelen ser accesibles dentro de la sesión actual y se sueltan automáticamente al final de la sesión.
- Líneas 1 y 2: `SELECT * FROM (...)`: Esta parte del código es una subconsulta utilizada para generar los datos insertados en el `featurevector1` tabla.
Dentro de la subconsulta, varias `SELECT` Las instrucciones se combinan utilizando `UNION ALL` comando. Cada `SELECT` genera una fila de datos con los valores especificados para `ProductName` columna.
- Línea 3: `SELECT 'iPad' AS ProductName`: Esto genera una fila con el valor `iPad` en el `ProductName` columna.
- Línea 5: `SELECT 'iPhone'`: Esto genera una fila con el valor `iPhone` en el `ProductName` columna.

La instrucción SQL crea una tabla como se muestra a continuación:

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Para crear el segundo vector de función, utilice la siguiente instrucción SQL:

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## Transformaciones de datos {#data-transformation}

En este ejemplo, se deben realizar varias acciones para comparar los conjuntos con precisión. En primer lugar, los espacios en blanco se eliminan de los vectores de funciones, ya que se supone que no contribuyen a la medida de similitud. A continuación, los duplicados presentes en el vector de funciones se eliminan a medida que desperdician el procesamiento computacional. A continuación, se extraen tokens de dos caracteres (bi-gramos) de los vectores de funciones. En este ejemplo, se supone que se superponen.

>[!NOTE]
>
>A título ilustrativo, las columnas procesadas se añaden junto al vector de función para cada uno de los pasos.

Las siguientes secciones ilustran las transformaciones de datos previas, como la deduplicación, la eliminación de espacios en blanco y la conversión en minúsculas antes de iniciar el proceso de tokenización.

### Anulación de duplicación {#deduplication}

A continuación, utilice el `DISTINCT` para eliminar duplicados. No hay duplicados en este ejemplo, pero es un paso importante para mejorar la precisión de cualquier comparación. A continuación se muestra el SQL necesario:

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Eliminación de espacios en blanco {#whitespace-removal}

En la siguiente instrucción SQL, los espacios en blanco se quitan de los vectores de características. El `replace(ProductName, ' ', '') AS featurevector1_nospaces` parte de la consulta toma la `ProductName` de la columna `featurevector1` y utiliza el `replace()` función. El `REPLACE` reemplaza todas las ocurrencias de un espacio (&#39; &#39;) con una cadena vacía (&#39;&#39;). Esto elimina efectivamente todos los espacios del `ProductName` valores. El resultado se alias como `featurevector1_nospaces`.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

Los resultados se muestran en la tabla siguiente:

|   | featurevector1_distinct | featurevector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

La instrucción SQL y sus resultados en el segundo vector de características se ven a continuación:

+++Seleccionar para expandir

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

Los resultados se muestran de la siguiente manera:

|   | featurevector2_distinct | featurevector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Convertir a minúsculas {#lowercase-conversion}

A continuación, SQL se mejora para convertir los nombres de producto a minúsculas y eliminar cualquier espacio en blanco. La función inferior (`lower(...)`) se aplica al resultado de `replace()` función. La función lower convierte todos los caracteres del objeto modificado `ProductName` valores en minúsculas. Esto garantiza que los valores estén en minúsculas independientemente de sus mayúsculas y minúsculas originales.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

El resultado de esta instrucción es:

|   | featurevector1_distinct | featurevector1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

La instrucción SQL y sus resultados en el segundo vector de características se ven a continuación:

+++Seleccionar para expandir

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

Los resultados se muestran de la siguiente manera:

|   | featurevector2_distinct | featurevector2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### Extraer tokens mediante SQL {#tokenization}

El siguiente paso es la tokenización o división de texto. La tokenización es el proceso de tomar texto y dividirlo en términos individuales. Normalmente, esto implica dividir frases en palabras. En este ejemplo, las cadenas se desglosan en bi-gramas (y n-gramas de orden superior) extrayendo tokens mediante funciones SQL como `regexp_extract_all`. Se deben generar bi-gramas superpuestos para una tokenización eficaz.

SQL se ha mejorado aún más para utilizar `regexp_extract_all`. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` Esta parte de la consulta procesa aún más los cambios `ProductName` valores creados en el paso anterior. Utiliza el `regexp_extract_all()` para extraer todas las subcadenas no superpuestas de uno a dos caracteres de las minúsculas y modificadas `ProductName` valores. El `.{2}` el patrón de expresión regular coincide con subcadenas de dos caracteres de longitud. El `regexp_extract_all(..., '.{2}', 0)` A continuación, parte de la función extrae todas las subcadenas coincidentes del texto de entrada.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

|   | featurevector1_distinct | featurevector1_transform | tokens |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;, &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Para mejorar aún más la precisión, SQL debe utilizarse para crear tokens superpuestos. Por ejemplo, a la cadena &quot;iPad&quot; de arriba le falta el token &quot;pa&quot;. Para solucionarlo, cambie el operador lookahead (utilizando `substring`) por un paso y generar los bi-gramas.

Similar al paso anterior, `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` extrae secuencias de dos caracteres del nombre de producto modificado, pero comienza a partir del segundo carácter con la variable `substring` para crear tokens superpuestos. A continuación, en las líneas 3-7 (`array_union(...) AS tokens`), el `array_union()` Esta función combina las matrices de secuencias de dos caracteres obtenidas mediante las dos extracciones de expresiones regulares. Esto garantiza que el resultado contenga tokens únicos de secuencias no superpuestas y superpuestas.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

|   | featurevector1_distinct | featurevector1_transform | tokens |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;,&quot;pa&quot;,&quot;dm&quot;,&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;,&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;,&quot;ch&quot;,&quot;wa&quot;,&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;,&quot;ph&quot;,&quot;on&quot;} |

{style="table-layout:auto"}

+++

Sin embargo, el uso de `substring` como solución al problema tiene limitaciones. Si tuviera que crear tokens a partir del texto basados en tri-gramas (tres caracteres), se requeriría el uso de dos `substrings` para mirar hacia adelante dos veces para conseguir los turnos necesarios. Para hacer 10 gramos, necesitarías nueve `substring` expresiones. Esto haría que el código se inflara y se volviera insostenible. El uso de expresiones regulares simples no es adecuado. Se necesita un nuevo enfoque.

### Ajustar para la longitud del nombre del producto {#length-adjustment}

El SQLl puede mejorarse con las funciones de secuencia y longitud. En el ejemplo siguiente, `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` genera una secuencia de números desde uno hasta la longitud del nombre del producto modificado menos tres. Por ejemplo, si el nombre del producto modificado es &quot;ipadmini&quot; con una longitud de ocho caracteres, genera números del uno al cinco (ocho-tres).

La instrucción siguiente extrae nombres de productos únicos y luego desglosa cada nombre en secuencias de caracteres (tokens) de cuatro longitudes de caracteres, excluyendo espacios y presentándolos como dos columnas. Una columna muestra los nombres de producto únicos y la otra columna muestra los tokens generados.

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

|   | featurevector1_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;,&quot;padm&quot;,&quot;admin&quot;,&quot;admin&quot;,&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;iwat&quot;,&quot;watch&quot;,&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;,&quot;phon&quot;,&quot;phone&quot;} |

{style="table-layout:auto"}

+++

### Asegúrese de establecer la longitud del token

Se pueden añadir condiciones adicionales a la instrucción para garantizar que las secuencias generadas tengan una longitud específica. La siguiente instrucción SQL amplía la lógica de generación de tokens al realizar la variable `transform` La función es más compleja. La instrucción utiliza el `filter` función dentro de `transform` para asegurarse de que las secuencias generadas tengan una longitud de seis caracteres. Gestiona los casos en los que esto no es posible asignando valores NULL a esas posiciones.

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

|   | featurevector1_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;,&quot;padmin&quot;,&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## Explorar soluciones mediante las funciones lambda de Data Distiller {#lambda-function-solutions}

Las funciones lambda son construcciones potentes que permiten implementar &quot;programaciones&quot; como la sintaxis en Data Distiller. Se pueden utilizar para repetir una función en varios valores de una matriz.

En el contexto de Data Distiller, las funciones lambda son ideales para crear n-gramas e iterar secuencias de caracteres.

El `reduce` función, especialmente cuando se utiliza dentro de secuencias generadas por `transform`, proporciona una forma de derivar valores acumulativos o acumulados, que pueden ser fundamentales en varios procesos analíticos y de planificación.

Por ejemplo, en la instrucción SQL siguiente, la variable `reduce()` función agrega elementos en una matriz utilizando un agregador personalizado. Simula un bucle for en **crear las sumas acumulativas de todos los enteros** de uno a cinco. `1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`.

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Lambda function to add numbers
    )
) AS sum_result;
```

A continuación se muestra un análisis de la instrucción SQL:

- Línea 1: `transform` aplica la función `x -> reduce` en cada elemento generado en la secuencia.
- Línea 2: `sequence(1, 5)` genera una secuencia de números del uno al cinco.
- Línea 3: `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` realiza una operación de reducción para cada elemento x de la secuencia (de 1 a 5).
   - El `reduce` La función toma un valor de acumulador inicial de 0, una secuencia de uno al valor actual de `x`, y una función lambda `(acc, y) -> acc + y` para añadir los números.
   - La función lambda `acc + y` acumula la suma sumando el valor actual `y` al acumulador `acc`.
- Línea 8: `AS sum_result` cambia el nombre de la columna resultante a sum_result.

En resumen, esta función lambda toma dos parámetros (`acc` y `y`) y define la operación que se va a realizar, que en este caso es añadir `y` al acumulador `acc`. Esta función lambda se ejecuta para cada elemento de la secuencia durante el proceso de reducción.

El resultado de esta instrucción es una sola columna (`sum_result`) que contiene las sumas acumuladas de números del uno al cinco.

### El valor de las funciones lambda {#value-of-lambda-functions}

En esta sección se analiza una versión reducida de una instrucción SQL de tres gramos para comprender mejor el valor de las funciones lambda en Data Distiller y crear n-gramos de forma más eficaz.

La declaración siguiente opera en el `ProductName` dentro de la columna `featurevector1` tabla. Produce un conjunto de subcadenas de tres caracteres derivadas de los nombres de productos modificados dentro de la tabla, utilizando posiciones obtenidas de la secuencia generada.

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

A continuación se muestra un análisis de la instrucción SQL:

- Línea 2: `transform` aplica una función lambda a cada entero de la secuencia.
- Línea 3: `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` genera una secuencia de enteros a partir de `1` a la longitud del nombre del producto modificado menos dos.
   - `length(lower(replace(ProductName, ' ', '')))` calcula la longitud de la `ProductName` después de convertirlo en minúsculas y eliminar espacios.
   - `- 2` resta dos de la longitud para garantizar que la secuencia genera posiciones iniciales válidas para subcadenas de 3 caracteres. Restar 2 garantiza que tiene suficientes caracteres después de cada posición inicial para extraer una subcadena de 3 caracteres. La función de subcadena aquí funciona como un operador de búsqueda anticipada.
- Línea 4: `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` es una función lambda que funciona en cada entero `i` en la secuencia generada.
   - El `substring(...)` extrae una subcadena de 3 caracteres de la función `ProductName` columna.
   - Antes de extraer la subcadena, `lower(replace(ProductName, ' ', ''))` convierte el `ProductName` a minúsculas y elimina espacios para garantizar la coherencia.

El resultado es una lista de subcadenas de tres caracteres de longitud, extraídas de los nombres de productos modificados, basándose en las posiciones especificadas en la secuencia.

## Filtrado de los resultados {#filter-results}

El `filter` función, con subsiguiente [transformaciones de datos](#data-transformation), permite una extracción más refinada y precisa de la información relevante de los datos de texto. Esto le permite obtener perspectivas, mejorar la calidad de los datos y facilitar mejores procesos de toma de decisiones.

El `filter` en la siguiente instrucción SQL sirve para refinar y limitar la secuencia de posiciones dentro de la cadena desde la que se extraen las subcadenas utilizando la función de transformación posterior.

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

El `filter` La función genera una secuencia de posiciones de inicio válidas dentro de la variable modificada `ProductName` y extrae subcadenas de una longitud específica. Solo se permiten las posiciones de inicio que permiten la extracción de una subcadena de siete caracteres.

La condición `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` garantiza que la posición inicial `i` plus `6` (la longitud de la subcadena de siete caracteres deseada menos una) no supera la longitud de la cadena modificada `ProductName`.

El `CASE` se utiliza para incluir o excluir condicionalmente subcadenas en función de su longitud. Solo se incluyen subcadenas de siete caracteres; otras se sustituyen por NULL. Estas subcadenas las utiliza la variable `transform` para crear una secuencia de subcadenas a partir de la variable `ProductName` en la columna `featurevector1` tabla.

>[!TIP]
>
>Puede usar el complemento [plantillas con parámetros](../ui/parameterized-queries.md) función para reutilizar y abstraer la lógica dentro de las consultas. Por ejemplo, cuando crea funciones de utilidad de uso general (como la que se muestra arriba para tokenizar cadenas), puede utilizar plantillas parametrizadas de Data Distiller donde el número de caracteres sería un parámetro.

## Calcular la unión cruzada de elementos únicos en dos vectores de funciones {#cross-join-unique-elements}

La identificación de las diferencias o discrepancias entre los dos conjuntos de datos en función de una transformación específica de los datos es un proceso común para mantener la precisión, mejorar la calidad y garantizar la coherencia entre los conjuntos de datos.

Esta instrucción SQL a continuación extrae los nombres de producto únicos que están presentes en `featurevector2` pero no en `featurevector1` después de aplicar las transformaciones.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Además de `EXCEPT`, también puede utilizar `UNION` y `INTERSECT` según su caso de uso. Además, puede experimentar con `ALL` o `DISTINCT` para ver la diferencia entre incluir todos los valores y devolver sólo los valores únicos de las columnas especificadas.

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

|   | lower(replace(NombreProducto, &#39; &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

A continuación, realice una combinación cruzada para combinar elementos de los dos vectores de funciones y crear pares de elementos para la comparación. El primer paso de este proceso es crear un vector tokenizado.

Un vector tokenizado es una representación estructurada de datos de texto en la que cada palabra, frase o unidad de significado (token) se convierte en un formato numérico. Esta conversión permite a los algoritmos de procesamiento de lenguaje natural comprender y analizar la información textual.

El SQL siguiente crea un vector tokenizado.

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>Si está utilizando [!DNL DbVisualizer]Después de crear o eliminar una tabla, actualice la conexión de base de datos para que se actualice la caché de metadatos de la tabla. Data Distiller no excluye las actualizaciones de metadatos.

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

|   | featurevector1_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 3 | reloj | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

A continuación, repita el proceso para `featurevector2`:

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

|   | featurevector2_distinct | tokens |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Con ambos vectores tokenizados completados, ahora puede crear la unión cruzada. Esto se ve en el siguiente SQL:

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

A continuación se muestra un resumen del SQL utilizado para crear la combinación cruzada:

- Línea 2: `A.featurevector1_distinct AS SetA_ProductNames` selecciona el `featurevector1_distinct` de la tabla `A` y le asigna un alias `SetA_ProductNames`. Esta sección de SQL da como resultado una lista de nombres de productos distintos del primer conjunto de datos.
- Línea 4: `A.tokens AS SetA_tokens1` selecciona el `tokens` de la tabla o subconsulta `A` y le asigna un alias `SetA_tokens1`. Esta sección de SQL da como resultado una lista de valores tokenizados asociados con los nombres de producto del primer conjunto de datos.
- Línea 8: La `CROSS JOIN` Esta operación combina todas las combinaciones posibles de filas de los dos conjuntos de datos. En otras palabras, vincula cada nombre de producto y sus tokens asociados de la primera tabla (`A`) con cada nombre de producto y sus tokens asociados de la segunda tabla (`B`). Esto da como resultado un producto cartesiano de los dos conjuntos de datos, donde cada fila de la salida representa una combinación del nombre de un producto y sus tokens asociados de ambos conjuntos de datos.

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 7 | reloj | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 8 | reloj | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 9 | reloj | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## Calcular la medida de similitud de Jaccard {#compute-the-jaccard-similarity-measure}

A continuación, calcule y utilice el coeficiente de similitud de Jaccard para realizar un análisis de similitud entre los dos conjuntos de nombres de productos comparando sus representaciones tokenizadas. La salida del script SQL siguiente proporciona lo siguiente: nombres de producto de ambos conjuntos, sus representaciones tokenizadas, recuentos de tokens únicos comunes y totales, y el coeficiente de similitud de Jaccard calculado para cada par de conjuntos de datos.


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

A continuación se muestra un resumen del SQL utilizado para calcular el coeficiente de similitud de Jaccard:

- Línea 6: `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` calcula el número de tokens comunes a ambos `SetA_tokens1` y `SetB_tokens2`. Este cálculo se obtiene calculando el tamaño de la intersección de las dos matrices de tokens.
- Línea 7: `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` calcula el número total de tokens únicos en ambos `SetA_tokens1` y `SetB_tokens2`. Esta línea calcula el tamaño de la unión de las dos matrices de tokens.
- Línea 8-10: `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` calcula la similitud de Jaccard entre los conjuntos de símbolos. Estas líneas dividen el tamaño de la intersección del token por el tamaño de la unión del token y redondean el resultado a dos decimales. El resultado es un valor entre cero y uno, donde uno indica similitud completa.

Los resultados se muestran en la tabla siguiente:

+++Seleccionar para expandir

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Similitud de Jaccard |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 7 | 0,43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 16 | 0,0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 11 | 0,09 |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 3 | 1.0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 12 | 0,0 |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 7 | 0,14 |
| 7 | reloj | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 0 | 8 | 0,0 |
| 8 | reloj | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 9 | reloj | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 0 | 10 | 0,0 |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 1 | 7 | 0,14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 5 | 5 | 1.0 |

{style="table-layout:auto"}

+++

## Filtrar resultados según el umbral de similitud de Jaccard {#similarity-threshold-filter}

Por último, filtre los resultados en función de un umbral predefinido para seleccionar solo aquellos pares que cumplan los criterios de similitud. La siguiente instrucción SQL filtra los productos con un coeficiente de similitud de Jaccard de al menos 0,4. Esto reduce los resultados a pares que muestran un grado sustancial de similitud.

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

Los resultados de esta consulta dan las columnas para la unión de similitud, como se ve a continuación:

+++Seleccionar para expandir

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++:

### Pasos siguientes {#next-steps}

Al leer este documento, ahora puede utilizar esta lógica para resaltar relaciones significativas o superposiciones entre conjuntos de datos dispares. La capacidad de identificar productos de diferentes conjuntos de datos que tienen una similitud significativa en sus características o atributos tiene numerosas aplicaciones reales. Esta lógica podría utilizarse para escenarios como la coincidencia de productos (para agrupar o recomendar productos similares a los clientes), la limpieza de datos (para mejorar la calidad de los datos) y el análisis de cestas de compras (para proporcionar perspectivas sobre el comportamiento de los clientes, las preferencias y las posibles oportunidades de ventas cruzadas).

Si aún no lo ha hecho, se recomienda leer el [Información general de canalización de funciones AI/ML](../data-distiller/ml-feature-pipelines/overview.md). Utilice esa descripción general para conocer cómo Data Distiller y su aprendizaje automático preferido pueden crear modelos de datos personalizados que admitan sus casos de uso de marketing con datos de Experience Platform.
