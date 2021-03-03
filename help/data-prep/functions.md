---
keywords: Experience Platform;inicio;temas populares;asignación de csv;asignación de archivo csv;asignación de archivo csv a xdm;asignación de csv a xdm;guía de interfaz de usuario;asignador;asignación;campos de asignación;funciones de asignación
solution: Experience Platform
title: Funciones de asignación de preparación de datos
topic: sobre validación
description: Este documento introduce las funciones de asignación utilizadas con la preparación de datos.
translation-type: tm+mt
source-git-commit: 6a541cca307dec8937c2d49470e8bcab770c80c7
workflow-type: tm+mt
source-wordcount: '3719'
ht-degree: 3%

---


# Funciones de asignación de preparación de datos

Las funciones de preparación de datos se pueden utilizar para calcular y calcular valores según lo introducido en los campos de origen.

## Campos

Un nombre de campo puede ser cualquier identificador legal: una secuencia de longitud ilimitada de letras y dígitos Unicode que comienza con una letra, el signo de dólar (`$`) o el carácter de subrayado (`_`). Los nombres de las variables también distinguen entre mayúsculas y minúsculas.

Si un nombre de campo no sigue esta convención, el nombre del campo debe estar ajustado con `${}`. Por lo tanto, si el nombre del campo es &quot;Nombre&quot; o &quot;Nombre&quot;, entonces el nombre debe ajustarse como `${First Name}` o `${First.Name}` respectivamente.

