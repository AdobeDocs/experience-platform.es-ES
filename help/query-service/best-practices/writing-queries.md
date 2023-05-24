---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;escribir consultas;escribir consultas;
solution: Experience Platform
title: Directrices generales para la ejecución de consultas en el servicio de consultas
type: Tutorial
description: Este documento describe los detalles importantes que deben conocerse al escribir consultas en Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: adf8da46d09c60b86df16493043efeacbdd24fe2
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 3%

---

# Directrices generales para la ejecución de consultas en [!DNL Query Service]

Este documento detalla detalles importantes que se deben conocer al escribir consultas en Adobe Experience Platform [!DNL Query Service].

Para obtener información detallada sobre la sintaxis SQL utilizada en [!DNL Query Service], lea la [Documentación de sintaxis SQL](../sql/syntax.md).

## Modelos de ejecución de consulta

Adobe Experience Platform [!DNL Query Service] tiene dos modelos de ejecución de consultas: interactivo y no interactivo. La ejecución interactiva se utiliza para el desarrollo de consultas y la generación de informes en las herramientas de inteligencia empresarial, mientras que la no interactiva se utiliza para trabajos de mayor tamaño y consultas operativas como parte de un flujo de trabajo de procesamiento de datos.

### Ejecución de consulta interactiva

Las consultas se pueden ejecutar de forma interactiva enviándolas a través del [!DNL Query Service] IU o [mediante un cliente conectado](../clients/overview.md). Al ejecutar [!DNL Query Service] mediante un cliente conectado, se ejecuta una sesión activa entre el cliente y [!DNL Query Service] hasta que se devuelva la consulta enviada o se agote el tiempo de espera.

La ejecución de consultas interactivas tiene las siguientes limitaciones:

| Parámetro | Limitation |
| --------- | ---------- |
| Query timeout | 10 minutos |
| Número máximo de filas devueltas | 50 000 |
| Máximo de consultas simultáneas | 5 |

>[!NOTE]
>
>Para anular la limitación de filas máximas, incluya `LIMIT 0` en la consulta. Se sigue aplicando el tiempo de espera de consulta de 10 minutos.

De forma predeterminada, los resultados de las consultas interactivas se devuelven al cliente y son **no** persistió. Para mantener los resultados como un conjunto de datos en [!DNL Experience Platform], la consulta debe utilizar el `CREATE TABLE AS SELECT` sintaxis.

### Ejecución de consulta no interactiva

Consultas enviadas a través de [!DNL Query Service] Las API se ejecutan de forma no interactiva. La ejecución no interactiva significa que [!DNL Query Service] recibe la llamada de API y ejecuta la consulta en el orden en que se recibe. Las consultas no interactivas siempre resultan en la generación de un nuevo conjunto de datos en [!DNL Experience Platform] para recibir los resultados o la inserción de nuevas filas en un conjunto de datos existente.

## Acceso a un campo específico dentro de un objeto

Para acceder a un campo dentro de un objeto de la consulta, puede utilizar la notación de puntos (`.`) o notación de corchetes (`[]`). La siguiente instrucción SQL utiliza la notación de puntos para recorrer el `endUserIds` objeto hasta el `mcid` objeto.

>[!NOTE]
>
>El ID del Experience Cloud (ECID) también se conoce como MCID y sigue utilizándose en áreas de nombres.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nombre de la tabla de análisis. |

La siguiente instrucción SQL utiliza la notación de corchetes para recorrer el `endUserIds` objeto hasta el `mcid` objeto.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nombre de la tabla de análisis. |

>[!NOTE]
>
>Dado que cada tipo de notación devuelve los mismos resultados, el que elija utilizar depende de sus preferencias.

Las dos consultas de ejemplo anteriores devuelven un objeto aplanado, en lugar de un valor único:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

El devuelto `endUserIds._experience.mcid` contiene los valores correspondientes para los parámetros siguientes:

- `id`
- `namespace`
- `primary`

Cuando la columna solo se declara hacia abajo en el objeto, devuelve todo el objeto como una cadena. Para ver solo el ID, utilice:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Comillas

Las comillas simples, las comillas dobles y las comillas invertidas tienen usos diferentes en las consultas del servicio de consultas.

### Comillas simples

La comilla simple (`'`) se utiliza para crear cadenas de texto. Por ejemplo, se puede utilizar en la variable `SELECT` para devolver un valor de texto estático en el resultado y en la instrucción `WHERE` para evaluar el contenido de una columna.

