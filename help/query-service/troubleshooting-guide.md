---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;guía de solución de problemas;preguntas frecuentes;solución de problemas;
solution: Experience Platform
title: Guía de solución de problemas del servicio de consultas
description: Este documento contiene preguntas y respuestas comunes relacionadas con el servicio de consulta. Los temas incluyen, exportación de datos, herramientas de terceros y errores de PSQL.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '4383'
ht-degree: 1%

---

# [!DNL Query Service] guía de solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes sobre el servicio de consultas y proporciona una lista de códigos de error que se ven con más frecuencia al utilizar el servicio de consultas. Para preguntas y solución de problemas relacionados con otros servicios de Adobe Experience Platform, consulte la [Guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

La siguiente lista de respuestas a las preguntas más frecuentes se divide en las siguientes categorías:

- [General](#general)
- [Exportación de datos](#exporting-data)
- [Herramientas de terceros](#third-party-tools)
- [Errores de API PostgreSQL](#postgresql-api-errors)
- [Errores de API de REST](#rest-api-errors)

## Preguntas generales del servicio de consultas {#general}

Esta sección incluye información sobre rendimiento, límites y procesos.

### ¿Puedo desactivar la función de autocompletar en el Editor del servicio de consultas?

+++Nº respuesta El editor no admite actualmente la desactivación de la función de autocompletar.
+++

### ¿Por qué el Editor de consultas a veces se vuelve lento cuando escribo una consulta?

+++Respuesta Una posible causa es la función de autocompletar. La función procesa ciertos comandos de metadatos que ocasionalmente pueden ralentizar el editor durante la edición de consultas.
+++

### ¿Puedo usar [!DNL Postman] para la API del servicio de consulta?

+++Respuesta Sí, puede visualizar e interactuar con todos los servicios de API de Adobe mediante [!DNL Postman] (una aplicación gratuita de terceros). Observe el [[!DNL Postman] guía de configuración](https://video.tv.adobe.com/v/28832) para obtener instrucciones paso a paso sobre cómo configurar un proyecto en la consola de Adobe Developer y adquirir todas las credenciales necesarias para su uso con [!DNL Postman]. Consulte la documentación oficial para [directrices sobre inicio, ejecución y uso compartido [!DNL Postman] colecciones](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### ¿Hay un límite en el número máximo de filas devueltas desde una consulta a través de la interfaz de usuario?

+++Respuesta Sí, el servicio de consulta aplica internamente un límite de 50 000 filas a menos que se especifique un límite explícito externamente. Consulte las directrices sobre [ejecución de consulta interactiva](./best-practices/writing-queries.md#interactive-query-execution) para obtener más información.
+++

### ¿Puedo utilizar consultas para actualizar filas?

+++Respuesta En consultas por lotes, no se admite la actualización de una fila dentro del conjunto de datos.
+++

### ¿Existe un límite de tamaño de datos para el resultado resultante de una consulta?

+++Nº respuesta No hay límite en el tamaño de los datos, pero hay un límite de tiempo de espera de consulta de 10 minutos desde una sesión interactiva. Si la consulta se ejecuta como una CTAS por lotes, no se aplica un tiempo de espera de 10 minutos. Consulte las directrices sobre [ejecución de consulta interactiva](./best-practices/writing-queries.md#interactive-query-execution) para obtener más información.
+++

### ¿Cómo puedo evitar el límite en el número de salida de filas de una consulta SELECT?

+++Respuesta Para evitar el límite de filas de salida, aplique &quot;LIMIT 0&quot; en la consulta. Por ejemplo:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### ¿Cómo puedo evitar que mis consultas se agoten en 10 minutos?

+++Respuesta Se recomiendan una o más de las siguientes soluciones en caso de que se agote el tiempo de espera de las consultas.

- [Convertir la consulta en una consulta CTAS](./sql/syntax.md#create-table-as-select) y programe la ejecución. La programación de una ejecución puede realizarse [a través de la interfaz de usuario](./ui/user-guide.md#scheduled-queries) o [API](./api/scheduled-queries.md#create).
- Ejecute la consulta en un fragmento de datos más pequeño aplicando [condiciones de filtro](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Ejecutar el comando EXPLAIN](./sql/syntax.md#explain) para recopilar más detalles.
- Revise las estadísticas de los datos dentro del conjunto de datos.
- Convierta la consulta en un formulario simplificado y vuelva a ejecutarse utilizando [declaraciones preparadas](./sql/prepared-statements.md).
+++

### ¿Hay algún problema o impacto en el rendimiento del servicio de consulta si se ejecutan varias consultas simultáneamente?

+++Nº respuesta El servicio de consulta tiene una capacidad de escalado automático que garantiza que las consultas simultáneas no tengan ningún impacto significativo en el rendimiento del servicio.
+++

### ¿Puedo usar palabras clave reservadas como nombre de columna?

+++Respuesta Hay ciertas palabras clave reservadas que no se pueden usar como nombres de columna, como, `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. Si desea utilizar estas palabras clave, debe omitir estas columnas.
+++

### ¿Cómo encuentro un nombre de columna de un conjunto de datos jerárquico?

+++Respuesta Los siguientes pasos describen cómo mostrar una vista tabular de un conjunto de datos a través de la interfaz de usuario, incluidos todos los campos y columnas anidados en un formulario acoplado.

- Después de iniciar sesión en el Experience Platform, seleccione **[!UICONTROL Conjuntos de datos]** en la navegación izquierda de la interfaz de usuario a la que navegar [!UICONTROL Conjuntos de datos] tablero.
- Los conjuntos de datos [!UICONTROL Examinar] se abre. Puede utilizar la barra de búsqueda para restringir las opciones disponibles. Seleccione un conjunto de datos de la lista mostrada.

![El tablero Conjuntos de datos en la interfaz de usuario de Platform con la barra de búsqueda y un conjunto de datos resaltados.](./images/troubleshooting/dataset-selection.png)

- La variable [!UICONTROL Actividad de conjuntos de datos] se abre. Select **[!UICONTROL Vista previa del conjunto de datos]** para abrir un cuadro de diálogo del esquema XDM y la vista tabular de los datos acoplados del conjunto de datos seleccionado. Encontrará más detalles en la [vista previa de la documentación de un conjunto de datos](../catalog/datasets/user-guide.md#preview-a-dataset)

![La pestaña Actividad del conjunto de datos del tablero Conjuntos de datos con la vista previa del conjunto de datos resaltada.](./images/troubleshooting/dataset-preview.png)

- Seleccione cualquier campo del esquema para mostrar su contenido en una columna plana. El nombre de la columna se muestra encima de su contenido en el lado derecho de la página. Debe copiar este nombre para utilizarlo para consultar este conjunto de datos.

![Esquema XDM y vista tabular de los datos acoplados. El nombre de columna de un conjunto de datos anidado se resalta en la interfaz de usuario.](./images/troubleshooting/column-name.png)

Consulte la documentación para obtener una guía completa sobre [cómo trabajar con estructuras de datos anidadas](./best-practices/nested-data-structures.md) con el Editor de consultas o un cliente de terceros.
+++

### ¿Cómo acelero una consulta en un conjunto de datos que contiene matrices?

+++Respuesta Para mejorar el rendimiento de las consultas en conjuntos de datos que contienen matrices, debe [explotar la matriz](https://spark.apache.org/docs/latest/api/sql/index.html#explode) como [Consulta CTAS](./sql/syntax.md#create-table-as-select) en tiempo de ejecución y, a continuación, explorarlo para obtener más información sobre las oportunidades de mejorar su tiempo de procesamiento.
+++

### ¿Por qué mi consulta CTAS sigue procesándose después de muchas horas solo para un pequeño número de filas?

+++Respuesta Si la consulta ha tardado mucho tiempo en un conjunto de datos muy pequeño, póngase en contacto con el servicio de atención al cliente.

Puede haber varios motivos para que una consulta se bloquee durante el procesamiento. Para determinar la causa exacta se requiere un análisis en profundidad caso por caso. [Contacto con el servicio de atención al cliente de Adobe](#customer-support) a ser este proceso.
+++

### ¿Cómo puedo ponerme en contacto con el servicio de atención al cliente de Adobe? {#customer-support}

+++Respuesta
[Una lista completa de los números de teléfono de asistencia al cliente de Adobe](https://helpx.adobe.com/ca/contact/phone.html) está disponible en la página de ayuda de Adobe. También puede encontrar ayuda en línea si completa los siguientes pasos:

- Vaya a [https://www.adobe.com/](https://www.adobe.com/) en el explorador web.
- En el lado derecho de la barra de navegación superior, seleccione **[!UICONTROL Iniciar sesión]**.

![El sitio web de Adobe con el inicio de sesión resaltado.](./images/troubleshooting/adobe-sign-in.png)

- Utilice su Adobe ID y contraseña registrados con su licencia de Adobe.
- Select **[!UICONTROL Ayuda y asistencia]** en la barra de navegación superior.

![Menú desplegable superior de la barra de navegación con Ayuda y asistencia, Soporte empresarial y Contacto resaltado.](./images/troubleshooting/help-and-support.png)

Aparece un banner desplegable que contiene un [!UICONTROL Ayuda y asistencia] para obtener más información. Select **[!UICONTROL Contáctenos]** para abrir el asistente virtual del servicio de atención al cliente de Adobe, o seleccione **[!UICONTROL Asistencia para empresas]** para obtener ayuda dedicada para organizaciones grandes.
+++

### ¿Cómo implemento una serie secuencial de trabajos, sin ejecutar los trabajos posteriores si el trabajo anterior no se completa correctamente?

+++Answer La función de bloque anónimo permite encadenar una o más sentencias SQL que se ejecutan en secuencia. También permiten la opción de la gestión de excepciones.

Consulte la [documentación de bloque anónimo](./best-practices/anonymous-block.md) para obtener más información.
+++

### ¿Cómo implemento la atribución personalizada en el servicio de consulta?

+++Respuesta Existen dos formas de implementar la atribución personalizada:

1. Usar una combinación de [Funciones definidas por Adobe](./sql/adobe-defined-functions.md) para identificar si se satisfacen las necesidades de casos de uso.
1. Si la sugerencia anterior no satisface su caso de uso, debe utilizar una combinación de [funciones de ventana](./sql/adobe-defined-functions.md#window-functions). Las funciones de ventana observan todos los eventos de una secuencia. También le permiten revisar los datos históricos y se pueden utilizar en cualquier combinación.
+++

### ¿Puedo crear plantillas de mis consultas para que pueda reutilizarlas fácilmente?

+++Respuesta Sí, puede crear plantillas de consultas mediante el uso de instrucciones preparadas. Las instrucciones preparadas pueden optimizar el rendimiento y evitar el reanálisis repetido de una consulta. Consulte la [documentación sobre declaraciones preparadas](./sql/prepared-statements.md) para obtener más información.
+++

### ¿Cómo puedo recuperar los registros de errores para una consulta? {#error-logs}

+++Respuesta Para recuperar los registros de errores de una consulta específica, primero debe utilizar la API del servicio de consulta para recuperar los detalles del registro de consultas. La respuesta HTTP contiene los ID de consulta necesarios para investigar un error de consulta.

Utilice el comando GET para recuperar varias consultas. Puede encontrar información sobre cómo realizar una llamada a la API en la [documentación de llamadas de API de muestra](./api/queries.md#sample-api-calls).

Desde la respuesta, identifique la consulta que desea investigar y realice otra solicitud de GET utilizando su `id` valor. Las instrucciones completas se encuentran en la sección [recuperar una consulta por documentación de ID](./api/queries.md#retrieve-a-query-by-id).

Una respuesta correcta devuelve el estado HTTP 200 y contiene la variable `errors` matriz. La respuesta se ha abreviado para su brevedad.

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

La variable [Documentación de referencia de la API del servicio de consulta](https://www.adobe.io/experience-platform-apis/references/query-service/) proporciona más información sobre todos los extremos disponibles.
+++

### ¿Qué significa &quot;Error validando esquema&quot;?

+++Respuesta El mensaje &quot;Error al validar esquema&quot; significa que el sistema no puede localizar un campo dentro del esquema. Debe leer el documento de prácticas recomendadas para [organización de recursos de datos en Query Service](./best-practices/organize-data-assets.md) seguido de [Crear tabla como documentación seleccionada](./sql/syntax.md#create-table-as-select).

El siguiente ejemplo demuestra el uso de una sintaxis CTAS y un tipo de datos de estructura:

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### ¿Cómo proceso rápidamente los nuevos datos que llegan al sistema todos los días?

+++Responder A La [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) se puede utilizar para leer datos de forma incremental en una tabla basada en un ID de instantánea. Es ideal para usar con la variable [carga incremental](./best-practices/incremental-load.md) patrón de diseño que solo procesa la información en el conjunto de datos que se ha creado o modificado desde la última ejecución de carga. Como resultado, aumenta la eficacia del procesamiento y se puede utilizar tanto con el procesamiento de flujo continuo como por lotes.
+++

### ¿Por qué hay una diferencia entre los números mostrados en la interfaz de usuario del perfil y los números calculados a partir del conjunto de datos de exportación del perfil?

+++Respuesta Los números mostrados en el panel de perfiles son precisos desde la última instantánea. Los números generados en la tabla de exportación de perfiles dependen totalmente de la consulta de exportación. Como resultado, la consulta del número de perfiles que cumplen los requisitos para un segmento en particular es una causa común de esta discrepancia.

>[!NOTE]
>
>Las consultas incluyen datos históricos, mientras que la interfaz de usuario solo muestra los datos del perfil actual.

+++

### ¿Por qué devolvía mi consulta un subconjunto vacío y qué debería hacer?

+++Respuesta La causa más probable es que la consulta sea demasiado estrecha en cuanto al ámbito. Debe eliminar sistemáticamente una sección de la sección `WHERE` hasta que empiece a ver algunos datos.

También puede confirmar que el conjunto de datos contiene datos utilizando una consulta pequeña como:

```sql
SELECT count(1) FROM myTableName
```

+++

### ¿Puedo realizar una muestra de mis datos?

+++Respuesta Esta función es actualmente un trabajo en curso. Los detalles estarán disponibles en [notas de la versión](../release-notes/latest/latest.md) y a través de los cuadros de diálogo de la interfaz de usuario de Platform una vez que la función esté lista para su lanzamiento.
+++

### ¿Qué funciones de ayuda admite el servicio de consulta?

+++Answer Query Service proporciona varias funciones de ayuda SQL integradas para ampliar la funcionalidad SQL. Consulte el documento para obtener una lista completa de [Funciones SQL admitidas por el servicio de consultas](./sql/spark-sql-functions.md).
+++

### Son nativos [!DNL Spark SQL] funciones compatibles o son usuarios restringidos únicamente al envolvente [!DNL Spark SQL] funciones proporcionadas por Adobe?

+++Respuesta Hasta ahora, no todas las fuentes abiertas [!DNL Spark SQL] se han probado las funciones en los datos del lago de datos. Una vez probados y confirmados, se añadirán a la lista de admitidos. Consulte la [lista de admitidos [!DNL Spark SQL] funciones](./sql/spark-sql-functions.md) para comprobar la existencia de una función específica.
+++

### ¿Pueden los usuarios definir sus propias funciones definidas por el usuario (UDF) que se pueden usar en otras consultas?

+++Respuesta Debido a consideraciones de seguridad de los datos, no se permite la definición personalizada de campos definidos por el usuario.
+++

### ¿Qué debo hacer si falla mi consulta programada?

+++Respuesta Primero, compruebe los registros para averiguar los detalles del error. La sección Preguntas frecuentes de [búsqueda de errores dentro de los registros](#error-logs) proporciona más información sobre cómo hacerlo.

También debe consultar la documentación para obtener instrucciones sobre cómo realizar [consultas programadas en la interfaz de usuario](./ui/user-guide.md#scheduled-queries) y [la API](./api/scheduled-queries.md).

A continuación se muestra una lista de consideraciones para las consultas programadas al usar la variable [!DNL Query Editor]. No se aplican al [!DNL Query Service] API:<br/>Solo puede añadir una programación a una consulta que ya se haya creado, guardado y ejecutado.<br/>You **cannot** agregue una programación a una consulta parametrizada.<br/>Consultas programadas **cannot** contiene un bloque anónimo.<br/>Solo se puede programar **one** plantilla de consulta mediante la interfaz de usuario. Si desea agregar programaciones adicionales a una plantilla de consulta, deberá utilizar la API . Si ya se ha agregado una programación mediante la API , no podrá agregar más programaciones mediante la interfaz de usuario de .
+++

### ¿Qué significa el error &quot;Límite de sesión alcanzado&quot;?

+++Respuesta &quot;Límite de sesión alcanzado&quot; significa que se ha alcanzado el número máximo de sesiones del servicio de consulta permitidas para su organización. Conéctese con el administrador de Adobe Experience Platform de su organización.
+++

### ¿Cómo gestiona el registro de consultas las consultas relacionadas con un conjunto de datos eliminado?

+++Answer Query Service nunca elimina el historial de consultas. Esto significa que cualquier consulta que haga referencia a un conjunto de datos eliminado devolverá &quot;Ningún conjunto de datos válido&quot; como resultado.
+++

### ¿Cómo puedo obtener solo los metadatos de una consulta?

+++Respuesta Puede ejecutar una consulta que devuelva cero filas para obtener solo los metadatos como respuesta. Esta consulta de ejemplo devuelve solo los metadatos de la tabla especificada.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### ¿Cómo puedo iterar rápidamente en una consulta CTAS (Crear tabla como selección) sin materializarla?

+++Respuesta Puede crear tablas temporales para iterar y experimentar rápidamente en una consulta antes de materializarla para su uso. También puede utilizar tablas temporales para validar si una consulta funciona.

Por ejemplo, puede crear una tabla temporal:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

A continuación, puede utilizar la tabla temporal de la siguiente manera:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

+++

### ¿Cómo puedo cambiar la zona horaria a y desde una marca de tiempo UTC?

+++Answer Adobe Experience Platform mantiene los datos en formato UTC (hora universal coordinada). Un ejemplo del formato UTC es `2021-12-22T19:52:05Z`

El servicio de consulta admite funciones SQL integradas para convertir una marca de tiempo determinada a formato UTC y desde él. Ambas `to_utc_timestamp()` y `from_utc_timestamp()` Los métodos emplean dos parámetros: marca de tiempo y zona horaria.

| Parámetro | Descripción |
|-----------|---------------|
| Marca de tiempo | La marca de tiempo puede escribirse en formato UTC o en formato simple `{year-month-day}` formato. Si no se proporciona ninguna hora, el valor predeterminado es la medianoche de la mañana de un día determinado. |
| Zona horaria | La zona horaria se escribe en un `{continent/city})` formato. Debe ser uno de los códigos de zona horaria reconocidos, tal como se encuentran en la variable [base de datos TZ de dominio público](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Convertir a la marca de tiempo UTC

La variable `to_utc_timestamp()` interpreta los parámetros dados y los convierte **a la marca de tiempo de su zona horaria local** en formato UTC. Por ejemplo, la zona horaria de Seúl, Corea del Sur, es UTC/GMT +9 horas. Al proporcionar una marca de hora de solo fecha, el método utiliza un valor predeterminado de medianoche por la mañana. La marca de tiempo y la zona horaria se convierten al formato UTC desde la hora de esa región hasta la marca de tiempo UTC de su región local.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

La consulta devuelve una marca de tiempo en la hora local del usuario. En este caso, las 3 pm del día anterior, ya que Seúl tiene nueve horas de anticipación.

```
2021-08-30 15:00:00
```

Otro ejemplo: si la marca de tiempo dada era `2021-07-14 12:40:00.0` para el `Asia/Seoul` zona horaria, la marca de tiempo UTC devuelta sería `2021-07-14 03:40:00.0`

El resultado de la consola que se proporciona en la interfaz de usuario del servicio de consulta es un formato más legible por el ser humano:

```
8/30/2021, 3:00 PM
```

#### Convertir desde la marca de tiempo UTC

La variable `from_utc_timestamp()` interpreta los parámetros dados **desde la marca de tiempo de su zona horaria local** y proporciona la marca de tiempo equivalente de la región deseada en formato UTC. En el siguiente ejemplo, la hora es las 2:40 p.m. en la zona horaria local del usuario. La zona horaria de Seúl que se pasa como variable supera las nueve horas de la zona horaria local.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La consulta devuelve una marca de tiempo en formato UTC para la zona horaria transferida como parámetro. El resultado es nueve horas antes de la zona horaria que ejecutó la consulta.

```
8/31/2021, 11:40 PM
```

### ¿Cómo debo filtrar mis datos de series temporales?

+++Respuesta Al consultar con datos de series temporales, debe utilizar el filtro de marcas de hora siempre que sea posible para realizar un análisis más preciso.

>[!NOTE]
>
> La cadena de fecha **must** estar en formato `yyyy-mm-ddTHH24:MM:SS`.

A continuación se puede ver un ejemplo del uso del filtro de marca de tiempo:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### ¿Cómo utilizo correctamente el `CAST` operador para convertir mis marcas de hora en consultas SQL?

+++Respuesta Al usar la variable `CAST` para convertir una marca de tiempo, debe incluir ambas fechas **y** tiempo.

Por ejemplo, si falta el componente de tiempo, como se muestra a continuación, se producirá un error:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

El uso correcto de la variable `CAST` se muestra a continuación:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### ¿Debo usar caracteres comodín, como *, para obtener todas las filas de mis conjuntos de datos?

+++Respuesta No puede utilizar caracteres comodín para obtener todos los datos de las filas, ya que el servicio de consultas debe tratarse como un **almacén de columnas** en lugar de un sistema de tienda tradicional basado en filas.
+++

### ¿Debería usar `NOT IN` en mi consulta SQL?

+++Responder A La `NOT IN` se utiliza a menudo para recuperar filas que no se encuentran en otra tabla o instrucción SQL. Este operador puede ralentizar el rendimiento y devolver resultados inesperados si las columnas que se comparan aceptan `NOT NULL`o tiene un gran número de registros.

En lugar de usar `NOT IN`, puede usar una de las opciones siguientes: `NOT EXISTS` o `LEFT OUTER JOIN`.

Por ejemplo, si tiene creadas las tablas siguientes:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Si está utilizando la variable `NOT EXISTS` operador, puede replicar utilizando la variable `NOT IN` mediante la siguiente consulta:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Alternativamente, si está utilizando la variable `LEFT OUTER JOIN` operador, puede replicar utilizando la variable `NOT IN` mediante la siguiente consulta:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### ¿Puedo crear un conjunto de datos utilizando una consulta CTAS con un nombre de guión bajo doble como los que se muestran en la interfaz de usuario? Por ejemplo: `test_table_001`.

+++Respuesta No, se trata de una limitación intencional en todo el Experience Platform que se aplica a todos los servicios de Adobe, incluido el servicio de consulta. Un nombre con dos guiones bajos es aceptable como esquema y como nombre de conjunto de datos, pero el nombre de tabla para el conjunto de datos solo puede contener un solo guión bajo.
+++

### ¿Cuántas consultas simultáneas se pueden ejecutar a la vez?

+++Respuesta No hay límite de concurrencia de consultas, ya que las consultas por lotes se ejecutan como trabajos back-end. Sin embargo, hay un límite de tiempo de espera de consulta establecido en 24 horas.
+++

### ¿Hay un panel de actividades en el que se puedan ver las actividades de consulta y el estado?

+++Respuesta Existen funciones de supervisión y alerta para comprobar las actividades y los estados de las consultas. Consulte la [Integración del registro de auditoría del servicio de consultas](./data-governance/audit-log-guide.md) y [registros de consultas](./ui/overview.md#log) documentos para obtener más información.
+++

### ¿Hay alguna forma de revertir las actualizaciones? Por ejemplo, si hay un error o es necesario reconfigurar algunos cálculos al escribir datos en Platform, ¿cómo se debe gestionar ese escenario?

+++Respuesta Actualmente, no se admiten devoluciones o actualizaciones de esta manera.
+++

### ¿Cómo se pueden optimizar las consultas en Adobe Experience Platform?

+++Respuesta El sistema no tiene índices, ya que no es una base de datos, pero sí tiene otras optimizaciones asociadas al almacén de datos. Las siguientes opciones están disponibles para ajustar las consultas:

- Filtro basado en el tiempo en datos de temporización.
- Optimización del push para el tipo de datos de estructura.
- Optimización del coste y la memoria para matrices y tipos de datos de asignación.
- Procesamiento incremental mediante instantáneas.
- Formato de datos persistente.
+++

### ¿Pueden restringirse los inicios de sesión a ciertos aspectos del servicio de consulta o es una solución &quot;todo o nada&quot;?

+++Answer Query Service es una solución &quot;todo o nada&quot;. No se puede proporcionar acceso parcial.
+++

### ¿Puedo restringir qué datos puede utilizar el servicio de consulta o simplemente acceder a todo el lago de datos de Adobe Experience Platform?

+++Respuesta Sí, puede restringir la consulta a conjuntos de datos con acceso de solo lectura.
+++

### ¿Qué otras opciones hay para restringir los datos a los que puede acceder el servicio de consulta?

+++Respuesta Existen tres métodos para restringir el acceso. Son los siguientes:

- Utilice instrucciones SELECT only y conceda acceso de solo lectura a los conjuntos de datos. Además, asigne el permiso administrar consulta.
- Utilice las instrucciones SELECT/INSERT/CREATE y conceda acceso de escritura a los conjuntos de datos. Además, asigne el permiso de gestión de consultas.
- Utilice una cuenta de integración con las sugerencias anteriores y asigne el permiso de integración de consultas.

+++

### Una vez que el servicio de consulta devuelve los datos, ¿Platform puede realizar alguna comprobación para asegurarse de que no ha devuelto ningún dato protegido?

- El servicio de consultas admite el control de acceso basado en atributos. Puede restringir el acceso a los datos en el nivel de columna/hoja o en el nivel de estructura. Consulte la documentación para obtener más información sobre el control de acceso basado en atributos.

### ¿Puedo especificar un modo SSL para la conexión a un cliente de terceros? Por ejemplo, ¿puedo usar &#39;verify-full&#39; con Power BI?

+++Respuesta Sí, se admiten los modos SSL. Consulte la [Documentación de modos SSL](./clients/ssl-modes.md) para obtener un desglose de los distintos modos SSL disponibles y el nivel de protección que proporcionan.
+++

### ¿Utilizamos TLS 1.2 para todas las conexiones de clientes de Power BI al servicio de consulta?

+ ++Respuesta Sí. Los datos en tránsito siempre son compatibles con HTTPS. La versión admitida actualmente es TLS1.2.
+++

### ¿Sigue usando https una conexión hecha en el puerto 80?

+++Respuesta Sí, una conexión realizada en el puerto 80 sigue utilizando SSL. También puede utilizar el puerto 5432.
+++

### ¿Puedo controlar el acceso a conjuntos de datos y columnas específicos para una conexión determinada? ¿Cómo se configura esto?

+++Respuesta Sí, el control de acceso basado en atributos se aplica si está configurado. Consulte la [información general sobre el control de acceso basado en atributos](../access-control/abac/overview.md) para obtener más información.
+++

### ¿Admite el servicio de consulta el comando &quot;INSERTAR SOBREESCRITURA EN&quot;?

+++Respuesta No, el servicio de consulta no admite el comando &quot;INSERTAR SOBREESCRITURA EN&quot;.
+++

## Exportación de datos {#exporting-data}

Esta sección proporciona información sobre la exportación de datos y límites.

### ¿Existe alguna forma de extraer datos del servicio de consulta después del procesamiento de la consulta y guardar los resultados en un archivo CSV? {#export-csv}

+ ++Respuesta Sí. Los datos se pueden extraer del servicio de consulta y también existe la opción de almacenar los resultados en formato CSV mediante un comando SQL.

Existen dos maneras de guardar los resultados de una consulta al utilizar un cliente PSQL. Puede usar la variable `COPY TO` o cree una instrucción con el siguiente formato:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Directrices sobre el uso de la `COPY TO` command](./sql/syntax.md#copy) se puede encontrar en la documentación de referencia de sintaxis SQL.
+++

### ¿Puedo extraer el contenido del conjunto de datos final que se ha introducido a través de consultas CTAS (suponiendo que estas son grandes cantidades de datos como Terabytes)?

+++Nº respuesta Actualmente no hay ninguna función disponible para la extracción de datos ingestados.
+++

### ¿Por qué el conector de datos de Analytics no devuelve datos?

+++Respuesta Una causa común de este problema es consultar datos de series temporales sin un filtro de tiempo. Por ejemplo:

```sql
SELECT * FROM prod_table LIMIT 1;
```

Debe escribirse como:

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## Herramientas de terceros {#third-party-tools}

Esta sección incluye información sobre el uso de herramientas de terceros como PSQL y Power BI.

### ¿Puedo conectar el servicio de consulta a una herramienta de terceros?

+++Respuesta Sí, puede conectar varios clientes de escritorio de terceros al servicio de consulta. Consulte la documentación para [detalles completos sobre los clientes disponibles y cómo conectarlos al servicio de Consulta](./clients/overview.md).
+++

### ¿Existe alguna forma de conectar el servicio de consulta una vez para utilizarlo de forma continua con una herramienta de terceros?

+++Respuesta Sí, los clientes de escritorio de terceros pueden conectarse al servicio de consulta mediante una configuración única de credenciales que no caducan. Un usuario autorizado puede generar credenciales que no caduquen y recibirlas en un archivo JSON que se descarga automáticamente a su equipo local. Completa [instrucciones sobre cómo crear y descargar credenciales que no caduquen](./ui/credentials.md#non-expiring-credentials) en la documentación.
+++

### ¿Por qué no funcionan mis credenciales que no caducan?

+++Respuesta El valor de las credenciales que no caducan son los argumentos concatenados del `technicalAccountID` y `credential` tomado del archivo JSON de configuración. El valor de la contraseña adopta la forma: `{{technicalAccountId}:{credential}}`.
Consulte la documentación para obtener más información sobre cómo [conectarse a clientes externos con credenciales](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### ¿Qué tipo de editores SQL de terceros puedo conectar con el Editor de servicios de consulta?

+++Respuesta Cualquier editor SQL de terceros que sea PSQL o [!DNL Postgres] el cliente compatible se puede conectar al Editor del servicio de consultas. Consulte la documentación para [conexión de clientes al servicio de consulta](./clients/overview.md) para obtener una lista de las instrucciones disponibles.
+++

### ¿Puedo conectar la herramienta de Power BI al servicio de consulta?

+++Respuesta Sí, puede conectar la Power BI al servicio de consulta. Consulte la documentación para [instrucciones sobre la conexión de la aplicación de escritorio de Power BI a Query Service](./clients/power-bi.md).
+++

### ¿Por qué los tableros tardan mucho en cargarse cuando están conectados al servicio de consulta?

+++Respuesta Cuando el sistema está conectado al servicio de consulta, está conectado a un motor de procesamiento interactivo o por lotes. Esto puede provocar que los tiempos de carga sean más largos para reflejar los datos procesados.

Si desea mejorar los tiempos de respuesta de los paneles, debe implementar un servidor de Business Intelligence (BI) como capa de almacenamiento en caché entre las herramientas de Query Service y BI. Por lo general, la mayoría de las herramientas de BI tienen una oferta adicional para un servidor.

El propósito de añadir la capa de servidor de caché es almacenar en caché los datos del servicio de consulta y utilizarlos para que los paneles aceleren la respuesta. Esto es posible, ya que los resultados de las consultas que se ejecutan se almacenan en caché en el servidor BI cada día. A continuación, el servidor en caché proporciona estos resultados a cualquier usuario con la misma consulta para reducir la latencia. Consulte la documentación de la utilidad o herramienta de terceros que está utilizando para obtener aclaraciones sobre esta configuración.
+++

### ¿Es posible acceder al servicio de consulta mediante la herramienta de conexión pgAdmin?

+++Respuesta No, la conectividad pgAdmin no es compatible. A [lista de clientes de terceros disponibles e instrucciones sobre cómo conectarlos al servicio de consulta](./clients/overview.md) en la documentación.
+++

## Errores de API PostgreSQL {#postgresql-api-errors}

La siguiente tabla proporciona códigos de error PSQL y sus posibles causas.

| Código de error | Estado de la conexión | Descripción | Posible causa |
|------------|---------------------------|-------------|----------------|
| **08P01** | N/A | Tipo de mensaje no admitido | Tipo de mensaje no admitido |
| **28P01** | Inicio: autenticación | Contraseña no válida | Token de autenticación no válido |
| **28000** | Inicio: autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **42P12** | Inicio: autenticación | No se encontraron tablas | No se encontraron tablas para su uso |
| **42601** | Consulta | Error de sintaxis | Error de sintaxis o comando no válido |
| **42P01** | Consulta | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **42P07** | Consulta | La tabla existe | Ya existe una tabla con el mismo nombre (CREATE TABLE) |
| **53400** | Consulta | El LÍMITE supera el valor máximo | El usuario especificó una cláusula LIMIT superior a 100.000 |
| **53400** | Consulta | Tiempo de espera de la instrucción | La declaración en directo presentada tardó más de 10 minutos |
| **58000** | Consulta | Error del sistema | Fallo interno del sistema |
| **0A000** | Consulta/Comando | No admitido | La función/funcionalidad de la consulta/comando no es compatible |
| **42501** | Consulta de TABLA DE COLOCACIÓN | El servicio de consulta no crea la tabla de pérdidas | El servicio de consultas no creó la tabla que se está soltando mediante el `CREATE TABLE` statement |
| **42501** | Consulta de TABLA DE COLOCACIÓN | Tabla no creada por el usuario autenticado | El usuario que ha iniciado sesión actualmente no ha creado la tabla que se está quitando |
| **42P01** | Consulta de TABLA DE COLOCACIÓN | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **42P12** | Consulta de TABLA DE COLOCACIÓN | No se encontró ninguna tabla para `dbName`: compruebe el `dbName` | No se encontraron tablas en la base de datos actual |

### ¿Por qué recibí un código de error 58000 al usar el método history_meta() en mi tabla?

+++Responder A La `history_meta()` se utiliza para acceder a una instantánea desde un conjunto de datos. Anteriormente, si se ejecutaba una consulta en un conjunto de datos vacío en Azure Data Lake Storage (ADLS), se recibía un código de error 58000 que indicaba que el conjunto de datos no existe. A continuación se muestra un ejemplo del antiguo error del sistema.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Este error se producía porque no había ningún valor devuelto para la consulta. Este comportamiento se ha corregido para que devuelva el siguiente mensaje:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## Errores de API de REST {#rest-api-errors}

La siguiente tabla proporciona códigos de error HTTP y sus posibles causas.

| Código de estado HTTP | Descripción | Posibles causas |
|------------------|-----------------------|----------------------------|
| 400 | Solicitud incorrecta | Consulta no formada o no válida |
| 401 | Error de autenticación | Token de autenticación no válido |
| 500 | Error interno del servidor | Fallo interno del sistema |