Además, si el nombre de un campo es **any** de las siguientes palabras clave reservadas, debe ajustarse con `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Se puede acceder a los datos de los subcampos mediante la notación de puntos. Por ejemplo, si había un objeto `name`, para acceder al campo `firstName`, utilice `name.firstName`.

## Lista de funciones

En las tablas siguientes se enumeran todas las funciones de asignación admitidas, incluidas las expresiones de ejemplo y sus resultados.

### Funciones de cadena

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Concatena las cadenas dadas. | <ul><li>CADENA: Las cadenas que se concatenarán.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;ahi&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explosión | Divide la cadena en función de un regex y devuelve una matriz de partes. Opcionalmente, puede incluir regex para dividir la cadena. De forma predeterminada, la división se resuelve en &quot;,&quot;. Los siguientes delimitadores **necesitan** que se escapen con `\`: `+, ?, ^, |, ., [, (, {, ), *, $, \` | <ul><li>CADENA: **Requerido** La cadena que debe dividirse.</li><li>REGEX: *Opcional* La expresión regular que puede utilizarse para dividir la cadena.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hola, ahí!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Devuelve la ubicación/índice de una subcadena. | <ul><li>ENTRADA: **Requerido** La cadena que se está buscando.</li><li>SUBCADENA: **Requerido** La subcadena que se está buscando dentro de la cadena.</li><li>START_POSITION: *Opcional* La ubicación de donde comenzar a buscar en la cadena.</li><li>OCURRENCIA: *Opcional* La enésima incidencia que se busca desde la posición de inicio. De forma predeterminada, se establece en 1. </li></ul> | instr(ENTRADA, SUBCADENA, START_POSITION, OCURRENCIA) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| sustitutor | Reemplaza la cadena de búsqueda si está presente en la cadena original. | <ul><li>ENTRADA: **Requerido** La cadena de entrada.</li><li>TO_FIND: **Requerido** La cadena que se va a buscar dentro de la entrada.</li><li>TO_REPLACE: **Requerido** La cadena que reemplazará el valor dentro de &quot;TO_FIND&quot;.</li></ul> | reemplazador(ENTRADA, TO_FIND, TO_REPLACE) | replacestr(&quot;Esto es una prueba de cadena&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Esta es una prueba de reemplazo de cadena&quot; |
| substr | Devuelve una subcadena de una longitud determinada. | <ul><li>ENTRADA: **Requerido** La cadena de entrada.</li><li>START_INDEX: **Requerido** Índice de la cadena de entrada donde se inicia la subcadena.</li><li>LONGITUD: **Requerido** La longitud de la subcadena.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;Esto es una prueba de subcadena&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Convierte una cadena en minúsculas. | <ul><li>ENTRADA: **Requerido** La cadena que se convertirá a minúsculas.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| mayúscula /<br>ucase | Convierte una cadena en mayúsculas. | <ul><li>ENTRADA: **Requerido** La cadena que se convertirá en mayúscula.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HOLA&quot; |
| split | Divide una cadena de entrada en un separador. El siguiente separador **necesita** ser escapado con `\`: `\`. | <ul><li>ENTRADA: **Requerido** La cadena de entrada que se va a dividir.</li><li>SEPARADOR: **Requerido** La cadena que se utiliza para dividir la entrada.</li></ul> | split(ENTRADA, SEPARADOR) | split(&quot;Hello world&quot;, &quot; &quot;&quot;) | `["Hello", "world"]` |
| join | Une una lista de objetos mediante el separador. | <ul><li>SEPARADOR: **Requerido** La cadena que se utilizará para unir los objetos.</li><li>OBJETOS: **Requerido** Una matriz de cadenas que se unirán.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hola mundo&quot; |
| lpad | Añade el lado izquierdo de una cadena con la otra cadena dada. | <ul><li>ENTRADA: **Requerido** La cadena que se va a rellenar. Esta cadena puede ser nula.</li><li>RECUENTO: **Requerido** El tamaño de la cadena que se va a rellenar.</li><li>AGRUPAMIENTO: **Requerido** La cadena con la que se rellena la entrada. Si es nulo o está vacío, se tratará como un solo espacio.</li></ul> | Lpad(ENTRADA, RECUENTO, AGRUPACIÓN) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | Añade el lado derecho de una cadena con la otra cadena dada. | <ul><li>ENTRADA: **Requerido** La cadena que se va a rellenar. Esta cadena puede ser nula.</li><li>RECUENTO: **Requerido** El tamaño de la cadena que se va a rellenar.</li><li>AGRUPAMIENTO: **Requerido** La cadena con la que se rellena la entrada. Si es nulo o está vacío, se tratará como un solo espacio.</li></ul> | rpad(ENTRADA, RECUENTO, AGRUPACIÓN) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtiene los primeros caracteres &quot;n&quot; de la cadena dada. | <ul><li>CADENA: **Requerido** La cadena para la que se obtienen los primeros caracteres &quot;n&quot;.</li><li>RECUENTO: **Requerido** Los caracteres &quot;n&quot; que desea obtener de la cadena.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Obtiene los últimos caracteres &quot;n&quot; de la cadena dada. | <ul><li>CADENA: **Requerido** La cadena para la que obtiene los últimos caracteres &quot;n&quot;.</li><li>RECUENTO: **Requerido** Los caracteres &quot;n&quot; que desea obtener de la cadena.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Elimina el espacio en blanco del principio de la cadena. | <ul><li>CADENA: **Requerido** La cadena de la que desea quitar el espacio en blanco.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Elimina el espacio en blanco del final de la cadena. | <ul><li>CADENA: **Requerido** La cadena de la que desea quitar el espacio en blanco.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Elimina el espacio en blanco del principio y del final de la cadena. | <ul><li>CADENA: **Requerido** La cadena de la que desea quitar el espacio en blanco.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| es igual que | Compara dos cadenas para confirmar si son iguales. Esta función distingue entre mayúsculas y minúsculas. | <ul><li>CADENA1: **Requerido** La primera cadena que desea comparar.</li><li>CADENA 2: **Requerido** La segunda cadena que desea comparar.</li></ul> | CADENA1. &#x200B;igual( &#x200B; STRING2) | &quot;string1&quot;.&#x200B;es igual a &#x200B;(&quot;STRING1&quot;) | false |
| igual a IgnoreCase | Compara dos cadenas para confirmar si son iguales. Esta función distingue entre mayúsculas y minúsculas **not**. | <ul><li>CADENA1: **Requerido** La primera cadena que desea comparar.</li><li>CADENA 2: **Requerido** La segunda cadena que desea comparar.</li></ul> | CADENA1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;.&#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

&#x200B;

### Funciones de expresión regular

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| extract_regex | Extrae grupos de la cadena de entrada, según una expresión regular. | <ul><li>CADENA: **Requerido** La cadena de la que está extrayendo los grupos.</li><li>REGEX: **Requerido** La expresión regular con la que desea que coincida el grupo.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Comprueba si la cadena coincide con la expresión regular introducida. | <ul><li>CADENA: **Requerido** La cadena que está comprobando coincide con la expresión regular.</li><li>REGEX: **Requerido** La expresión regular con la que se compara.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

### Funciones hash

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Toma una entrada y produce un valor hash utilizando Secure Hash Algorithm 1 (SHA-1). | <ul><li>ENTRADA: **Requerido** El texto sin formato que se va a hash.</li><li>CONJUNTO DE CARÁCTER: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha1(ENTRADA, CHARSET) | sha1(&quot;mi texto&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Toma una entrada y produce un valor hash utilizando Secure Hash Algorithm 256 (SHA-256). | <ul><li>ENTRADA: **Requerido** El texto sin formato que se va a hash.</li><li>CONJUNTO DE CARÁCTER: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha256(ENTRADA, JUEGO) | sha256(&quot;mi texto&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Toma una entrada y produce un valor hash utilizando Secure Hash Algorithm 512 (SHA-512). | <ul><li>ENTRADA: **Requerido** El texto sin formato que se va a hash.</li><li>CONJUNTO DE CARÁCTER: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha512(ENTRADA, ENTRADA) | sha512(&quot;mi texto&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Toma una entrada y produce un valor hash usando MD5. | <ul><li>ENTRADA: **Requerido** El texto sin formato que se va a hash.</li><li>CONJUNTO DE CARÁCTER: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII. </li></ul> | md5(ENTRADA, JUEGO) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Toma una entrada utiliza un algoritmo de comprobación de redundancia cíclica (CRC) para producir un código cíclico de 32 bits. | <ul><li>ENTRADA: **Requerido** El texto sin formato que se va a hash.</li><li>CONJUNTO DE CARÁCTER: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | crc32(ENTRADA, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### Funciones URL

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | Devuelve el protocolo de la dirección URL dada. Si la entrada no es válida, devuelve nulo. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer el protocolo.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Devuelve el host de la URL dada. Si la entrada no es válida, devuelve nulo. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer el host.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Devuelve el puerto de la URL dada. Si la entrada no es válida, devuelve nulo. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer el puerto.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Devuelve la ruta de la dirección URL dada. De forma predeterminada, se devuelve la ruta completa. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer la ruta.</li><li>FULL_PATH: *Opcional* Un valor booleano que determina si se devuelve la ruta completa. Si se establece en false, solo se devuelve el final de la ruta.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_query_str | Devuelve la cadena de consulta de una dirección URL determinada. | <ul><li>URL: **Requerido** La URL desde la que intenta obtener la cadena de consulta.</li><li>ANCLAJE: **Requerido** Determina qué se hará con el anclaje en la cadena de consulta. Puede ser uno de los tres valores: &quot;conservar&quot;, &quot;eliminar&quot; o &quot;anexar&quot;.<br><br>Si el valor es &quot;keep&quot;, el anclaje se adjuntará al valor devuelto.<br>Si el valor es &quot;remove&quot;, el anclaje se eliminará del valor devuelto.<br>Si el valor es &quot;append&quot;, el anclaje se devolverá como un valor independiente.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/There?name= &#x200B; ferret#nariz&quot;, &quot;keep&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/There?name= &#x200B; ferret#note&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com ›:8042/over/here?name ferret#nariz&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Funciones de fecha y hora

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla. Puede encontrar más información sobre la función `date` en la [guía de la función date](./dates.md).

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | Recupera la hora actual. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Recupera la hora Unix actual. |  | timestamp() | timestamp() | 1571850624571 |
| format | Da formato a la fecha de entrada según un formato especificado. | <ul><li>FECHA: **Requerido** La fecha de entrada, como objeto ZonianDateTime, a la que desea dar formato.</li><li>FORMATO: **Requerido** El formato al que desea cambiar la fecha.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;aaaa-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Convierte una marca de hora en una cadena de fecha según el formato especificado. | <ul><li>MARCA DE TIEMPO: **Requerido** La marca de tiempo a la que desea dar formato. Esto se escribe en milisegundos.</li><li>FORMATO: **Requerido** El formato al que desea cambiar la marca de tiempo.</li></ul> | dformat &#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23 de Octubre del 2019 11:24&quot; |
| date | Convierte una cadena de fecha en un objeto ZonianDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li><li>FORMATO: **Requerido** La cadena que representa el formato de la fecha.</li><li>DEFAULT_DATE: **Requerido** La fecha predeterminada devuelta, si la fecha proporcionada es nula.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| date | Convierte una cadena de fecha en un objeto ZonianDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li><li>FORMATO: **Requerido** La cadena que representa el formato de la fecha.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date | Convierte una cadena de fecha en un objeto ZonianDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Recupera las partes de la fecha. Se admiten los siguientes valores de componentes: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br> 11/>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;week&quot;<br>&quot;dw&quot; a20/>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;&lt;a22 8/>&quot;seconds&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;miliseconds&quot;<br>&quot;ms&quot;<br><br><br> | <ul><li>COMPONENTE: **Requerido** Una cadena que representa la parte de la fecha. </li><li>FECHA: **Requerido** La fecha, en un formato estándar.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Reemplaza un componente en una fecha determinada. Se aceptan los siguientes componentes: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;&lt;a11//>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;seconds&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br> | <ul><li>COMPONENTE: **Requerido** Una cadena que representa la parte de la fecha. </li><li>VALOR: **Requerido** El valor que se debe configurar para el componente en una fecha determinada.</li><li>FECHA: **Requerido** La fecha, en un formato estándar.</li></ul> | set_date_part &#x200B;(COMPONENTE, VALOR, FECHA) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Crea una fecha a partir de partes. Esta función también se puede inducir utilizando make_timestamp. | <ul><li>AÑO: **Obligatorio** El año, escrito con cuatro dígitos.</li><li>MES: **Requerido** El mes. Los valores permitidos son del 1 al 12.</li><li>DÍA: **Requerido** El día. Los valores permitidos son del 1 al 31.</li><li>HORA: **Requerido** La hora. Los valores permitidos son de 0 a 23.</li><li>MINUTO: **Requerido** El minuto. Los valores permitidos son de 0 a 59.</li><li>NANOSECOND: **Requerido** Los valores de nanosegundo. Los valores permitidos son 0 a 9999999999.</li><li>ZONA HORARIA: **Requerido** La zona horaria de la fecha.</li></ul> | make_date_time &#x200B;(AÑO, MES, DÍA, HORA, MINUTO, SEGUNDO, NANOSECOND, ZONA HORARIA) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Convierte una fecha de cualquier zona horaria en una fecha UTC. | <ul><li>FECHA: **Requerido** La fecha que está intentando convertir.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Convierte una fecha de una zona horaria a otra. | <ul><li>FECHA: **Requerido** La fecha que está intentando convertir.</li><li>ZONA: **Requerido** La zona horaria a la que intenta convertir la fecha.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

&#x200B;

### Jerarquías - Objetos

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Devuelve el tamaño de la entrada. | <ul><li>ENTRADA: **Requerido** El objeto del que está intentando encontrar el tamaño.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Comprueba si un objeto está vacío o no. | <ul><li>ENTRADA: **Requerido** El objeto que está intentando comprobar está vacío.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | Crea una lista de objetos. | <ul><li>ENTRADA: **Requerido** Una agrupación de pares de claves y matrices.</li></ul> | array_to_object(INPUT) | need sample | need sample |
| to_object | Crea un objeto basado en los pares clave/valor plano dados. | <ul><li>ENTRADA: **Requerido** Una lista plana de pares clave/valor.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crea un objeto a partir de la cadena de entrada. | <ul><li>CADENA: **Requerido** La cadena que se está analizando para crear un objeto.</li><li>VALUE_DELIMITER: *Opcional* El delimitador que separa un campo del valor. El delimitador predeterminado es `:`.</li><li>FIELD_DELIMITER: *Opcional* El delimitador que separa los pares de valor de campo. El delimitador predeterminado es `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | teléfono - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Comprueba si el objeto existe dentro de los datos de origen. | <ul><li>ENTRADA: **Requerido** La ruta que se debe comprobar si existe dentro de los datos de origen.</li></ul> | is_set(INPUT) | is_set &#x200B;(&quot;evars.evar.field1&quot;) | true |
| anulación | Establece el valor del atributo en `null`. Debe utilizarse cuando no desee copiar el campo en el esquema de destino. |  | nullify() | nullify() | `null` |

### Jerarquías: matrices

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| coalesce | Devuelve el primer objeto no nulo de una matriz determinada. | <ul><li>ENTRADA: **Requerido** La matriz de la que desea encontrar el primer objeto no nulo.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;seconds&quot;) | &quot;first&quot; |
| first | Recupera el primer elemento de la matriz dada. | <ul><li>ENTRADA: **Requerido** La matriz de la que desea encontrar el primer elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera el último elemento de la matriz dada. | <ul><li>ENTRADA: **Requerido** La matriz de la que desea encontrar el último elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Agrega elementos al final de la matriz. | <ul><li>MATRIZ: **Requerido** La matriz a la que está agregando elementos.</li><li>VALORES: Los elementos que desea anexar a la matriz.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;] |
| join_array | Combina las matrices entre sí. | <ul><li>MATRIZ: **Requerido** La matriz a la que está agregando elementos.</li><li>VALORES: Las matrices que desee anexar a la matriz principal.</li></ul> | join_array &#x200B;(ARRAY, VALUES) | join_array &#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;] |
| to_array | Toma una lista de entradas y la convierte en una matriz. | <ul><li>INCLUDE_NULLS: **Requerido** Un valor booleano para indicar si se deben incluir o no números en la matriz de respuestas.</li><li>VALORES: **Requerido** Los elementos que se van a convertir en una matriz.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Operadores lógicos

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decode | Si se da una clave y una lista de pares de valor clave acoplados como una matriz, la función devuelve el valor si se encuentra una clave o devuelve un valor predeterminado si está presente en la matriz. | <ul><li>CLAVE: **Requerido** La clave a buscar coincidencias.</li><li>OPCIONES: **Requerido** Una matriz plana de pares clave/valor. Opcionalmente, se puede colocar un valor predeterminado al final.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Si el stateCode dado es &quot;ca&quot;, &quot;California&quot;.<br>Si el stateCode dado es &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Si stateCode no coincide con lo siguiente, &quot;N/D&quot;. |
| iif | Evalúa una expresión booleana determinada y devuelve el valor especificado en función del resultado. | <ul><li>EXPRESIÓN: **Requerido** La expresión booleana que se está evaluando.</li><li>TRUE_VALUE: **Required** El valor que se devuelve si la expresión se evalúa como verdadera.</li><li>FALSE_VALUE: **Required** El valor que se devuelve si la expresión se evalúa como falsa.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### Agregación

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Devuelve el mínimo de los argumentos dados. Utiliza el orden natural. | <ul><li>OPCIONES: **Requerido** Uno o más objetos que se pueden comparar entre sí.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Devuelve el máximo de los argumentos dados. Utiliza el orden natural. | <ul><li>OPCIONES: **Requerido** Uno o más objetos que se pueden comparar entre sí.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Conversiones de tipo

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Convierte una cadena en BigInteger. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 100000,34 |
| to_decimal | Convierte una cadena en Double. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en un valor Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Convierte una cadena en flotante. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en flotante.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Convierte una cadena en un entero. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en un entero.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### Funciones JSON

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Deserialice el contenido JSON de la cadena dada. | <ul><li>CADENA: **Requerido** La cadena JSON que se va a deserializar.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}) | Un objeto que representa el JSON. |

### Operaciones especiales

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Genera un ID pseudo-aleatorio. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

### Funciones de agente de usuario

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Extrae el nombre del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrae la versión principal del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS5 |
| ua_os_version | Extrae la versión del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrae el nombre y la versión del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS5.1.1 |
| ua_agent_version | Extrae la versión del agente de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extrae el nombre del agente y la versión principal de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrae el nombre del agente de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrae la clase del dispositivo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Phone |