La siguiente consulta declara un valor de texto estático (`'datasetA'`) para una columna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

La siguiente consulta utiliza una cadena entre comillas simples (`'homepage'`) en su cláusula WHERE para devolver eventos de una página específica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### Comillas dobles

Las comillas dobles (`"`) se utiliza para declarar un identificador con espacios.

La siguiente consulta utiliza comillas dobles para devolver valores de columnas especificadas cuando una columna contiene un espacio en su identificador:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Comillas dobles **no puede** se utilizará con acceso al campo de notación de puntos.

### Comillas anteriores

La cita final `` ` `` se utiliza para omitir los nombres de columna reservados **solamente** al utilizar sintaxis de notación de puntos. Por ejemplo, desde `order` es una palabra reservada en SQL, debe utilizar comillas invertidas para acceder al campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Las comillas invertidas también se utilizan para acceder a un campo que comienza con un número. Por ejemplo, para acceder al campo `30_day_value`, deberá utilizar la notación de comillas invertidas.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Las comillas invertidas son **no** es necesario si utiliza la notación de corchetes.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Visualización de información de tabla

Después de conectarse al servicio de consultas, puede ver todas las tablas disponibles en Platform mediante el `\d` o `SHOW TABLES` comandos.

### Vista de tabla estándar

El `\d` muestra el estándar [!DNL PostgreSQL] ver para enumerar tablas. A continuación se muestra un ejemplo de la salida de este comando:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Vista de tabla detallada

`SHOW TABLES` es un comando personalizado que proporciona información más detallada sobre las tablas. A continuación se muestra un ejemplo de la salida de este comando:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Información del esquema

Para ver información más detallada sobre los esquemas de la tabla, puede utilizar la variable `\d {TABLE_NAME}` comando, donde `{TABLE_NAME}` es el nombre de la tabla cuya información de esquema desea ver.

En el ejemplo siguiente se muestra la información de esquema de `luma_midvalues` , que se vería utilizando `\d luma_midvalues`:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Además, puede obtener más información sobre una columna concreta añadiendo el nombre de la columna al nombre de la tabla. Esto se escribiría en el formato `\d {TABLE_NAME}_{COLUMN}`.

El siguiente ejemplo muestra información adicional para `web` y se invocarían con el siguiente comando: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Unirse a conjuntos de datos

Puede unir varios conjuntos de datos para incluir datos de otros conjuntos de datos en la consulta.

El ejemplo siguiente combinaría los dos conjuntos de datos siguientes (`your_analytics_table` y `custom_operating_system_lookup`) y crea un `SELECT` para los 50 sistemas operativos principales por número de vistas de página.

**Consulta**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Resultados**

| OperatingSystem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003 y XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10,6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## Anulación de duplicación

El servicio de consulta admite la anulación de duplicación de datos o la eliminación de filas duplicadas de los datos. Para obtener más información sobre la deduplicación, lea la [Guía de anulación de duplicación del servicio de consultas](../essential-concepts/deduplication.md).

## Cálculos de zona horaria en el servicio de consultas

El servicio de consulta estandariza los datos persistentes en Adobe Experience Platform mediante el formato de marca de tiempo UTC. Para obtener más información sobre cómo traducir el requisito de zona horaria a y desde una marca de tiempo UTC, consulte la [Sección de preguntas frecuentes sobre cómo cambiar la zona horaria a y desde una marca de tiempo UTC](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Pasos siguientes

Al leer este documento, se le han introducido algunas consideraciones importantes al escribir consultas utilizando [!DNL Query Service]. Para obtener más información sobre cómo utilizar la sintaxis SQL para escribir sus propias consultas, lea la [Documentación de sintaxis SQL](../sql/syntax.md).

Para obtener más ejemplos de consultas que se pueden utilizar en el servicio de consultas, lea la siguiente documentación de caso de uso:

- [Perspectivas de Analytics](../use-cases/analytics-insights.md)
- [Creación de un informe de tendencias de eventos](../use-cases/trended-report-of-events.md)
- [Ver un informe de resumen de un visitante](../use-cases/roll-up-report-of-a-visitor.md)
- [Enumeración de las vistas de página de un usuario](../use-cases/list-visitor-sessions.md)
- [Enumerar visitantes por número de vistas de página](../use-cases/visitors-by-number-of-page-views.md)
