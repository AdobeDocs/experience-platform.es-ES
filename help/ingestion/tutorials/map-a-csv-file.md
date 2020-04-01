---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Asignación de un archivo CSV a un esquema XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# Asignación de un archivo CSV a un esquema XDM

Para poder transferir datos CSV a la plataforma de Adobe Experience, los datos deben asignarse a un esquema del modelo de datos de experiencia (XDM). Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario de la plataforma de experiencia.

Además, en el apéndice de este tutorial se proporciona más información sobre el uso de funciones [de](#mapping-functions)asignación.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Modelo de datos de experiencia (sistema XDM)](../../xdm/home.md): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
- [Ingesta](../batch-ingestion/overview.md)por lotes: El método mediante el cual Platform ingesta datos de los archivos de datos proporcionados por el usuario.

Este tutorial también requiere que ya haya creado un conjunto de datos para ingestar los datos de CSV. Para ver los pasos para crear un conjunto de datos en la interfaz de usuario, consulte el tutorial [de ingesta de](./ingest-batch-data.md)datos.

## Añadir datos

En la interfaz de usuario de la plataforma de experiencia, haga clic en **Flujos de trabajo** en el panel de navegación izquierdo y, a continuación, haga clic en **Asignar CSV al esquema** XDM. En el carril derecho que aparece, haga clic en **Iniciar**.

![](../images/tutorials/map-a-csv-file/workflow-tab.png)

Aparece el flujo de trabajo _Asignar CSV a esquema_ XDM, comenzando en el paso _Añadir datos_ .

![](../images/tutorials/map-a-csv-file/add-data.png)

Arrastre y suelte el archivo CSV en el espacio proporcionado o haga clic en **Examinar** para seleccionar un archivo directamente. Una vez cargado el archivo, aparece una sección de datos _de_ muestra que muestra las diez primeras filas de datos. Una vez que confirme que los datos se han cargado según lo esperado, haga clic en **Siguiente**.

![](../images/tutorials/map-a-csv-file/csv-added.png)

## Elegir un destino

Aparece el paso _Destino_ . En la lista proporcionada, seleccione el conjunto de datos en el que se van a ingestar los datos CSV y, a continuación, haga clic en **Siguiente**.

![](../images/tutorials/map-a-csv-file/select-destination.png)

## Asignar campos CSV a campos de esquema XDM

Aparece el paso _Asignación_ . Las columnas del archivo CSV se muestran en Campo __ de origen, con sus correspondientes campos de esquema XDM en Campo _de_ Destinatario. Los campos de destinatario no seleccionados están delineados en rojo.

Para asignar una columna CSV a un campo XDM, haga clic en el icono de esquema situado junto al campo de destinatario correspondiente de la columna.

![](../images/tutorials/map-a-csv-file/target-field-mapping.png)

Aparece la ventana _Seleccionar esquema_ . Aquí puede desplazarse por la estructura del esquema XDM y localizar el campo al que desea asignar la columna CSV. Haga clic en un campo XDM para seleccionarlo y, a continuación, haga clic en **Seleccionar**.

![](../images/tutorials/map-a-csv-file/xdm-field-selection.png)

La pantalla _Asignación_ vuelve a aparecer y el campo XDM seleccionado aparece ahora en Campo __ Destinatario.

![](../images/tutorials/map-a-csv-file/xdm-field-mapped.png)

Si no desea asignar una columna CSV concreta, puede eliminar la asignación haciendo clic en el icono **** Eliminar situado junto al campo destinatario. Si desea agregar una nueva asignación, haga clic en **Añadir nueva asignación** en la parte inferior de la lista.

![](../images/tutorials/map-a-csv-file/remove-or-add-mapping.png)

Al asignar campos, también puede incluir funciones para calcular valores en función de los campos de origen de entrada. Consulte la sección de funciones [de](#mapping-functions) asignación del apéndice para obtener más información.

Repita los pasos anteriores para continuar asignando columnas CSV a campos XDM. Una vez que haya terminado, haga clic en **Siguiente**.

![](../images/tutorials/map-a-csv-file/mapping-finish.png)

## Datos de entrada

Aparece el paso _Ingesta_ , que le permite revisar los detalles del archivo de origen y del conjunto de datos de destinatario. Haga clic en **Ingestar** para inicio de la ingesta de datos CSV. Según el tamaño del archivo CSV, este proceso puede tardar varios minutos. La pantalla se actualiza una vez completada la ingestión, lo que indica que la operación ha sido correcta o incorrecta. Click **Finish** to complete the workflow.

![](../images/tutorials/map-a-csv-file/ingest-data.png)

## Pasos siguientes

Siguiendo este tutorial, ha asignado correctamente un archivo CSV plano a un esquema XDM y lo ha ingerido en plataforma. Estos datos ahora pueden ser utilizados por los servicios de plataforma descendente, como el Perfil de clientes en tiempo real. Consulte la descripción general [del Perfil del cliente en tiempo](../../profile/home.md) real para obtener más información.

## Apéndice

La siguiente sección proporciona información adicional para asignar columnas CSV a campos XDM.

### Funciones de asignación

Determinadas funciones de asignación se pueden utilizar para calcular y calcular valores en función de lo que se introduzca en los campos de origen. Para utilizar una función, escríbala en Campo __ de origen con la sintaxis y las entradas adecuadas.

Por ejemplo, para concatenar campos CSV de **ciudad** y **país** y asignarlos al campo XDM de **ciudad** , establezca el campo de origen como `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

La siguiente tabla lista todas las funciones de asignación admitidas, incluidas las expresiones de muestra y sus resultados.

| Función | Descripción | expresión de muestra | Salida de muestra |
| -------- | ----------- | ----------------- | ------------- |
| concat | Concatena cadenas determinadas. | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explosionar | Divide la cadena según un regex y devuelve una matriz de partes. | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Devuelve la ubicación/índice de una subcadena. | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| sustitutor | Reemplaza la cadena de búsqueda si está presente en la cadena original. | replacestr(&quot;Esto es una cadena re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Ésta es una prueba de reemplazo de cadena&quot; |
| substr | Devuelve una subcadena de una longitud determinada. | substr(&quot;Esta es una prueba de subcadena&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Convierte una cadena en minúsculas. | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| superior /<br>ucase | Convierte una cadena en mayúsculas. | top(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HOLA&quot; |
| split | Divide una cadena de entrada en un separador. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Une una lista de objetos mediante el separador. | `join(" ", ["Hello", "world"]`) | &quot;Hola mundo&quot; |
| fusionarse | Devuelve el primer objeto no nulo de una lista determinada. | coalesce(null, null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| decode | Dada una clave y una lista de pares de valor clave acoplados como una matriz, la función devuelve el valor si se encuentra la clave o devuelve un valor predeterminado si está presente en la matriz. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;Versión 2&quot; |
| iif | Evalúa una determinada expresión booleana y devuelve el valor especificado en función del resultado. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| min | Devuelve el mínimo de los argumentos dados. Utiliza ordenación natural. | min(3, 1, 4) | 1 |
| max | Devuelve el máximo de los argumentos dados. Utiliza ordenación natural. | max(3, 1, 4) | 4 |
| first | Recupera el primer argumento dado. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera el último argumento dado. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | Genera un ID seudoaleatorio. | uuid()<br>guid() | {UNIQUE_ID} |
| now | Recupera la hora actual. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Recupera la hora Unix actual. | timestamp() | 1571850624571 |
| format | Da formato a la fecha de entrada según un formato especificado. | format({DATE}, &quot;aaaa-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Convierte una marca de hora en una cadena de fecha según un formato especificado. | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-Oct-2019 11:24&quot; |
| date | Convierte una cadena de fecha en un objeto ZonianDateTime (formato ISO 8601). | date(&quot;23-Oct-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Recupera las partes de la fecha. Se admiten los siguientes valores de componente: <br><br>&quot;<br>&quot;year&quot;<br>&quot;yyyy&quot;<br><br>&quot;yy&quot;<br>&quot;trimestre&quot;<br>&quot;qq&quot;<br><br>&quot;q&quot;<br>&quot;mes&quot;<br>&quot;mm&quot;<br><br>&quot;m&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;día del año&quot;&quot;dy&quot;y&quot;&quot;día&quot;dd&quot;d&quot;d&quot;semana&quot;u&quot;día de la semana&quot;&quot;dw&quot;hh&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;h&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;u&quot;ea&quot;ea&quot;u&quot;ea&quot;ea&quot;ea&quot;u&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;u&quot;ea&quot;ea&quot;u&quot;h&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;u&quot;h&quot;h&quot;h&quot;h&quot;h&quot;ea&quot;h&quot;ea&quot;ea&quot;ea&quot;ea&quot;u&quot;u&quot;h&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;h&quot;h&quot;ea&quot;u&quot;h&quot;ea&quot;ea&quot;h&quot;u&quot;ea&quot;h&quot;h&quot;h&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;ea&quot;u&quot;ea&quot;ea&quot;ea&quot;u&quot;ea&quot;ea&quot;ea&quot;&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minuto&quot;&quot;mi&quot;&quot;n&quot;&quot;segundo&quot;&quot;ss&quot;&quot;s&quot;&quot;milisegundo&quot;&quot;ms&quot;&quot; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Reemplaza un componente en una fecha determinada. Se aceptan los siguientes componentes: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br><br><br><br><br><br><br><br><br><br>&quot;hour&quot;hh&quot;minuto&quot;&quot;minuto&quot;&quot;mi&quot;&quot;&quot;segundo&quot;&quot;ss&quot;&quot;s&quot;&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Crea una fecha a partir de partes. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;América/Los Ángeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Devuelve la marca de tiempo actual. | current_timestamp() | 1571850624571 |
| current_date | Devuelve la fecha actual sin un componente de tiempo. | current_date() | &quot;18 de noviembre de 2019&quot; |