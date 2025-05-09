---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de iu;asignador;asignar;campos de asignación;funciones de asignación;
solution: Experience Platform
title: Funciones de asignación de preparación de datos
description: Este documento presenta las funciones de asignación utilizadas con la preparación de datos.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 2d640b282feb783694276c69366b1fccadddfd78
workflow-type: tm+mt
source-wordcount: '6028'
ht-degree: 2%

---

# Funciones de asignación de preparación de datos

Las funciones de preparación de datos se pueden utilizar para calcular y calcular valores basados en lo que se introduce en los campos de origen.

## Campos

Un nombre de campo puede ser cualquier identificador válido: una secuencia de longitud ilimitada de letras y dígitos Unicode que comience por una letra, el signo de dólar (`$`) o el carácter de subrayado (`_`). Los nombres de variables también distinguen entre mayúsculas y minúsculas.

Si el nombre de campo no sigue esta convención, el nombre de campo debe incluirse entre `${}`. Por lo tanto, si el nombre de campo es &quot;First Name&quot; o &quot;First.Name&quot;, el nombre debe incluirse entre `${First Name}` o `${First\.Name}`, respectivamente.

>[!TIP]
>
>Al interactuar con jerarquías, si un atributo secundario tiene un punto (`.`), debe utilizar una barra invertida (`\`) para omitir los caracteres especiales. Para obtener más información, lea la guía sobre [caracteres especiales de escape](home.md#escape-special-characters).

Si el nombre de campo es **any** de las siguientes palabras clave reservadas, debe incluirse `${}{}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

Además, las palabras clave reservadas también incluyen cualquiera de las funciones de asignador enumeradas en esta página.

Se puede acceder a los datos de los subcampos utilizando la notación de puntos. Por ejemplo, si había un objeto `name`, para tener acceso al campo `firstName`, utilice `name.firstName`.

## Lista de funciones

En las tablas siguientes se enumeran todas las funciones de asignación admitidas, incluidas las expresiones de muestra y sus resultados.

### Funciones de cadena {#string}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concatena | Concatena las cadenas dadas. | <ul><li>STRING: cadenas que se concatenarán.</li></ul> | concat(CADENA_1, CADENA_2) | concat(&quot;Hola, &quot;, &quot;hay&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explotar | Divide la cadena en función de una regex y devuelve una matriz de partes. Opcionalmente, puede incluir regex para dividir la cadena. De forma predeterminada, la división se resuelve en &quot;,&quot;. Los siguientes delimitadores **necesitan** que se escapen con `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Si incluye varios caracteres como delimitador, el delimitador se tratará como un delimitador de varios caracteres. | <ul><li>CADENA: **Requerida** La cadena que debe dividirse.</li><li>REGEX: *Opcional* La expresión regular que se puede usar para dividir la cadena.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hola, ¡ahí!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Devuelve la ubicación o el índice de una subcadena. | <ul><li>ENTRADA: **Requerida** La cadena que se está buscando.</li><li>SUBCADENA: **Requerida** La subcadena que se está buscando dentro de la cadena.</li><li>START_POSITION: *Opcional* La ubicación de donde comenzar a buscar en la cadena.</li><li>OCURRENCIA: *Opcional* La enésima ocurrencia que se busca desde la posición inicial. De forma predeterminada, se establece en 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| reemplazantes | Reemplaza la cadena de búsqueda si está presente en la cadena original. | <ul><li>ENTRADA: **Requerida** La cadena de entrada.</li><li>TO_FIND: **Requerido** La cadena que buscar dentro de la entrada.</li><li>TO_REPLACE: **Requerido** La cadena que reemplazará el valor dentro de &quot;TO_FIND&quot;.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replace(&quot;Esto es una cadena re-test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Esta es una prueba de reemplazo de cadena&quot; |
| substr | Devuelve una subcadena de una longitud determinada. | <ul><li>ENTRADA: **Requerida** La cadena de entrada.</li><li>START_INDEX: **Requerido** Índice de la cadena de entrada donde comienza la subcadena.</li><li>LENGTH: **Requerido** Longitud de la subcadena.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot;un subconjunto&quot; |
| lower /<br>lcase | Convierte una cadena a minúsculas. | <ul><li>ENTRADA: **Requerida** La cadena que se convertirá a minúsculas.</li></ul> | lower(INPUT) | lower(&quot;HeLo&quot;)<br>lcase(&quot;HeLo&quot;) | &quot;hola&quot; |
| upper /<br>ucase | Convierte una cadena a mayúsculas. | <ul><li>ENTRADA: **Requerida** La cadena que se convertirá a mayúsculas.</li></ul> | upper(ENTRADA) | upper(&quot;HeLo&quot;)<br>ucase(&quot;HeLo&quot;) | &quot;HOLA&quot; |
| split | Divide una cadena de entrada en un separador. El siguiente separador **necesita** que se escape con `\`: `\`. Si incluye varios delimitadores, la cadena se dividirá en **cualquiera** de los delimitadores presentes en la cadena. **Nota:** Esta función sólo devuelve índices no nulos de la cadena, independientemente de la presencia del separador. Si se requieren todos los índices, incluidos los valores nulos, en la matriz resultante, utilice la función &quot;explode&quot; en su lugar. | <ul><li>ENTRADA: **Requerida** La cadena de entrada que se va a dividir.</li><li>SEPARADOR: **Requerido** La cadena que se usa para dividir la entrada.</li></ul> | split(ENTRADA, SEPARADOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| unirse | Une una lista de objetos mediante el separador. | <ul><li>SEPARADOR: **Requerido** La cadena que se usará para unir los objetos.</li><li>OBJETOS: **Requerido** Una matriz de cadenas que se unirán.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hola mundo&quot; |
| lpad | Rellena el lado izquierdo de una cadena con la otra cadena dada. | <ul><li>ENTRADA: **Requerida** La cadena que se va a rellenar. Esta cadena puede ser nula.</li><li>RECUENTO: **Requerido** El tamaño de la cadena que se va a rellenar.</li><li>RELLENO: **Requerido** La cadena con la que se va a rellenar la entrada. Si es nulo o está vacío, se tratará como un solo espacio.</li></ul> | lpad(ENTRADA, RECUENTO, RELLENO) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | Rellena el lado derecho de una cadena con la otra cadena dada. | <ul><li>ENTRADA: **Requerida** La cadena que se va a rellenar. Esta cadena puede ser nula.</li><li>RECUENTO: **Requerido** El tamaño de la cadena que se va a rellenar.</li><li>RELLENO: **Requerido** La cadena con la que se va a rellenar la entrada. Si es nulo o está vacío, se tratará como un solo espacio.</li></ul> | rpad(ENTRADA, RECUENTO, RELLENO) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtiene los primeros caracteres &quot;n&quot; de la cadena dada. | <ul><li>CADENA: **Requerida** La cadena para la que está obteniendo los primeros caracteres &quot;n&quot;.</li><li>RECUENTO: **Requerido** Los caracteres &quot;n&quot; que desea obtener de la cadena.</li></ul> | left(CADENA, RECUENTO) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| derecha | Obtiene los últimos &quot;n&quot; caracteres de la cadena dada. | <ul><li>CADENA: **Requerida** La cadena para la que se obtienen los últimos caracteres &quot;n&quot;.</li><li>RECUENTO: **Requerido** Los caracteres &quot;n&quot; que desea obtener de la cadena.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Elimina el espacio en blanco del principio de la cadena. | <ul><li>CADENA: **Requerida** La cadena de la que desea quitar el espacio en blanco.</li></ul> | ltrim(CADENA) | ltrim(&quot; hello&quot;) | &quot;hola&quot; |
| rtrim | Elimina el espacio en blanco del final de la cadena. | <ul><li>CADENA: **Requerida** La cadena de la que desea quitar el espacio en blanco.</li></ul> | rtrim(CADENA) | rtrim(&quot;hello &quot;) | &quot;hola&quot; |
| trim | Elimina el espacio en blanco del principio y del final de la cadena. | <ul><li>CADENA: **Requerida** La cadena de la que desea quitar el espacio en blanco.</li></ul> | trim(CADENA) | trim(&quot; hello &quot;) | &quot;hola&quot; |
| igual a | Compara dos cadenas para confirmar si son iguales. Esta función distingue entre mayúsculas y minúsculas. | <ul><li>CADENA1: **Requerida** La primera cadena que desea comparar.</li><li>CADENA2: **Requerida** La segunda cadena que desea comparar.</li></ul> | CADENA1.&#x200B;es igual a( CADENA2) | &quot;cadena1&quot;.&#x200B;igual a&#x200B;(&quot;STRING1&quot;) | falso |
| igual a IgnoreCase | Compara dos cadenas para confirmar si son iguales. Esta función **no** distingue entre mayúsculas y minúsculas. | <ul><li>CADENA1: **Requerida** La primera cadena que desea comparar.</li><li>CADENA2: **Requerida** La segunda cadena que desea comparar.</li></ul> | CADENA1.&#x200B;igual a IgnoreCase&#x200B;(STRING2) | &quot;cadena1&quot;.&#x200B;igual a IgnoreCase&#x200B;(&quot;STRING1) | verdadero |

{style="table-layout:auto"}

### Funciones de expresión regular

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrae grupos de la cadena de entrada en función de una expresión regular. | <ul><li>CADENA: **Requerida** La cadena de la que está extrayendo los grupos.</li><li>REGEX: **Requerido** Expresión regular que desea que coincida el grupo.</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot;&#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Comprueba si la cadena coincide con la expresión regular introducida. | <ul><li>CADENA: **Requerida** La cadena que está comprobando coincide con la expresión regular.</li><li>REGEX: **Requerido** Expresión regular con la que está comparando.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | verdadero |

{style="table-layout:auto"}

### Funciones hash {#hashing}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Toma una entrada y produce un valor hash utilizando el algoritmo hash seguro 1 (SHA-1). | <ul><li>ENTRADA: **Requerida** El texto sin formato que se va a hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles incluyen UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;mi texto&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 48690840c5dfcce3c80 |
| sha256 | Toma una entrada y produce un valor hash utilizando el algoritmo hash seguro 256 (SHA-256). | <ul><li>ENTRADA: **Requerida** El texto sin formato que se va a hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles incluyen UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha256(ENTRADA, CHARSET) | sha256(&quot;mi texto&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Toma una entrada y produce un valor hash utilizando el algoritmo hash seguro 512 (SHA-512). | <ul><li>ENTRADA: **Requerida** El texto sin formato que se va a hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles incluyen UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha512(ENTRADA, CHARSET) | sha512(&quot;mi texto&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef 708bf11b4232bb21d2a8704ada2cdcd7b367dd078a89 a5c908cfe377aceb1072a7b 386b7d4fd2ff68a8fd24d16 |
| md5 | Toma una entrada y produce un valor hash con MD5. | <ul><li>ENTRADA: **Requerida** El texto sin formato que se va a hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles incluyen UTF-8, UTF-16, ISO-8859-1 y US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;mi texto&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 e9bd0198d03ba6852c7 |
| crc32 | Toma una entrada utiliza un algoritmo de comprobación de redundancia cíclica (CRC) para producir un código cíclico de 32 bits. | <ul><li>ENTRADA: **Requerida** El texto sin formato que se va a hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles incluyen UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;mi texto&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### Funciones de URL {#url}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Devuelve el protocolo de la dirección URL determinada. Si la entrada no es válida, devuelve nulo. | <ul><li>URL: **Requerida** Dirección URL de la cual se debe extraer el protocolo.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform .adobe.com/home&quot;) | https |
| get_url_host | Devuelve el host de la URL determinada. Si la entrada no es válida, devuelve nulo. | <ul><li>URL: **Requerida** Dirección URL de la cual se debe extraer el host.</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Devuelve el puerto de la dirección URL determinada. Si la entrada no es válida, devuelve nulo. | <ul><li>URL: **Requerido** Dirección URL de la cual se debe extraer el puerto.</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/ joe/employee.csv&quot;) | 22 |
| get_url_path | Devuelve la ruta de la dirección URL determinada. De forma predeterminada, se devuelve la ruta de acceso completa. | <ul><li>URL: **Requerida** Dirección URL de la cual se debe extraer la ruta.</li><li>FULL_PATH: *Opcional* Un valor booleano que determina si se devuelve la ruta de acceso completa. Si se establece en false, solo se devuelve el final de la ruta.</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com// home/joe/employee.csv&quot;) | &quot;//home/joe/ employee.csv&quot; |
| get_url_query_str | Devuelve la cadena de consulta de una dirección URL determinada como un mapa del nombre y el valor de la cadena de consulta. | <ul><li>URL: **Requerida** Dirección URL desde la que intenta obtener la cadena de consulta.</li><li>ANCLAJE: **Requerido** Determina qué se hará con el anclaje en la cadena de consulta. Puede ser uno de los tres valores siguientes: &quot;keep&quot;, &quot;remove&quot; o &quot;append&quot;.<br><br>Si el valor es &quot;conservar&quot;, el anclaje se adjuntará al valor devuelto.<br>Si el valor es &quot;remove&quot;, el anclaje se eliminará del valor devuelto.<br>Si el valor es &quot;anexar&quot;, el anclaje se devolverá como un valor independiente.</li></ul> | get_url_query_str&#x200B;(URL, ANCLAJE) | get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there?name= ferret#nose&quot;, &quot;keep&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there?name= ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com&#x200B;:8042/over/there&#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Esta función toma una URL como entrada y reemplaza o codifica los caracteres especiales con caracteres ASCII. Para obtener más información sobre caracteres especiales, lea la [lista de caracteres especiales](#special-characters) en el apéndice de este documento. | <ul><li>URL: **Requerida** La dirección URL de entrada con caracteres especiales que desea reemplazar o codificar con caracteres ASCII.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partneralliance_asia-pacífico_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacífico_2022 |
| get_url_decoded | Esta función toma una URL como entrada y descodifica los caracteres ASCII en caracteres especiales.  Para obtener más información sobre caracteres especiales, lea la [lista de caracteres especiales](#special-characters) en el apéndice de este documento. | <ul><li>URL: **Requerida** La URL de entrada con caracteres ASCII que desea descodificar en caracteres especiales.</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacífico_2022&quot;) | https</span>://example.com/partneralliance_asia-pacífico_2022 |

{style="table-layout:auto"}

### Funciones de fecha y hora {#date-and-time}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla. Encontrará más información sobre la función `date` en la sección de fechas de la [guía de administración de formato de datos](./data-handling.md#dates).

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Recupera la hora actual. | | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | Recupera la hora Unix actual. | | timestamp() | timestamp() | 1571850624571 |
| formato | Aplica formato a la fecha de entrada según un formato especificado. | <ul><li>FECHA: **Requerida** La fecha de entrada, como objeto ZonedDateTime, a la que desea dar formato.</li><li>FORMATO: **Requerido** El formato al que desea cambiar la fecha.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | Convierte una marca de tiempo en una cadena de fecha según un formato especificado. | <ul><li>Marca de tiempo: **Requerida** La marca de tiempo a la que desea dar formato. Esto se escribe en milisegundos.</li><li>FORMATO: **Requerido** El formato en el que desea que se convierta la marca de tiempo.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| fecha | Convierte una cadena de fecha en un objeto ZonedDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li><li>FORMATO: **Requerido** La cadena que representa el formato de la fecha de origen.**Nota:** Esto hace que **no** represente el formato en el que desea convertir la cadena de fecha. </li><li>DEFAULT_DATE: **Obligatorio** Se devolvió la fecha predeterminada, si la fecha proporcionada es nula.</li></ul> | date(FECHA, FORMATO, FECHA_PREDETERMINADA) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| fecha | Convierte una cadena de fecha en un objeto ZonedDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li><li>FORMATO: **Requerido** La cadena que representa el formato de la fecha de origen.**Nota:** Esto hace que **no** represente el formato en el que desea convertir la cadena de fecha. </li></ul> | date(FECHA, FORMATO) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| fecha | Convierte una cadena de fecha en un objeto ZonedDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li></ul> | date(FECHA) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Recupera las partes de la fecha. Se admiten los siguientes valores de componente: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;día<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br> | <ul><li>COMPONENTE: **Requerido** Una cadena que representa la parte de la fecha. </li><li>FECHA: **Requerida** La fecha, en un formato estándar.</li></ul> | date_part&#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Reemplaza un componente en una fecha determinada. Se aceptan los siguientes componentes: <br><br>&quot;año&quot;<br>&quot;aaaa&quot;<br>&quot;aa&quot;<br><br>&quot;mes&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;día&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hora&quot;<br>&quot;hh&quot;<br><br>&quot;minuto&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;segundo&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPONENTE: **Requerido** Una cadena que representa la parte de la fecha. </li><li>VALOR: **Requerido** Valor que se va a establecer para el componente en una fecha determinada.</li><li>FECHA: **Requerida** La fecha, en un formato estándar.</li></ul> | set_date_part&#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Crea una fecha a partir de artículos. Esta función también se puede inducir usando make_timestamp. | <ul><li>AÑO: **Obligatorio** El año, escrito con cuatro dígitos.</li><li>MES: **Requerido** mes. Los valores permitidos son del 1 al 12.</li><li>DÍA: **Requerido** El día. Los valores permitidos son del 1 al 31.</li><li>HORA: **Requerido** La hora. Los valores permitidos son de 0 a 23.</li><li>MINUTO: **Requerido** El minuto. Los valores permitidos son de 0 a 59.</li><li>NANOSECOND: **Requerido** Los valores de nanosegundos. Los valores permitidos son de 0 a 999999999.</li><li>ZONA HORARIA: **Requerida** La zona horaria de la fecha y hora.</li></ul> | make_date_time&#x200B;(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;América/Los_Ángeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Convierte una fecha de cualquier zona horaria en una fecha en UTC. | <ul><li>FECHA: **Requerida** La fecha que intenta convertir.</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Convierte una fecha de una zona horaria a otra. | <ul><li>FECHA: **Requerida** La fecha que intenta convertir.</li><li>ZONA: **Requerida** Zona horaria a la que intenta convertir la fecha.</li></ul> | zone_date_to_zone&#x200B;(DATE, ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Jerarquías: objetos {#objects}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Comprueba si un objeto está o no vacío. | <ul><li>ENTRADA: **Requerida** El objeto que intenta comprobar está vacío.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | falso |
| array_to_object | Crea una lista de objetos. | <ul><li>ENTRADA: **Requerida** Una agrupación de pares de claves y matrices.</li></ul> | array_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Crea un objeto basado en los pares de clave/valor plano dados. | <ul><li>ENTRADA: **Requerida** Una lista plana de pares clave/valor.</li></ul> | to_object(INPUT) | to_object&#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crea un objeto de la cadena de entrada. | <ul><li>STRING: **Requerido** La cadena que se está analizando para crear un objeto.</li><li>VALUE_DELIMITER: *Opcional* El delimitador que separa un campo del valor. El delimitador predeterminado es `:`.</li><li>FIELD_DELIMITER: *Opcional* El delimitador que separa los pares de valor de campo. El delimitador predeterminado es `,`.</li></ul> | str_to_object&#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Nota**: Puede utilizar la función `get()` junto con `str_to_object()` para recuperar los valores de las claves de la cadena. | <ul><li>Ejemplo #1: str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>Ejemplo #2: str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>Ejemplo #1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Ejemplo #2: &quot;John&quot;</li></ul> |
| contains_key | Comprueba si el objeto existe en los datos de origen. **Nota:** Esta función reemplaza la función obsoleta `is_set()`. | <ul><li>ENTRADA: **Requerida** Ruta de acceso que se debe comprobar si existe dentro de los datos de origen.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | verdadero |
| anular | Establece el valor del atributo en `null`. Debe utilizarse cuando no desee copiar el campo en el esquema de destino. | | nullify() | nullify() | `null` |
| get_keys | Analiza los pares clave/valor y devuelve todas las claves. | <ul><li>OBJETO: **Requerido** El objeto del cual se extraerán las claves.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Pride and Prejudice&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analiza los pares clave/valor y devuelve el valor de la cadena, en función de la clave dada. | <ul><li>CADENA: **Requerida** La cadena que desea analizar.</li><li>CLAVE: **Requerida** Clave para la que se debe extraer el valor.</li><li>VALUE_DELIMITER: **Requerido** El delimitador que separa el campo y el valor. Si se proporciona `null` o una cadena vacía, este valor es `:`.</li><li>FIELD_DELIMITER: *Opcional* El delimitador que separa los pares de campo y valor. Si se proporciona `null` o una cadena vacía, este valor es `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | Toma un mapa y una entrada de clave. Si la entrada es una clave única, la función devuelve el valor asociado a esa clave. Si la entrada es una matriz de cadenas, la función devuelve todos los valores correspondientes a las claves proporcionadas. Si el mapa entrante tiene claves duplicadas, el valor devuelto debe anular la duplicación de las claves y devolver valores únicos. | <ul><li>MAPA: **Requerido** Los datos del mapa de entrada.</li><li>CLAVE: **Requerida** La clave puede ser una sola cadena o una matriz de cadenas. Si se proporciona cualquier otro tipo primitivo (datos/número), se trata como una cadena.</li></ul> | get_values(MAP, KEY) | Consulte el [apéndice](#map_get_values) para ver un ejemplo de código. | |
| map_has_keys | Si se proporcionan una o más claves de entrada, la función devuelve true. Si se proporciona una matriz de cadenas como entrada, la función devuelve true en la primera clave encontrada. | <ul><li>MAPA: **Requerido** Los datos de asignación de entrada</li><li>CLAVE: **Requerida** La clave puede ser una sola cadena o una matriz de cadenas. Si se proporciona cualquier otro tipo primitivo (datos/número), se trata como una cadena.</li></ul> | map_has_keys(MAP, KEY) | Consulte el [apéndice](#map_has_keys) para ver un ejemplo de código. | |
| add_to_map | Acepta al menos dos entradas. Se puede proporcionar cualquier cantidad de mapas como entradas. La preparación de datos devuelve un solo mapa que tiene todos los pares clave-valor de todas las entradas. Si se repiten una o más claves (en el mismo mapa o entre mapas), la preparación de datos anula la duplicación de las claves para que el primer par clave-valor persista en el orden en que se pasaron en la entrada. | MAPA: **Requerido** Los datos del mapa de entrada. | add_to_map(MAPA 1, MAPA 2, MAPA 3, ...) | Consulte el [apéndice](#add_to_map) para ver un ejemplo de código. | |
| object_to_map (Sintaxis 1) | Utilice esta función para crear tipos de datos de mapa. | <ul><li>CLAVE: **Requerido** Las claves deben ser una cadena. Si se proporciona cualquier otro valor primitivo, como números enteros o fechas, se convierten automáticamente en cadenas y se tratan como cadenas.</li><li>ANY_TYPE: **Obligatorio** Se refiere a cualquier tipo de datos XDM admitido, excepto Mapas.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, ... ) | Consulte el [apéndice](#object_to_map) para ver un ejemplo de código. | |
| object_to_map (Sintaxis 2) | Utilice esta función para crear tipos de datos de mapa. | <ul><li>OBJETO: **Requerido** Puede proporcionar un objeto entrante o matriz de objetos y señalar a un atributo dentro del objeto como clave.</li></ul> | object_to_map(OBJECT) | Consulte el [apéndice](#object_to_map) para ver un ejemplo de código. |
| object_to_map (Sintaxis 3) | Utilice esta función para crear tipos de datos de mapa. | <ul><li>OBJETO: **Requerido** Puede proporcionar un objeto entrante o matriz de objetos y señalar a un atributo dentro del objeto como clave.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Consulte el [apéndice](#object_to_map) para ver un ejemplo de código. |

{style="table-layout:auto"}

Para obtener información sobre la característica de copia de objetos, consulte la sección [debajo de](#object-copy).

### Jerarquías - Matrices {#arrays}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| fundirse | Devuelve el primer objeto no nulo de una matriz determinada. | <ul><li>ENTRADA: **Requerida** La matriz de la que desea encontrar el primer objeto no nulo.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;primero&quot; |
| primero | Recupera el primer elemento de la matriz determinada. | <ul><li>ENTRADA: **Requerida** La matriz de la que desea encontrar el primer elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| última(s) | Recupera el último elemento de la matriz determinada. | <ul><li>ENTRADA: **Requerida** La matriz de la que desea encontrar el último elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Añade elementos al final de la matriz. | <ul><li>MATRIZ: **Requerida** Matriz a la que está agregando elementos.</li><li>VALUES: Los elementos que desea anexar a la matriz.</li></ul> | add_to_array&#x200B;(MATRIZ, VALORES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_array | Combina las matrices entre sí. | <ul><li>MATRIZ: **Requerida** Matriz a la que está agregando elementos.</li><li>VALUES: Las matrices que desea anexar a la matriz principal.</li></ul> | join_array&#x200B;(ARRAY, VALUES) | join_array&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Toma una lista de entradas y la convierte en una matriz. | <ul><li>INCLUDE_NULLS: **Requerido** Valor booleano que indica si se deben incluir o no valores nulos en la matriz de respuesta.</li><li>VALORES: **Requerido** Los elementos que se van a convertir en una matriz.</li></ul> | to_array&#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Devuelve el tamaño de la entrada. | <ul><li>ENTRADA: **Requerida** El objeto del que intenta encontrar el tamaño.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Esta función se utiliza para anexar todos los elementos de toda la matriz de entrada al final de la matriz en Profile. Esta función es **solamente** aplicable durante las actualizaciones. Si se utiliza en el contexto de las inserciones, esta función devuelve la entrada tal cual. | <ul><li>MATRIZ: **Requerido** La matriz para anexar la matriz en el perfil.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | Esta función se utiliza para reemplazar elementos en una matriz. Esta función es **solamente** aplicable durante las actualizaciones. Si se utiliza en el contexto de las inserciones, esta función devuelve la entrada tal cual. | <ul><li>MATRIZ: **Requerido** La matriz para reemplazar la matriz en el perfil.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |
| [!BADGE Solo destinos]{type=Informative} array_to_string | Une las representaciones de cadena de los elementos de una matriz utilizando el separador especificado. Si la matriz es multidimensional, se acopla antes de unirse. **Nota**: esta función se usa en destinos. Lea la [documentación](../destinations/ui/export-arrays-maps-objects.md) para obtener más información. | <ul><li>SEPARADOR: **Requerido** El separador usado para unir los elementos de la matriz.</li><li>MATRIZ: **Requerida** Matriz que se unirá (después del acoplamiento).</li></ul> | array_to_string(SEPARATOR, ARRAY) | `array_to_string(";", ["Hello", "world"])` | &quot;Hola;mundo&quot; |
| [!BADGE Solo destinos]{type=Informative} filterArray* | Filtra la matriz determinada en función de un predicado. **Nota**: esta función se usa en destinos. Lea la [documentación](../destinations/ui/export-arrays-maps-objects.md) para obtener más información. | <ul><li>MATRIZ: **Requerido** La matriz que se filtrará</li><li>PREDICADO: **Requerido** El predicado que se aplicará en cada elemento de la matriz dada. | filterArray(MATRIZ, PREDICADO) | `filterArray([5, -6, 0, 7], x -> x > 0)` | [5, 7] |
| [!BADGE Solo destinos]{type=Informative} transformArray* | Transforma la matriz determinada en función de un predicado. **Nota**: esta función se usa en destinos. Lea la [documentación](../destinations/ui/export-arrays-maps-objects.md) para obtener más información. | <ul><li>MATRIZ: **Requerido** La matriz que se va a transformar.</li><li>PREDICADO: **Requerido** El predicado que se aplicará en cada elemento de la matriz dada. | transformArray(MATRIZ, PREDICADO) | ` transformArray([5, 6, 7], x -> x + 1)` | [6, 7, 8] |
| [!BADGE Solo destinos]{type=Informative} flattenArray* | Acople la matriz determinada (multidimensional) a una matriz unidimensional. **Nota**: esta función se usa en destinos. Lea la [documentación](../destinations/ui/export-arrays-maps-objects.md) para obtener más información. | <ul><li>MATRIZ: **Requerido** La matriz que se va a acoplar.</li></ul> | flattenArray(MATRIZ) | flattenArray([[&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;, &#39;d&#39;]], [[&#39;e&#39;], [&#39;f&#39;]]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;, &#39;f&#39;] |

{style="table-layout:auto"}

### Jerarquías: asignación {#map}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Esta función toma una matriz de objetos y una clave como entrada y devuelve un mapa del campo de la clave con el valor como clave y el elemento de matriz como valor. | <ul><li>ENTRADA: **Requerida** La matriz de objetos de la que desea encontrar el primer objeto no nulo.</li><li>CLAVE: **Requerida** La clave debe ser un nombre de campo en la matriz de objetos y el objeto como valor.</li></ul> | array_to_map(OBJECT[] INPUTS, KEY) | Lea el [apéndice](#object_to_map) para ver un ejemplo de código. |
| object_to_map | Esta función toma un objeto como argumento y devuelve un mapa de pares clave-valor. | <ul><li>ENTRADA: **Requerida** La matriz de objetos de la que desea encontrar el primer objeto no nulo.</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address) donde input es &quot; + &quot;address: {line1 : \&quot;345 park ave\&quot;,line2: \&quot;bldg 2\&quot;,City : \&quot;san jose\&quot;,State : \&quot;CA\&quot;,type: \&quot;office\&quot;}&quot; | Devuelve un mapa con pares de nombre y valor de campo determinados o nulo si la entrada es nula. Por ejemplo: `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Esta función toma una lista de pares clave-valor y devuelve un mapa de pares clave-valor. | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;, \&quot;John\&quot;, \&quot;lastName\&quot;, \&quot;Doe\&quot;)&quot; | Devuelve un mapa con pares de nombre y valor de campo determinados o nulo si la entrada es nula. Por ejemplo: `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Operadores lógicos {#logical-operators}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| descifrar | Dadas una clave y una lista de pares de valor clave acoplados como una matriz, la función devuelve el valor si se encuentra la clave o devuelve un valor predeterminado si está presente en la matriz. | <ul><li>CLAVE: **Requerida** La clave que se va a buscar coincide.</li><li>OPTIONS: **Requerido** Una matriz aplanada de pares clave/valor. De forma opcional, se puede colocar un valor predeterminado al final.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Si el stateCode proporcionado es &quot;ca&quot;, &quot;California&quot;.<br>Si el stateCode proporcionado es &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Si stateCode no coincide con lo siguiente, &quot;N/A&quot;. |
| iif | Evalúa una expresión booleana determinada y devuelve el valor especificado en función del resultado. | <ul><li>EXPRESIÓN: **Requerida** La expresión booleana que se está evaluando.</li><li>TRUE_VALUE: **Requerido** El valor que se devuelve si la expresión se evalúa como true.</li><li>FALSE_VALUE: **Requerido** El valor que se devuelve si la expresión se evalúa como falsa.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### Agregación {#aggregation}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Devuelve el mínimo de los argumentos dados. Utiliza el orden natural. | <ul><li>OPTIONS: **Requerido** Uno o más objetos que se pueden comparar entre sí.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Devuelve el máximo de los argumentos dados. Utiliza el orden natural. | <ul><li>OPTIONS: **Requerido** Uno o más objetos que se pueden comparar entre sí.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Escribir conversiones {#type-conversions}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Convierte una cadena en un BigInteger. | <ul><li>STRING: **Requerido** La cadena que se va a convertir en un BigInteger.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Convierte una cadena en un valor Double. | <ul><li>CADENA: **Requerida** La cadena que se va a convertir en un valor de tipo Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Convierte una cadena en flotante. | <ul><li>CADENA: **Requerida** La cadena que se va a convertir en un valor Flotante.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Convierte una cadena en un número entero. | <ul><li>STRING: **Requerido** La cadena que se va a convertir en un número entero.</li></ul> | to_integer(CADENA) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### Funciones JSON {#json}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserialice el contenido JSON de la cadena determinada. | <ul><li>CADENA: **Requerida** La cadena JSON que se va a deserializar.</li></ul> | json_to_object&#x200B;(STRING) | json_to_object&#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}}) | Un objeto que representa el JSON. |

{style="table-layout:auto"}

### Operaciones especiales {#special-operations}

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Genera un ID pseudoaleatorio. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | Esta función toma una cadena FPID y la convierte en un ECID para su uso en aplicaciones de Adobe Experience Platform y Adobe Experience Cloud. | <ul><li>CADENA: **Requerido** La cadena FPID que se convertirá en ECID.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Funciones del agente de usuario {#user-agent}

Cualquiera de las funciones de agente de usuario que se incluyen en la tabla siguiente puede devolver cualquiera de los siguientes valores:

* Teléfono: dispositivo móvil con pantalla pequeña (normalmente &lt; 7&quot;)
* Móvil: dispositivo móvil que aún no se ha identificado. Este dispositivo móvil puede ser un eReader, una tableta, un teléfono, un reloj, etc.

Para obtener más información sobre los valores de los campos de dispositivos, lea la [lista de valores de los campos de dispositivos](#device-field-values) en el apéndice de este documento.

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrae el nombre del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrae la versión principal del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | IOS 5 |
| ua_os_version | Extrae la versión del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrae el nombre y la versión del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrae la versión del agente de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extrae el nombre del agente y la versión principal de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrae el nombre del agente de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrae la clase de dispositivo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Teléfono |

{style="table-layout:auto"}

### Funciones de Analytics {#analytics}

>[!NOTE]
>
>Solo puede utilizar las siguientes funciones de análisis para flujos de WebSDK y Adobe Analytics.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extrae el ID de evento de una cadena de eventos de Analytics. | <ul><li>EVENT_STRING: **Requerido** La cadena de evento de Analytics separada por comas.</li><li>EVENT_NAME: **Requerido** El nombre del evento que se va a extraer e ID.</li></ul> | aa_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 123456 |
| aa_get_event_value | Extrae el valor del evento de una cadena de eventos de Analytics. Si no se especifica el valor del evento, se devuelve 1. | <ul><li>EVENT_STRING: **Requerido** La cadena de evento de Analytics separada por comas.</li><li>EVENT_NAME: **Requerido** El nombre del evento del que se extraerá un valor.</li></ul> | aa_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 5 |
| aa_get_product_categories | Extrae la categoría de producto de una cadena de productos de Analytics. | <ul><li>PRODUCTS_STRING: **Requerido** La cadena de productos de Analytics.</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories(&quot;;Ejemplo de producto 1;1;3.50,Ejemplo de categoría 2;Ejemplo de producto 2;1;5.99&quot;) | [null,&quot;Ejemplo de categoría 2&quot;] |
| aa_get_product_names | Extrae el nombre de un producto de una cadena de productos de Analytics. | <ul><li>PRODUCTS_STRING: **Requerido** La cadena de productos de Analytics.</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names(&quot;;Ejemplo de producto 1;1;3.50,Ejemplo de categoría 2;Ejemplo de producto 2;1;5.99&quot;) | [&quot;Ejemplo de producto 1&quot;,&quot;Ejemplo de producto 2&quot;] |
| aa_get_product_quantity | Extrae las cantidades de una cadena de productos de Analytics. | <ul><li>PRODUCTS_STRING: **Requerido** La cadena de productos de Analytics.</li></ul> | aa_get_product_quantity(PRODUCTS_STRING) | aa_get_product_quantity(&quot;;Ejemplo de producto 1;1;3.50,Ejemplo de categoría 2;Ejemplo de producto 2&quot;) | [&quot;1&quot;, nulo] |
| aa_get_product_price | Extrae el precio de una cadena de productos de Analytics. | <ul><li>PRODUCTS_STRING: **Requerido** La cadena de productos de Analytics.</li></ul> | aa_get_product_price(PRODUCTS_STRING) | aa_get_product_price(&quot;;Ejemplo de producto 1;1;3.50,Ejemplo de categoría 2;Ejemplo de producto 2&quot;) | [&quot;3.50&quot;, nulo] |
| aa_get_product_event_values | Extrae los valores del evento con nombre de la cadena de products como una matriz de cadenas. | <ul><li>PRODUCTS_STRING: **Requerido** La cadena de productos de Analytics.</li><li>EVENT_NAME: **Requerido** El nombre del evento del que se extraerán los valores.</li></ul> | aa_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_values(&quot;;Ejemplo product 1;1;4.20;event1=2.3\|event2=5:1,;Ejemplo product 2;1;4.20;event1=3\|event2=2:2&quot;, &quot;event1&quot;) | [&quot;2.3&quot;, &quot;3&quot;] |
| aa_get_product_evars | Extrae los valores de eVar del evento con nombre de la cadena de products como una matriz de cadenas. | <ul><li>PRODUCTS_STRING: **Requerido** La cadena de productos de Analytics.</li><li>EVAR_NAME: **Requerido** El nombre de eVar que se va a extraer.</li></ul> | aa_get_product_evars(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_evars(&quot;;Ejemplo de producto;1;6.69;;eVar1=Valor de comercialización&quot;, &quot;eVar1&quot;) | [&quot;Valor de comercialización&quot;] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Copia de objeto {#object-copy}

>[!TIP]
>
>La función de copia de objetos se aplica automáticamente cuando un objeto del origen se asigna a un objeto del XDM. No se necesitan acciones adicionales de los usuarios.

Puede utilizar la función de copia de objetos para copiar automáticamente los atributos de un objeto sin realizar cambios en la asignación. Por ejemplo, si los datos de origen tienen una estructura de:

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

y una estructura XDM de:

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

A continuación, la asignación pasa a ser:

```json
address -> addr
address.line1 -> addr.addrLine1
```

En el ejemplo anterior, los atributos `city` y `state` también se incorporan automáticamente durante la ejecución porque el objeto `address` está asignado a `addr`. Si crea un atributo `line2` en la estructura XDM y los datos de entrada también contienen un `line2` en el objeto `address`, también se incorporará automáticamente sin necesidad de modificar manualmente la asignación.

Para garantizar que la asignación automática funcione, se deben cumplir los siguientes requisitos previos:

* Los objetos de nivel principal deben asignarse;
* Se deben haber creado nuevos atributos en el esquema XDM;
* Los nuevos atributos deben tener nombres coincidentes en el esquema de origen y en el esquema XDM.

Si no se cumplen todos los requisitos previos, debe asignar manualmente el esquema de origen al esquema XDM mediante la preparación de datos.

## Apéndice

A continuación se proporciona información adicional sobre el uso de funciones de asignación de preparación de datos

### Caracteres especiales {#special-characters}

La siguiente tabla describe una lista de caracteres reservados y sus caracteres codificados correspondientes.

| Carácter reservado | Carácter codificado |
| --- | --- |
| espacio | %20 |
| ! | %21 |
| ” | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
| ; | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| &lbrack; | %5B |
| | | %5C |
| &rbrack; | %5D |
| ^ | %5E |
| &grave; | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Valores de campo de dispositivo {#device-field-values}

La tabla siguiente describe una lista de valores de campos de dispositivo y sus descripciones correspondientes.

| Device | Descripción |
| --- | --- |
| Escritorio | Un tipo de dispositivo de escritorio o portátil. |
| Anonimizado | Un dispositivo anónimo. En algunos casos, estos son `useragents` que han sido alterados por un software de anonimización. |
| Desconocido | Un dispositivo desconocido. Generalmente son `useragents` y no contienen información sobre el dispositivo. |
| Dispositivo móvil | Dispositivo móvil que aún no se ha identificado. Este dispositivo móvil puede ser un eReader, una tableta, un teléfono, un reloj, etc. |
| Tableta | Un dispositivo móvil con una pantalla grande (normalmente > 7&quot;). |
| Teléfono | Un dispositivo móvil con una pantalla pequeña (normalmente &lt; 7&quot;). |
| Ver | Un dispositivo móvil con una pantalla pequeña (normalmente &lt; 2&quot;). Estos dispositivos funcionan normalmente como una pantalla adicional para un dispositivo de tipo teléfono/tableta. |
| Realidad aumentada | Un dispositivo móvil con capacidades de AR. |
| Realidad virtual | Un dispositivo móvil con capacidades de RV. |
| eReader | Dispositivo similar a una tableta, pero normalmente con una pantalla de [!DNL eInk]. |
| Cuadro en la parte superior | Dispositivo conectado que permite la interacción a través de una pantalla de tamaño TV. |
| TV | Dispositivo similar al decodificador, pero integrado en el televisor. |
| Dispositivo doméstico | Un electrodoméstico (generalmente grande), como un refrigerador. |
| Consola de juego | Un sistema de juego fijo como [!DNL Playstation] o [!DNL XBox]. |
| Consola de juego portátil | Un sistema de juegos móvil como [!DNL Nintendo Switch]. |
| Voz | Un dispositivo controlado por voz como [!DNL Amazon Alexa] o [!DNL Google Home]. |
| Coche | Un explorador basado en vehículo. |
| Robot | Robots que visitan un sitio web. |
| Robot móvil | Robots que visitan un sitio web pero que indican que desean que se les considere visitantes móviles. |
| Robot Imitator | Robots que visitan un sitio web, fingiendo que son robots como [!DNL Google], pero no lo son. **Nota**: En la mayoría de los casos, los imitadores de robots son robots. |
| Nube | Una aplicación basada en la nube. Estos no son ni robots ni hackers, sino aplicaciones que necesitan conectarse. Esto incluye [!DNL Mastodon] servidores. |
| Pirata Informático | Este valor de dispositivo se utiliza en caso de que se detecten scripts en la cadena `useragent`. |

{style="table-layout:auto"}

### Muestras de código {#code-samples}

#### map_get_values {#map-get-values}

+++Seleccione para ver el ejemplo

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++Seleccione para ver el ejemplo

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++Seleccione para ver el ejemplo

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**Sintaxis 1**

+++Seleccione para ver el ejemplo

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**Sintaxis 2**

+++Seleccione para ver el ejemplo

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**Sintaxis 3**

+++Seleccione para ver el ejemplo

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++Seleccione para ver el ejemplo

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

