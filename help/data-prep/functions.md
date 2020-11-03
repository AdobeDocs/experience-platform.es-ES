---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;mapping fields;mapping functions;
solution: Experience Platform
title: Funciones de preparación de datos
topic: overview
description: Este documento presenta las funciones de asignación utilizadas con la preparación de datos.
translation-type: tm+mt
source-git-commit: 6deb8f5e11b87550601679f06c8445d90fd22709
workflow-type: tm+mt
source-wordcount: '3459'
ht-degree: 3%

---


# Funciones de preparación de datos

Las funciones de preparación de datos se pueden utilizar para calcular y calcular valores en función de lo que se introduzca en los campos de origen.

## Campos

Un nombre de campo puede ser cualquier identificador legal: una secuencia de letras y dígitos Unicode de longitud ilimitada, que comienza con una letra, el signo de dólar (`$`) o el carácter de subrayado (`_`). Los nombres de las variables también distinguen entre mayúsculas y minúsculas.

Si un nombre de campo no sigue esta convención, el nombre del campo debe estar ajustado con `${}`. Por ejemplo, si el nombre del campo es &quot;Nombre&quot; o &quot;Nombre.Nombre&quot;, el nombre debe ajustarse como `${First Name}` o `${First.Name}` respectivamente.

Además, los nombres de campo son **cualquiera** de las siguientes palabras clave reservadas, debe estar ajustado con `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Se puede acceder a los datos de los subcampos mediante la notación de puntos. Por ejemplo, si hay un `name` objeto, para acceder al `firstName` campo, utilice `name.firstName`.

## Lista de funciones

Las siguientes tablas lista todas las funciones de asignación admitidas, incluidas las expresiones de muestra y sus resultados.

### Funciones de cadena

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Concatena las cadenas dadas. | <ul><li>CADENA: Cadenas que se concatenarán.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explosionar | Divide la cadena según un regex y devuelve una matriz de partes. Opcionalmente, puede incluir regex para dividir la cadena. De forma predeterminada, la división se resuelve en &quot;,&quot;. | <ul><li>CADENA: **Requerido** La cadena que se debe dividir.</li><li>REGEX: *Opcional* La expresión normal que se puede utilizar para dividir la cadena.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Devuelve la ubicación/índice de una subcadena. | <ul><li>ENTRADA: **Requerido** La cadena que se está buscando.</li><li>SUBCADENA: **Requerido** La subcadena que se busca dentro de la cadena.</li><li>INICIO_POSITION: *Opcional* La ubicación de dónde se va a buscar en la cadena con el inicio.</li><li>OCURRENCIA: *Opcional* La enésima incidencia que se va a buscar desde la posición de inicio. De forma predeterminada, se establece en 1. </li></ul> | instr(ENTRADA, SUBCADENA, INICIO_POSICIÓN, OCURRENCIA) | instr(&quot;adobe`<span>`.com&quot;, &quot;com&quot;) | 6 |
| sustitutor | Reemplaza la cadena de búsqueda si está presente en la cadena original. | <ul><li>ENTRADA: **Requerido** La cadena de entrada.</li><li>TO_FIND: **Requerido** La cadena que se busca dentro de la entrada.</li><li>TO_REPLACE: **Requerido** La cadena que reemplazará el valor dentro de &quot;TO_FIND&quot;.</li></ul> | remplacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;Esto es una cadena re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Ésta es una prueba de reemplazo de cadena&quot; |
| substr | Devuelve una subcadena de una longitud determinada. | <ul><li>ENTRADA: **Requerido** La cadena de entrada.</li><li>INICIO_INDEX: **Requerido** Índice de la cadena de entrada donde inicio la subcadena.</li><li>LENGTH: **Required** The length of the substring.</li></ul> | substr(INPUT, INICIO_INDEX, LONGITUD) | substr(&quot;Esta es una prueba de subcadena&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Convierte una cadena en minúsculas. | <ul><li>ENTRADA: **Requerido** La cadena que se convertirá a minúsculas.</li></ul> | lower (ENTRADA) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| superior /<br>ucase | Convierte una cadena en mayúsculas. | <ul><li>ENTRADA: **Requerido** La cadena que se convertirá en mayúscula.</li></ul> | superior(ENTRADA) | top(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HOLA&quot; |
| split | Divide una cadena de entrada en un separador. | <ul><li>ENTRADA: **Requerido** La cadena de entrada que se va a dividir.</li><li>SEPARADOR: **Requerido** La cadena que se utiliza para dividir la entrada.</li></ul> | split(ENTRADA, SEPARADOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Une una lista de objetos mediante el separador. | <ul><li>SEPARADOR: **Requerido** La cadena que se utilizará para unir los objetos.</li><li>OBJETOS: **Requerido** Matriz de cadenas que se unirán.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hola mundo&quot; |
| lpad | Pade el lado izquierdo de una cadena con la otra cadena dada. | <ul><li>ENTRADA: **Requerido** La cadena que se va a rellenar. Esta cadena puede ser nula.</li><li>RECUENTO: **Requerido** El tamaño de la cadena que se va a añadir.</li><li>AGREGAR: **Requerido** La cadena con la que se rellena la entrada. Si es nulo o está vacío, se tratará como un solo espacio.</li></ul> | lpad(ENTRADA, RECUENTO, ADICIÓN) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Pade el lado derecho de una cadena con la otra cadena dada. | <ul><li>ENTRADA: **Requerido** La cadena que se va a rellenar. Esta cadena puede ser nula.</li><li>RECUENTO: **Requerido** El tamaño de la cadena que se va a añadir.</li><li>AGREGAR: **Requerido** La cadena con la que se rellena la entrada. Si es nulo o está vacío, se tratará como un solo espacio.</li></ul> | rpad(ENTRADA, RECUENTO, ADICIÓN) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtiene los primeros caracteres &quot;n&quot; de la cadena dada. | <ul><li>CADENA: **Requerido** La cadena para la que se obtienen los primeros caracteres &quot;n&quot;.</li><li>RECUENTO: **** RequeridoCaracteres &quot;n&quot; que desea obtener de la cadena.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Obtiene los últimos caracteres &quot;n&quot; de la cadena dada. | <ul><li>CADENA: **Requerido** La cadena para la que se obtienen los últimos caracteres &quot;n&quot;.</li><li>RECUENTO: **** RequeridoCaracteres &quot;n&quot; que desea obtener de la cadena.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Quita el espacio en blanco del principio de la cadena. | <ul><li>CADENA: **Requerido** La cadena de la que desea quitar el espacio en blanco.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Quita el espacio en blanco del final de la cadena. | <ul><li>CADENA: **Requerido** La cadena de la que desea quitar el espacio en blanco.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Quita el espacio en blanco del principio y del final de la cadena. | <ul><li>CADENA: **Requerido** La cadena de la que desea quitar el espacio en blanco.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| es igual que | Compara dos cadenas para confirmar si son iguales. Esta función distingue entre mayúsculas y minúsculas. | <ul><li>STRING1: **Requerido** La primera cadena que desea comparar.</li><li>STRING2: **Requerido** La segunda cadena que desea comparar.</li></ul> | STRING1.equals(STRING2) | &quot;string1&quot;.equals(&quot;STRING1) | false |
| igual a IgnoreCase | Compara dos cadenas para confirmar si son iguales. Esta función **no distingue entre** mayúsculas y minúsculas. | <ul><li>STRING1: **Requerido** La primera cadena que desea comparar.</li><li>STRING2: **Requerido** La segunda cadena que desea comparar.</li></ul> | STRING1.equalsIgnoreCase(STRING2) | &quot;string1&quot;.equalsIgnoreCase(&quot;STRING1) | true |

### Funciones de hash

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Toma una entrada y produce un valor hash mediante el algoritmo hash seguro 1 (SHA-1). | <ul><li>ENTRADA: **Requerido** El texto sin formato con hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha1(ENTRADA, JUEGO DE ENTRADAS) | sha1(&quot;mi texto&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Toma una entrada y produce un valor hash mediante el algoritmo hash seguro 256 (SHA-256). | <ul><li>ENTRADA: **Requerido** El texto sin formato con hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha256(ENTRADA, ENTRADA) | sha256(&quot;mi texto&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Toma una entrada y produce un valor hash mediante el algoritmo hash seguro 512 (SHA-512). | <ul><li>ENTRADA: **Requerido** El texto sin formato con hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | sha512(ENTRADA, JUEGO DE ENTRADAS) | sha512(&quot;mi texto&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Toma una entrada y produce un valor hash mediante MD5. | <ul><li>ENTRADA: **Requerido** El texto sin formato con hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII. </li></ul> | md5(ENTRADA, JUEGO DE ENTRADAS) | md5(&quot;mi texto&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Toma una entrada utiliza un algoritmo de comprobación de redundancia cíclica (CRC) para producir un código cíclico de 32 bits. | <ul><li>ENTRADA: **Requerido** El texto sin formato con hash.</li><li>CHARSET: *Opcional* El nombre del conjunto de caracteres. Los valores posibles son UTF-8, UTF-16, ISO-8859-1 y US-ASCII.</li></ul> | crc32(ENTRADA, CONJUNTO DE ENTRADAS) | crc32(&quot;mi texto&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### Funciones URL

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | Devuelve el protocolo de la dirección URL dada. Si la entrada no es válida, devuelve null. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer el protocolo.</li></ul> | get_url_protocol(URL) | get_url_protocol(&quot;https://platform.adobe.com/home&quot;) | https |
| get_url_host | Devuelve el host de la dirección URL dada. Si la entrada no es válida, devuelve null. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer el host.</li></ul> | get_url_host(URL) | get_url_host(&quot;https://platform.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Devuelve el puerto de la dirección URL dada. Si la entrada no es válida, devuelve null. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer el puerto.</li></ul> | get_url_port(URL) | get_url_port(&quot;sftp://example.com//home/joe/employee.csv&quot;) | 22 |
| get_url_path | Devuelve la ruta de la dirección URL dada. De forma predeterminada, se devuelve la ruta completa. | <ul><li>URL: **Requerido** La dirección URL desde la que se debe extraer la ruta.</li><li>FULL_PATH: *Opcional* Un valor booleano que determina si se devuelve la ruta completa. Si se establece en false, solo se devuelve el final de la ruta.</li></ul> | get_url_path(URL, FULL_PATH) | get_url_path(&quot;sftp://example.com//home/joe/employee.csv&quot;) | &quot;//home/joe/employee.csv&quot; |
| get_url_consulta_str | Devuelve la cadena de consulta de una dirección URL determinada. | <ul><li>URL: **Requerido** La URL desde la que intenta obtener la cadena de consulta.</li><li>ANCLAJE: **Requerido** Determina qué se hará con el anclaje en la cadena de consulta. Puede ser uno de los tres valores: &quot;retener&quot;, &quot;eliminar&quot; o &quot;anexar&quot;.<br><br>Si el valor es &quot;keep&quot;, el anclaje se adjuntará al valor devuelto.<br>Si el valor es &quot;remove&quot;, el anclaje se eliminará del valor devuelto.<br>Si el valor es &quot;append&quot;, el anclaje se devolverá como un valor independiente.</li></ul> | get_url_consulta_str(URL, ANCHOR) | get_url_consulta_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;keep&quot;)<br>get_url_consulta_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;remove&quot;)<br>get_url_consulta_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Funciones de fecha y hora

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | Recupera la hora actual. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Recupera la hora Unix actual. |  | timestamp() | timestamp() | 1571850624571 |
| format | Da formato a la fecha de entrada según un formato especificado. | <ul><li>FECHA: **Requerido** La fecha de entrada, como objeto ZonianDateTime, a la que se desea dar formato.</li><li>FORMATO: **Requerido** El formato al que desea cambiar la fecha.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;aaaa-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Convierte una marca de hora en una cadena de fecha según un formato especificado. | <ul><li>MARCA DE HORA: **Requerido** La marca de tiempo a la que desea dar formato. Esto se escribe en milisegundos.</li><li>FORMATO: **Requerido** El formato al que desea cambiar la marca de tiempo.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-Oct-2019 11:24&quot; |
| date | Convierte una cadena de fecha en un objeto ZonianDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li><li>FORMATO: **Requerido** La cadena que representa el formato de la fecha.</li><li>DEFAULT_DATE: **Requerido** La fecha predeterminada devuelta, si la fecha proporcionada es nula.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;, now())) | &quot;2019-10-23T11:24Z&quot; |
| date | Convierte una cadena de fecha en un objeto ZonianDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li><li>FORMATO: **Requerido** La cadena que representa el formato de la fecha.</li></ul> | date(FECHA, FORMATO) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date | Convierte una cadena de fecha en un objeto ZonianDateTime (formato ISO 8601). | <ul><li>FECHA: **Requerido** La cadena que representa la fecha.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Recupera las partes de la fecha. Se admiten los siguientes valores de componente: <br><br>&quot;year&quot;<br>&quot;aaaaaa&quot;<br>&quot;yy&quot;<br><br>&quot;trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;mes&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;día del año&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;dy&quot;y&quot;&quot;día&quot;d&quot;d&quot;semana&quot;ww&quot;w&quot;w&quot;día de la semana&quot;día de la semana&quot;dw&quot;w&quot;ea&quot;hh&quot;h&quot;h&quot;hh&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot; &quot;hh24&quot;&quot;hh12&quot;&quot;minuto&quot;&quot;mi&quot;&quot;n&quot;&quot;segundo&quot;&quot;ss&quot;&quot;s&quot;&quot;milisegundo&quot;&quot;ms&quot;&quot; | <ul><li>COMPONENTE: **Requerido** Una cadena que representa la parte de la fecha. </li><li>FECHA: **Requerido** La fecha, en un formato estándar.</li></ul> | date_part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Reemplaza un componente en una fecha determinada. Se aceptan los siguientes componentes: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br><br><br><br><br><br><br><br><br>&quot;hh&quot;minuto&quot;&quot;mi&quot;&quot;s&quot;ss&quot;s&quot;&quot;&quot; | <ul><li>COMPONENTE: **Requerido** Una cadena que representa la parte de la fecha. </li><li>VALOR: **Requerido** El valor que se va a establecer para el componente en una fecha determinada.</li><li>FECHA: **Requerido** La fecha, en un formato estándar.</li></ul> | set_date_part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Crea una fecha a partir de partes. Esta función también se puede inducir con make_timestamp. | <ul><li>AÑO: **Requerido** El año, escrito en cuatro dígitos.</li><li>MES: **Requerido** El mes. Los valores permitidos son del 1 al 12.</li><li>DÍA: **Requerido** El día. Los valores permitidos son del 1 al 31.</li><li>HORA: **Requerido** La hora. Los valores permitidos son 0 a 23.</li><li>MINUTO: **Requerido** El minuto. Los valores permitidos son 0 a 59.</li><li>NANOSEGUND: **Requerido** Los valores nanosegundos. Los valores permitidos son 0 a 9999999999.</li><li>ZONA HORARIA: **Requerido** La zona horaria de la fecha y hora.</li></ul> | make_date_time(AÑO, MES, DÍA, HORA, MINUTO, SEGUNDO, NANOSECOND, ZONA HORARIA) | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;América/Los Ángeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Convierte una fecha de cualquier zona horaria en una fecha en UTC. | <ul><li>FECHA: **Requerido** La fecha en la que está intentando convertir.</li></ul> | zone_date_to_utc(DATE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Convierte una fecha de una zona horaria a otra. | <ul><li>FECHA: **Requerido** La fecha en la que está intentando convertir.</li><li>ZONA: **Requerido** El huso horario al que intenta convertir la fecha.</li></ul> | zone_date_to_zone(DATE, ZONE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

### Jerarquías - Objetos

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Devuelve el tamaño de la entrada. | <ul><li>ENTRADA: **Requerido** El objeto del que está intentando encontrar el tamaño.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Comprueba si un objeto está vacío o no. | <ul><li>ENTRADA: **Requerido** El objeto que está intentando comprobar está vacío.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | Crea una lista de objetos. | <ul><li>ENTRADA: **Requerido** Agrupación de pares de claves y matrices.</li></ul> | array_to_object(INPUT) | necesita muestra | necesita muestra |
| to_object | Crea un objeto basado en los pares clave/valor planos dados. | <ul><li>ENTRADA: **Requerido** Una lista plana de pares clave/valor.</li></ul> | to_object(INPUT) | to_object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crea un objeto a partir de la cadena de entrada. | <ul><li>CADENA: **Requerido** La cadena que se está analizando para crear un objeto.</li><li>VALUE_DELIMITER: *Opcional* El delimitador que separa un campo del valor. The default delimiter is `:`.</li><li>FIELD_DELIMITER: *Opcional* El delimitador que separa los pares de valor de campo. The default delimiter is `,`.</li></ul> | str_to_object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | teléfono - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Comprueba si el objeto existe dentro de los datos de origen. | <ul><li>ENTRADA: **Requerido** La ruta que se debe comprobar si existe dentro de los datos de origen.</li></ul> | is_set(INPUT) | is_set(&quot;evars.evar.field1&quot;) | true |
| anular | Define el valor del atributo en `null`. Debe utilizarse cuando no desee copiar el campo en el esquema de destinatario. |  | nullify() | nullify() | `null` |

### Jerarquías: matrices

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| fusionarse | Devuelve el primer objeto no nulo de una matriz determinada. | <ul><li>ENTRADA: **Requerido** La matriz de la que desea buscar el primer objeto no nulo.</li></ul> | combinación(ENTRADA) | coalesce(null, null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Recupera el primer elemento de la matriz dada. | <ul><li>ENTRADA: **Requerido** La matriz de la que desea encontrar el primer elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera el último elemento de la matriz dada. | <ul><li>ENTRADA: **Requerido** La matriz de la que desea encontrar el último elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Toma una lista de entradas y la convierte en una matriz. | <ul><li>INCLUDE_NULLS: **Requerido** Un valor booleano que indica si se deben incluir o no números en la matriz de respuestas.</li><li>VALORES: **Requerido** Los elementos que se van a convertir en una matriz.</li></ul> | to_array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Operadores lógicos

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decode | Dada una clave y una lista de pares de valor clave acoplados como una matriz, la función devuelve el valor si se encuentra la clave o devuelve un valor predeterminado si está presente en la matriz. | <ul><li>CLAVE: **Requerido** La clave que se debe coincidir.</li><li>OPTIONS: **Requerido** Matriz acoplada de pares clave/valor. Opcionalmente, se puede colocar un valor predeterminado al final.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/D&quot;) | Si el stateCode proporcionado es &quot;ca&quot;, &quot;California&quot;.<br>Si el stateCode proporcionado es &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Si stateCode no coincide con lo siguiente, &quot;N/D&quot;. |
| iif | Evalúa una determinada expresión booleana y devuelve el valor especificado en función del resultado. | <ul><li>BOOLEAN_EXPRESIÓN: **Requerido** La expresión booleana que se está evaluando.</li><li>TRUE_VALUE: **Requerido** El valor que se devuelve si la expresión se evalúa como true.</li><li>FALSE_VALUE: **Requerido** El valor que se devuelve si la expresión se evalúa como false.</li></ul> | iif(BOOLEAN_EXPRESIÓN, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### Agregación

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Devuelve el mínimo de los argumentos dados. Utiliza ordenación natural. | <ul><li>OPTIONS: **Requerido** Uno o más objetos que se pueden comparar entre sí.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Devuelve el máximo de los argumentos dados. Utiliza ordenación natural. | <ul><li>OPTIONS: **Requerido** Uno o más objetos que se pueden comparar entre sí.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Conversiones de tipo

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Convierte una cadena en un BigInteger. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en un BigInteger.</li></ul> | to_bigint(STRING) | to_bigint(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | Convierte una cadena en un Doble. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en un Doble.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | Convierte una cadena en flotante. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en flotante.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | Convierte una cadena en un entero. | <ul><li>CADENA: **Requerido** La cadena que se va a convertir en un entero.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### Funciones JSON

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Deserialice el contenido JSON de la cadena dada. | <ul><li>CADENA: **Requerido** La cadena JSON que se va a deserializar.</li></ul> | json_to_object(STRING) | json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}) | Un objeto que representa el JSON. |

### Operaciones especiales

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Genera un ID seudoaleatorio. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c2063333 |

### Funciones de agente de usuario

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de muestra |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Extrae el nombre del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_name(USER_AGENT) | ua_os_name(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrae la versión principal del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_version_major(USER_AGENT) | ua_os_version_major(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrae la versión del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_version(USER_AGENT) | ua_os_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrae el nombre y la versión del sistema operativo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_os_name_version(USER_AGENT) | ua_os_name_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrae la versión del agente de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_version(USER_AGENT) | ua_agent_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extrae el nombre del agente y la versión principal de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_version_major(USER_AGENT) | ua_agent_version_major(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrae el nombre del agente de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_agent_name(USER_AGENT) | ua_agent_name(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrae la clase de dispositivo de la cadena del agente de usuario. | <ul><li>USER_AGENT: **Requerido** La cadena del agente de usuario.</li></ul> | ua_device_class(USER_AGENT) | ua_device_class(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 como Mac OS X) AppleWebKit/534.46 (KHTML, como Gecko) Versión/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Phone |