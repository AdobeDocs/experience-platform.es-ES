---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;guía de solución de problemas;faq;solución de problemas;
solution: Experience Platform
title: Preguntas frecuentes
description: Este documento contiene preguntas frecuentes y respuestas relacionadas con el servicio de consultas. Los temas incluyen exportación de datos, herramientas de terceros y errores de PSQL.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 8f60d53c1adaf29ce2dce7c3af84f8b39998f7d0
workflow-type: tm+mt
source-wordcount: '4384'
ht-degree: 1%

---

# Preguntas frecuentes

Este documento proporciona respuestas a las preguntas más frecuentes sobre el servicio de consultas y proporciona una lista de los códigos de error más frecuentes al utilizar el servicio de consultas. Si tiene alguna pregunta o solución de problemas relacionados con otros servicios de Adobe Experience Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

La siguiente lista de respuestas a las preguntas más frecuentes se divide en las siguientes categorías:

- [General](#general)
- [Exportación de datos](#exporting-data)
- [Herramientas de terceros](#third-party-tools)
- [Errores de API de PostgreSQL](#postgresql-api-errors)
- [Errores de API de REST](#rest-api-errors)

## Preguntas generales del servicio de consultas {#general}

Esta sección incluye información sobre el rendimiento, los límites y los procesos.

### ¿Puedo desactivar la función de autocompletar en el Editor del servicio de consultas?

+++Nº de respuesta El editor no admite actualmente la desactivación de la característica de autocompletar.
+++

### ¿Por qué el Editor de consultas a veces se vuelve lento cuando escribo en una consulta?

+++Responder Una causa potencial es la función de autocompletar. La función procesa ciertos comandos de metadatos que ocasionalmente pueden ralentizar el editor durante la edición de consultas.
+++

### ¿Puedo usar [!DNL Postman] para la API del servicio de consultas?

+++Respuesta Sí, puede visualizar e interactuar con todos los servicios de API de Adobe mediante [!DNL Postman] (una aplicación gratuita de terceros). Vea la [[!DNL Postman] guía de configuración](https://video.tv.adobe.com/v/28832) para obtener instrucciones paso a paso sobre cómo configurar un proyecto en la consola de Adobe Developer y adquirir todas las credenciales necesarias para utilizarlo con [!DNL Postman]. Consulte la documentación oficial de [instrucciones sobre cómo iniciar, ejecutar y compartir [!DNL Postman] colecciones](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### ¿Hay un límite en el número máximo de filas devueltas por una consulta a través de la interfaz de usuario?

+++Responda Sí, el servicio de consultas aplica internamente un límite de 50 000 filas a menos que se especifique un límite explícito externamente. Consulte las directrices sobre [ejecución de consulta interactiva](./best-practices/writing-queries.md#interactive-query-execution) para obtener más información.
+++

### ¿Puedo utilizar las consultas para actualizar filas?

+++Respuesta: En consultas por lotes no se admite la actualización de una fila dentro del conjunto de datos.
+++

### ¿Existe un límite de tamaño de datos para el resultado de una consulta?

+++Nº de respuesta No hay límite en el tamaño de los datos, pero hay un límite de tiempo de espera de consulta de 10 minutos desde una sesión interactiva. Si la consulta se ejecuta como un CTAS por lotes, no se aplica un tiempo de espera de 10 minutos. Consulte las directrices sobre [ejecución de consulta interactiva](./best-practices/writing-queries.md#interactive-query-execution) para obtener más información.
+++

### ¿Cómo puedo evitar el límite en el número de filas de salida de una consulta SELECT?

+++Respuesta Para evitar el límite de filas de salida, aplique &quot;LIMIT 0&quot; en la consulta. Por ejemplo:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### ¿Cómo evito que mis consultas agoten el tiempo de espera en 10 minutos?

+++Respuesta Se recomiendan una o más de las siguientes soluciones en caso de que se agote el tiempo de espera de las consultas.

- [Conversión de la consulta en una consulta CTAS](./sql/syntax.md#create-table-as-select) y programe la ejecución. La programación de una ejecución se puede realizar [a través de la IU](./ui/user-guide.md#scheduled-queries) o el [API](./api/scheduled-queries.md#create).
- Ejecute la consulta en un fragmento de datos más pequeño aplicando parámetros adicionales [condiciones de filtro](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Ejecute el comando EXPLAIN](./sql/syntax.md#explain) para recopilar más detalles.
- Revise las estadísticas de los datos dentro del conjunto de datos.
- Convierta la consulta en un formulario simplificado y vuelva a ejecutarla mediante [declaraciones preparadas](./sql/prepared-statements.md).
+++

### ¿Hay algún problema o impacto en el rendimiento del servicio de consultas si se ejecutan varias consultas simultáneamente?

+++Nº de respuesta El servicio de consultas tiene una capacidad de escalado automático que garantiza que las consultas simultáneas no tengan ningún impacto notable en el rendimiento del servicio.
+++

### ¿Puedo utilizar palabras clave reservadas como nombre de columna?

+++Respuesta Hay ciertas palabras clave reservadas que no se pueden usar como nombre de columna, como `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. Si desea utilizar estas palabras clave, debe omitir estas columnas.
+++

### ¿Cómo encuentro un nombre de columna de un conjunto de datos jerárquico?

+++Respuesta Los siguientes pasos describen cómo mostrar una vista tabular de un conjunto de datos a través de la interfaz de usuario, incluidos todos los campos y columnas anidados en un formulario aplanado.

- Después de iniciar sesión en el Experience Platform, seleccione **[!UICONTROL Conjuntos de datos]** en la navegación izquierda de la interfaz de usuario para desplazarse a [!UICONTROL Conjuntos de datos] panel.
- Los conjuntos de datos [!UICONTROL Examinar] se abre. Puede utilizar la barra de búsqueda para restringir las opciones disponibles. Seleccione un conjunto de datos de la lista mostrada.

![El panel Conjuntos de datos de la IU de Platform con la barra de búsqueda y un conjunto de datos resaltados.](./images/troubleshooting/dataset-selection.png)

- El [!UICONTROL Actividad de conjuntos de datos] aparece la pantalla. Seleccionar **[!UICONTROL Previsualizar conjunto de datos]** para abrir un cuadro de diálogo del esquema XDM y la vista tabular de los datos aplanados del conjunto de datos seleccionado. Puede encontrar más información en la [previsualización de documentación de un conjunto de datos](../catalog/datasets/user-guide.md#preview-a-dataset)

![La pestaña Actividad de conjunto de datos del panel Conjuntos de datos con el conjunto de datos de vista previa resaltado.](./images/troubleshooting/dataset-preview.png)

- Seleccione cualquier campo del esquema para mostrar su contenido en una columna aplanada. El nombre de la columna se muestra encima de su contenido en el lado derecho de la página. Debe copiar este nombre para utilizarlo para consultar este conjunto de datos.

![El esquema XDM y la vista tabular de los datos aplanados. El nombre de columna de un conjunto de datos anidado se resalta en la interfaz de usuario.](./images/troubleshooting/column-name.png)

Consulte la documentación para obtener instrucciones completas sobre [cómo trabajar con estructuras de datos anidadas](./key-concepts/nested-data-structures.md) mediante el Editor de consultas o un cliente de terceros.
+++

### ¿Cómo acelero una consulta en un conjunto de datos que contiene matrices?

+++Respuesta Para mejorar el rendimiento de las consultas en conjuntos de datos que contienen matrices, debe [explosionar la matriz](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [Consulta CTAS](./sql/syntax.md#create-table-as-select) en tiempo de ejecución y, a continuación, explórela para buscar oportunidades que mejoren su tiempo de procesamiento.
+++

### ¿Por qué mi consulta CTAS sigue procesándose después de muchas horas para un pequeño número de filas?

+++Respuesta Si la consulta ha tardado mucho tiempo en un conjunto de datos muy pequeño, póngase en contacto con el servicio de atención al cliente.

Puede haber varias razones para que una consulta se bloquee durante el procesamiento. Para determinar la causa exacta se requiere un análisis en profundidad caso por caso. [Atención al cliente de Adobe](#customer-support) por ser este proceso.
+++

### ¿Cómo puedo contactar con Atención al cliente de Adobe? {#customer-support}

+++Respuesta
[Una lista completa de los números de teléfono de asistencia al cliente de Adobe](https://helpx.adobe.com/ca/contact/phone.html) está disponible en la página de ayuda de Adobe. También puede encontrar ayuda en línea si completa los siguientes pasos:

- Vaya a [https://www.adobe.com/](https://www.adobe.com/) en el explorador web.
- En el lado derecho de la barra de navegación superior, seleccione **[!UICONTROL Iniciar sesión]**.

![El sitio web de Adobe con la opción Iniciar sesión resaltada.](./images/troubleshooting/adobe-sign-in.png)

- Utilice su Adobe ID y contraseña registrados con su licencia de Adobe.
- Seleccionar **[!UICONTROL Ayuda y asistencia]** en la barra de navegación superior.

![Menú desplegable de la barra de navegación superior con ayuda y asistencia, asistencia técnica para empresas y contacto resaltado.](./images/troubleshooting/help-and-support.png)

Aparece un banner desplegable que contiene una [!UICONTROL Ayuda y asistencia] sección. Seleccionar **[!UICONTROL Contáctenos.]** para abrir el Asistente virtual del Servicio de atención al cliente de Adobe, o seleccione **[!UICONTROL Soporte Enterprise]** para obtener ayuda específica para grandes organizaciones.
+++

### ¿Cómo implemento una serie secuencial de trabajos, sin ejecutar trabajos subsiguientes si el trabajo anterior no se completa correctamente?

+++Respuesta La función de bloque anónimo permite encadenar una o más sentencias SQL que se ejecutan en secuencia. También permiten la opción de la gestión de excepciones.

Consulte la [documentación de bloque anónimo](./key-concepts/anonymous-block.md) para obtener más información.
+++

### ¿Cómo implemento la atribución personalizada en el servicio de consultas?

+++Respuesta: Existen dos formas de implementar la atribución personalizada:

1. Usar una combinación de los [Funciones definidas por el Adobe](./sql/adobe-defined-functions.md) para identificar si se cumplen las necesidades del caso de uso.
1. Si la sugerencia anterior no cumple con su caso de uso, debe utilizar una combinación de [funciones de ventana](./sql/adobe-defined-functions.md#window-functions). Las funciones de ventana buscan todos los eventos en una secuencia. También le permiten revisar los datos históricos y se pueden utilizar en cualquier combinación.
+++

### ¿Puedo crear una plantilla de mis consultas para poder reutilizarlas fácilmente?

+++Responda Sí, puede crear plantillas de consultas mediante el uso de instrucciones preparadas. Las instrucciones preparadas pueden optimizar el rendimiento y evitar volver a analizar una consulta de forma repetida. Consulte la [documentación de declaraciones preparadas](./sql/prepared-statements.md) para obtener más información.
+++

### ¿Cómo se recuperan los registros de errores de una consulta? {#error-logs}

+++Respuesta Para recuperar los registros de errores de una consulta específica, primero debe utilizar la API del servicio de consultas para recuperar los detalles del registro de consultas. La respuesta HTTP contiene los ID de consulta necesarios para investigar un error de consulta.

Utilice el comando GET para recuperar varias consultas. Encontrará información sobre cómo realizar una llamada a la API en la [ejemplo de documentación de llamadas de API](./api/queries.md#sample-api-calls).

En la respuesta, identifique la GET que desee investigar y realice otra solicitud utilizando `id` valor. Puede encontrar las instrucciones completas en la [Recuperación de una consulta por documentación de ID](./api/queries.md#retrieve-a-query-by-id).

Una respuesta correcta devuelve el estado HTTP 200 y contiene el `errors` matriz. La respuesta se ha abreviado para ser más breve.

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

El [Documentación de referencia de API del servicio de consultas](https://www.adobe.io/experience-platform-apis/references/query-service/) proporciona más información sobre todos los extremos disponibles.
+++

### ¿Qué significa &quot;Error al validar el esquema&quot;?

+++Respuesta El mensaje &quot;Error al validar el esquema&quot; significa que el sistema no puede localizar un campo dentro del esquema. Debe leer el documento de prácticas recomendadas para [organización de recursos de datos en el servicio de consultas](./best-practices/organize-data-assets.md) seguido del [Crear tabla como, seleccione la documentación](./sql/syntax.md#create-table-as-select).

En el ejemplo siguiente se muestra el uso de una sintaxis CTAS y un tipo de datos struct:

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

### ¿Cómo proceso rápidamente los nuevos datos que entran en el sistema todos los días?

+++Responda Al [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) La cláusula se puede utilizar para leer de forma incremental los datos de una tabla en función de un ID de instantánea. Esto es ideal para su uso con el [carga incremental](./key-concepts/incremental-load.md) patrón de diseño que solo procesa la información en el conjunto de datos que se ha creado o modificado desde la última ejecución de carga. Como resultado, aumenta la eficacia del procesamiento y se puede utilizar tanto con el procesamiento de datos por lotes como con el streaming.
+++

### ¿Por qué hay una diferencia entre los números que se muestran en la interfaz de usuario del perfil y los números calculados a partir del conjunto de datos de exportación de perfiles?

+++Respuesta Los números mostrados en el panel de perfiles son precisos a partir de la última instantánea. Los números generados en la tabla de exportación de perfiles dependen totalmente de la consulta de exportación. Como resultado, una causa común de esta discrepancia es consultar el número de perfiles que cumplen los requisitos de una audiencia determinada.

>[!NOTE]
>
>La consulta incluye datos históricos, mientras que la interfaz de usuario solo muestra los datos de perfil actuales.

+++

### ¿Por qué mi consulta devolvió un subconjunto vacío y qué debo hacer?

+++Respuesta La causa más probable es que la consulta tenga un ámbito demasiado limitado. Debe eliminar sistemáticamente una sección del `WHERE` hasta que empiece a ver algunos datos.

También puede confirmar que el conjunto de datos contiene datos mediante una pequeña consulta como:

```sql
SELECT count(1) FROM myTableName
```

+++

### ¿Puedo tomar muestras de mis datos?

+++Respuesta Actualmente, esta función está en curso. Los detalles estarán disponibles en [notas de la versión](../release-notes/latest/latest.md) y a través de los cuadros de diálogo de IU de Platform una vez que la función esté lista para su lanzamiento.
+++

### ¿Qué funciones de ayuda admite el servicio de consultas?

+++El servicio de consulta de respuesta proporciona varias funciones de ayuda SQL integradas para ampliar la funcionalidad SQL. Consulte el documento para obtener una lista completa de los [Funciones SQL admitidas por el servicio de consultas](./sql/spark-sql-functions.md).
+++

### Son todos nativos [!DNL Spark SQL] funciones admitidas o son usuarios restringidos solo al envoltorio [!DNL Spark SQL] funciones proporcionadas por el Adobe?

+++Responder Hasta ahora, no todo es de código abierto [!DNL Spark SQL] Las funciones de se han probado en los datos del lago de datos. Una vez probadas y confirmadas, se añadirán a la lista de admitidas. Consulte la [lista de admitidos [!DNL Spark SQL] Funciones](./sql/spark-sql-functions.md) para buscar una función específica.
+++

### ¿Pueden los usuarios definir sus propias funciones definidas por el usuario (UDF) que se pueden utilizar en otras consultas?

+++Respuesta Debido a consideraciones de seguridad de los datos, no se permite la definición personalizada de FDU.
+++

### ¿Qué debo hacer si falla mi consulta programada?

+++Responda primero, compruebe los registros para averiguar los detalles del error. La sección de preguntas frecuentes sobre [búsqueda de errores en registros](#error-logs) proporciona más información sobre cómo hacerlo.

También debe consultar la documentación para obtener instrucciones sobre cómo realizar [consultas programadas en la interfaz de usuario](./ui/user-guide.md#scheduled-queries) y mediante [la API](./api/scheduled-queries.md).

Tenga en cuenta lo siguiente al utilizar [!DNL Query Editor] solo puede agregar una programación a una consulta que ya se haya creado, guardado y ejecutado. Esto no se aplica al [!DNL Query Service] API.
+++

### ¿Qué significa el error &quot;Límite de sesión alcanzado&quot;?

+++La respuesta &quot;Se ha alcanzado el límite de sesiones&quot; significa que se ha alcanzado el número máximo de sesiones del Servicio de consultas permitidas para su organización. Conéctese con el administrador de Adobe Experience Platform de su organización.
+++

### ¿Cómo gestiona el registro de consultas las consultas relacionadas con un conjunto de datos eliminado?

+++El servicio de consulta de respuesta nunca elimina el historial de consultas. Esto significa que cualquier consulta que haga referencia a un conjunto de datos eliminado devolverá &quot;Ningún conjunto de datos válido&quot; como resultado.
+++

### ¿Cómo puedo obtener solo los metadatos de una consulta?

+++Respuesta Puede ejecutar una consulta que devuelva cero filas para obtener únicamente los metadatos como respuesta. Esta consulta de ejemplo devuelve sólo los metadatos de la tabla especificada.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### ¿Cómo puedo iterar rápidamente en una consulta CTAS (Crear tabla como selección) sin materializarla?

+++Respuesta Puede crear tablas temporales para repetir y experimentar rápidamente una consulta antes de materializarla para su uso. También puede utilizar tablas temporales para validar si una consulta funciona.

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

### ¿Cómo cambio la zona horaria a y desde una marca de tiempo UTC?

+++Responder Adobe Experience Platform conserva los datos en formato UTC (hora universal coordinada). Un ejemplo del formato UTC es `2021-12-22T19:52:05Z`

El servicio de consultas admite funciones SQL integradas para convertir una marca de tiempo determinada al formato UTC y desde este. Tanto la `to_utc_timestamp()` y el `from_utc_timestamp()` Los métodos de toman dos parámetros: marca de tiempo y zona horaria.

| Parámetro | Descripción |
|-----------|---------------|
| Marca de tiempo | La marca de tiempo puede escribirse en formato UTC o simple `{year-month-day}` formato. Si no se proporciona ninguna hora, el valor predeterminado es medianoche en la mañana del día determinado. |
| Zona horaria | La zona horaria está escrita en un `{continent/city})` formato. Debe ser uno de los códigos de zona horaria reconocidos, tal como se encuentran en la [base de datos TZ de dominio público](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Convertir a la marca de tiempo UTC

El `to_utc_timestamp()` El método interpreta los parámetros dados y los convierte **a la marca de tiempo de su zona horaria local** en formato UTC. Por ejemplo, la zona horaria de Seúl, Corea del Sur, es UTC/GMT +9 horas. Al proporcionar una marca de tiempo de solo fecha, el método utiliza un valor predeterminado de medianoche en la mañana. La marca de tiempo y la zona horaria se convierten al formato UTC desde el momento de esa región a una marca de tiempo UTC de su región local.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

La consulta devuelve una marca de tiempo en la hora local del usuario. En este caso, a las 3 p. m. del día anterior, ya que Seúl está nueve horas por delante.

```
2021-08-30 15:00:00
```

Otro ejemplo: si la marca de tiempo dada era `2021-07-14 12:40:00.0` para el `Asia/Seoul` timezone, la marca de tiempo UTC devuelta sería `2021-07-14 03:40:00.0`

El resultado de la consola proporcionado en la interfaz de usuario del servicio de consultas tiene un formato más legible en lenguaje natural:

```
8/30/2021, 3:00 PM
```

#### Convertir desde la marca de tiempo UTC

El `from_utc_timestamp()` El método interpreta los parámetros dados **de la marca de tiempo de su zona horaria local** y proporciona la marca de tiempo equivalente de la región deseada en formato UTC. En el ejemplo siguiente, la hora es las 2:40 p.m. en la zona horaria local del usuario. La zona horaria de Seúl que se pasa como variable está nueve horas por delante de la zona horaria local.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

La consulta devuelve una marca de tiempo en formato UTC para la zona horaria pasada como parámetro. El resultado es nueve horas antes de la zona horaria que ejecutó la consulta.

```
8/31/2021, 11:40 PM
```

### ¿Cómo debo filtrar los datos de las series temporales?

+++Respuesta: Cuando consulte con datos de series temporales, debe utilizar el filtro de marcas de hora siempre que sea posible para realizar un análisis más preciso.

>[!NOTE]
>
> La cadena de fecha **debe** estar en el formato `yyyy-mm-ddTHH24:MM:SS`.

A continuación se puede ver un ejemplo de uso del filtro de marca de tiempo:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### ¿Cómo utilizo correctamente el `CAST` para convertir mis marcas de tiempo en consultas SQL?

+++Responda al usar el `CAST` para convertir una marca de tiempo, debe incluir la fecha y **y** hora.

Por ejemplo, si falta el componente de tiempo, como se muestra a continuación, se producirá un error:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

El uso correcto del `CAST` operador se muestra a continuación:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### ¿Debería utilizar caracteres comodín, como *, para obtener todas las filas de mis conjuntos de datos?

+++Respuesta No puede utilizar caracteres comodín para obtener todos los datos de las filas, ya que el servicio de consultas debe tratarse como una **almacén en columnas** en lugar de un sistema de almacén tradicional basado en filas.
+++

### ¿Debería usar `NOT IN` en mi consulta SQL?

+++Responda Al `NOT IN` El operador se utiliza a menudo para recuperar filas que no se encuentran en otra tabla o instrucción SQL. Este operador puede ralentizar el rendimiento y devolver resultados inesperados si las columnas que se comparan aceptan `NOT NULL`o tiene un gran número de registros.

En lugar de usar `NOT IN`, puede utilizar cualquiera de las siguientes opciones `NOT EXISTS` o `LEFT OUTER JOIN`.

Por ejemplo, si ha creado las siguientes tablas:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Si utiliza el complemento `NOT EXISTS` , puede replicar utilizando el operador `NOT IN` mediante la siguiente consulta:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Alternativamente, si utiliza el `LEFT OUTER JOIN` , puede replicar utilizando el operador `NOT IN` mediante la siguiente consulta:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### ¿Puedo crear un conjunto de datos utilizando una consulta CTAS con un nombre de guion bajo doble como los que se muestran en la interfaz de usuario? Por ejemplo: `test_table_001`.

+++Respuesta no, se trata de una limitación intencionada entre Experience Platform que se aplica a todos los servicios de Adobe, incluido el servicio de consultas. Se acepta un nombre con dos guiones bajos como esquema y nombre de conjunto de datos, pero el nombre de tabla del conjunto de datos solo puede contener un guion bajo.
+++

### ¿Cuántas consultas simultáneas se pueden ejecutar a la vez?

+++Respuesta No hay límite de concurrencia de consultas, ya que las consultas por lotes se ejecutan como trabajos back-end. Sin embargo, hay un límite de tiempo de espera de consulta establecido en 24 horas.
+++

### ¿Hay un panel de actividad en el que pueda ver las actividades de consulta y el estado?

+++Respuesta Existen capacidades de monitorización y alertas para comprobar las actividades de consulta y los estados. Consulte la [Integración del registro de auditoría del servicio de consultas](./data-governance/audit-log-guide.md) y el [registros de consultas](./ui/overview.md#log) documentos para obtener más información.
+++

### ¿Hay alguna forma de revertir las actualizaciones? Por ejemplo, si hay un error o es necesario volver a configurar algunos cálculos al escribir datos en Platform, ¿cómo se debe gestionar ese escenario?

+++Responder Actualmente, no se admiten reversiones ni actualizaciones de esta manera.
+++

### ¿Cómo se pueden optimizar las consultas en Adobe Experience Platform?

+++Respuesta El sistema no tiene índices, ya que no es una base de datos, pero tiene otras optimizaciones asociadas al almacén de datos. Las siguientes opciones están disponibles para ajustar las consultas:

- Un filtro basado en el tiempo en datos de series temporales.
- Inserción optimizada para el tipo de datos struct.
- Inserción optimizada de coste y memoria para cabinas y tipos de datos de asignación.
- Procesamiento incremental mediante instantáneas.
- Un formato de datos persistente.
+++

### ¿Pueden los inicios de sesión restringirse a determinados aspectos del servicio de consultas o es una solución de &quot;todo o nada&quot;?

+++El servicio de consulta de respuestas es una solución de &quot;todo o nada&quot;. No se puede proporcionar acceso parcial.
+++

### ¿Puedo restringir qué datos puede utilizar el servicio de consulta de datos o simplemente accede a todo el lago de datos de Adobe Experience Platform?

+++Respuesta Sí, puede restringir la consulta a conjuntos de datos con acceso de solo lectura.
+++

### ¿Qué otras opciones hay para restringir los datos a los que puede acceder el servicio de consulta?

+++Respuesta Existen tres métodos para restringir el acceso. Son las siguientes:

- Utilice instrucciones SELECT únicamente y proporcione acceso de solo lectura a los conjuntos de datos. Además, asigne el permiso de administración de consultas.
- Utilice las instrucciones SELECT/INSERT/CREATE y proporcione acceso de escritura a los conjuntos de datos. Además, asigne el permiso de administración de consultas.
- Utilice una cuenta de integración con las sugerencias anteriores y asigne el permiso de integración de consultas.

+++

### Una vez que el servicio de consulta devuelve los datos, ¿Platform puede ejecutar alguna comprobación para asegurarse de que no ha devuelto datos protegidos?

- El servicio de consultas admite el control de acceso basado en atributos. Puede restringir el acceso a los datos en el nivel de columna/hoja y/o en el nivel de estructura. Consulte la documentación para obtener más información sobre el control de acceso basado en atributos.

### ¿Puedo especificar un modo SSL para la conexión a un cliente de terceros? Por ejemplo, ¿puedo usar &#39;verify-full&#39; con Power BI?

+++Responda que sí, se admiten los modos SSL. Consulte la [Documentación de modos SSL](./clients/ssl-modes.md) para obtener un desglose de los diferentes modos SSL disponibles y el nivel de protección que proporcionan.
+++

### ¿Utilizamos TLS 1.2 para todas las conexiones de clientes de Power BI al servicio de consultas?

+++Conteste Sí. Los datos en tránsito siempre son compatibles con HTTPS. La versión admitida actualmente es TLS1.2.
+++

### ¿Sigue usando https una conexión realizada en el puerto 80?

+++Respuesta Sí, una conexión realizada en el puerto 80 sigue utilizando SSL. También puede utilizar el puerto 5432.
+++

### ¿Puedo controlar el acceso a conjuntos de datos y columnas específicos para una conexión en particular? ¿Cómo se configura?

+++Respuesta Sí, el control de acceso basado en atributos se aplica si se configura. Consulte la [información general sobre el control de acceso basado en atributos](../access-control/abac/overview.md) para obtener más información.
+++

### ¿Query Service admite el comando &quot;INSERT OVERWRITE INTO&quot;?

+++Respuesta no, el servicio de consultas no admite el comando &quot;INSERTAR SOBRESCRITURA EN&quot;.
+++

### ¿Con qué frecuencia se actualizan los datos de uso en el tablero de uso de licencias para las horas calculadas de Data Distiller?

+++Respuesta El panel de uso de licencias del horario laboral del equipo de Data Distiller se actualiza cuatro veces al día, cada seis horas.
+++

### ¿Puedo utilizar el comando CREATE VIEW sin acceso a Data Distiller?

+++Responda Sí, puede usar `CREATE VIEW` sin acceso a Data Distiller. Este comando proporciona una vista lógica de los datos, pero no los vuelve a escribir en el lago de datos.
+++

## Exportación de datos {#exporting-data}

Esta sección proporciona información sobre la exportación de datos y límites.

### ¿Existe alguna forma de extraer datos del servicio de consulta después del procesamiento de la consulta y guardar los resultados en un archivo CSV? {#export-csv}

+++Conteste Sí. Los datos se pueden extraer del servicio de consulta y también existe la opción de almacenar los resultados en formato CSV a través de un comando SQL.

Existen dos maneras de guardar los resultados de una consulta al utilizar un cliente SQL. Puede usar el complemento `COPY TO` o cree una instrucción con el siguiente formato:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Directrices sobre el uso del `COPY TO` mando](./sql/syntax.md#copy) se puede encontrar en la documentación de referencia de sintaxis SQL.
+++

### ¿Puedo extraer el contenido del conjunto de datos final que se ha introducido a través de consultas CTAS (suponiendo que sean cantidades mayores de datos, como terabytes)?

+++Nº de respuesta Actualmente no hay ninguna función disponible para la extracción de datos ingeridos.
+++

### ¿Por qué el conector de datos de Analytics no devuelve datos?

+++Respuesta Una causa común de este problema es la consulta de datos de series temporales sin un filtro de tiempo. Por ejemplo:

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

### ¿Puedo conectar el servicio de consultas a una herramienta de terceros?

+++Responda Sí, puede conectar varios clientes de escritorio de terceros al servicio de consultas. Consulte la documentación de [detalles completos sobre los clientes disponibles y cómo conectarlos al servicio de consultas](./clients/overview.md).
+++

### ¿Existe alguna forma de conectar el servicio de consulta una vez para utilizarlo de forma continua con una herramienta de terceros?

+++Responda Sí, los clientes de escritorio de terceros se pueden conectar al servicio de consultas mediante una configuración única de credenciales que no caducan. Las credenciales que no caducan las puede generar un usuario autorizado y recibirlas en un archivo JSON que se descarga automáticamente en su equipo local. Completo [instrucciones sobre cómo crear y descargar credenciales que no caducan](./ui/credentials.md#non-expiring-credentials) se puede encontrar en la documentación.
+++

### ¿Por qué las credenciales que no caducan no funcionan?

+++Respuesta El valor de las credenciales que no caducan son los argumentos concatenados del `technicalAccountID` y el `credential` tomado del archivo JSON de configuración. El valor de la contraseña adopta la forma siguiente: `{{technicalAccountId}:{credential}}`.
Consulte la documentación para obtener más información sobre cómo [conectarse a clientes externos con credenciales](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### ¿Qué tipo de editores SQL de terceros puedo conectar al Editor de servicios de consulta?

+++Responda Cualquier editor SQL de terceros que sea PSQL o [!DNL Postgres] Los clientes compatibles se pueden conectar al Editor del servicio de consultas. Consulte la documentación de [conectar clientes al servicio de consultas](./clients/overview.md) para obtener una lista de las instrucciones disponibles.
+++

### ¿Puedo conectar la herramienta de Power BI al servicio de consultas?

+++Responda Sí, puede conectar Power BI al servicio de consultas. Consulte la documentación de [instrucciones para conectar la aplicación de escritorio de Power BI al servicio de consultas](./clients/power-bi.md).
+++

### ¿Por qué tardan mucho tiempo en cargarse los paneles al conectarse al servicio de consultas?

+++Respuesta Cuando el sistema está conectado al servicio de consultas, está conectado a un motor de procesamiento interactivo o por lotes. Esto puede conllevar un mayor tiempo de carga para reflejar los datos procesados.

Si desea mejorar los tiempos de respuesta de sus paneles, debe implementar un servidor de Business Intelligence (BI) como capa de almacenamiento en caché entre el servicio de consultas y las herramientas de BI. Por lo general, la mayoría de las herramientas de BI tienen una oferta adicional para un servidor.

El propósito de añadir la capa del servidor de caché es almacenar en caché los datos del servicio de consulta y utilizar el mismo para los paneles a fin de acelerar la respuesta. Esto es posible ya que los resultados de las consultas que se ejecutan se almacenarían en caché en el servidor de BI todos los días. A continuación, el servidor de almacenamiento en caché proporciona estos resultados a cualquier usuario con la misma consulta para reducir la latencia. Consulte la documentación de la utilidad o herramienta de terceros que está utilizando para obtener más información sobre esta configuración.
+++

### ¿Es posible acceder al servicio de consultas mediante la herramienta de conexión pgAdmin?

+++Respuesta No, no se admite la conectividad con pgAdmin. A [lista de clientes de terceros disponibles e instrucciones sobre cómo conectarlos al servicio de consultas](./clients/overview.md) se puede encontrar en la documentación.
+++

## Errores de API de PostgreSQL {#postgresql-api-errors}

La siguiente tabla proporciona códigos de error PSQL y sus posibles causas.

| Código de error | Estado de conexión | Descripción | Posible causa |
|------------|---------------------------|-------------|----------------|
| **08P01** | N/A | Tipo de mensaje no compatible | Tipo de mensaje no compatible |
| **28P01** | Inicio: autenticación | Contraseña no válida | Token de autenticación no válido |
| **28000** | Inicio: autenticación | Tipo de autorización no válido | Tipo de autorización no válido. Debe ser `AuthenticationCleartextPassword`. |
| **42P12** | Inicio: autenticación | No se han encontrado tablas | No se han encontrado tablas para su uso |
| **42601** | Consulta | Error de sintaxis | Error de comando o sintaxis no válido |
| **42P01** | Consulta | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **42P07** | Consulta | La tabla existe | Ya existe una tabla con el mismo nombre (CREATE TABLE) |
| **53400** | Consulta | El LÍMITE supera el valor máximo | El usuario especificó una cláusula LIMIT superior a 100 000 |
| **53400** | Consulta | Tiempo de espera de instrucción | La declaración en directo enviada ha tardado más de 10 minutos como máximo |
| **58000** | Consulta | Error del sistema | Fallo interno del sistema |
| **0A000** | Consulta/Comando | No admitido | No se admite la función/funcionalidad de la consulta/comando |
| **42501** | DROP TABLE Query | El servicio de consultas no crea la tabla de colocación | El servicio de consultas no creó la tabla que se está quitando mediante el `CREATE TABLE` declaración |
| **42501** | DROP TABLE Query | Tabla no creada por el usuario autenticado | El usuario que ha iniciado sesión actualmente no ha creado la tabla que se está quitando |
| **42P01** | DROP TABLE Query | Tabla no encontrada | No se encontró la tabla especificada en la consulta |
| **42P12** | DROP TABLE Query | No se ha encontrado ninguna tabla para `dbName`: compruebe la `dbName` | No se encontraron tablas en la base de datos actual |

### ¿Por qué recibí un código de error 58000 al usar el método history_meta() en mi tabla?

+++Responda Al `history_meta()` se utiliza para acceder a una instantánea de un conjunto de datos. Anteriormente, si ejecutaba una consulta en un conjunto de datos vacío en Azure Data Lake Storage (ADLS), recibía un código de error 58000 que indicaba que el conjunto de datos no existe. A continuación se muestra un ejemplo del error del sistema antiguo.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Este error se produjo porque no había ningún valor devuelto para la consulta. Este comportamiento se ha corregido para devolver el siguiente mensaje:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## Errores de API de REST {#rest-api-errors}

La siguiente tabla proporciona códigos de error HTTP y sus posibles causas.

| Código de estado HTTP | Descripción | Posibles causas |
|------------------|-----------------------|----------------------------|
| 400 | Solicitud incorrecta | Consulta incorrecta o no válida |
| 401 | Error de autenticación | Token de autenticación no válido |
| 500 | Error interno del servidor | Fallo interno del sistema |
