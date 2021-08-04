---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;escritura de consultas;escritura de consultas;
solution: Experience Platform
title: Guía general para la ejecución de consultas en el servicio de consultas
topic-legacy: queries
type: Tutorial
description: Este documento detalla detalles importantes que deben conocerse al escribir consultas en el servicio de consulta de Adobe Experience Platform.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: c720b9e6f81ed4ad8bd3360a9b1a19bfcd21a0ef
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 3%

---

# Directrices generales para la ejecución de consultas en [!DNL Query Service]

Este documento detalla detalles importantes que deben conocerse al escribir consultas en Adobe Experience Platform [!DNL Query Service].

Para obtener información detallada sobre la sintaxis SQL utilizada en [!DNL Query Service], lea la [Documentación de sintaxis SQL](../sql/syntax.md).

## Modelos de ejecución de consultas

Adobe Experience Platform [!DNL Query Service] tiene dos modelos de ejecución de consultas: interactivo y no interactivo. La ejecución interactiva se utiliza para el desarrollo de consultas y la generación de informes en las herramientas de inteligencia empresarial, mientras que la no interactiva se utiliza para trabajos más grandes y consultas operativas como parte de un flujo de trabajo de procesamiento de datos.

### Ejecución de consultas interactivas

Las consultas se pueden ejecutar de forma interactiva enviándolas a través de la [!DNL Query Service] interfaz de usuario o [a través de un cliente conectado](../clients/overview.md). Al ejecutar [!DNL Query Service] a través de un cliente conectado, se ejecuta una sesión activa entre el cliente y [!DNL Query Service] hasta que se devuelve o se agota el tiempo de espera de la consulta enviada.

La ejecución de consultas interactivas tiene las siguientes limitaciones:

| Parámetro | Limitación |
| --------- | ---------- |
| Tiempo de espera de consulta | 10 minutos |
| Máximo de filas devueltas | 50.000 |
| Máximo de consultas simultáneas | 5 |

>[!NOTE]
>
>Para anular la limitación máxima de filas, incluya `LIMIT 0` en la consulta. Se sigue aplicando el tiempo de espera de consulta de 10 minutos.

De forma predeterminada, los resultados de las consultas interactivas se devuelven al cliente y **no** persisten. Para mantener los resultados como un conjunto de datos en [!DNL Experience Platform], la consulta debe utilizar la sintaxis `CREATE TABLE AS SELECT`.

### Ejecución de consultas no interactivas

Las consultas enviadas a través de la API [!DNL Query Service] se ejecutan de forma no interactiva. La ejecución no interactiva significa que [!DNL Query Service] recibe la llamada de API y ejecuta la consulta en el orden en que se recibe. Las consultas no interactivas siempre resultan en la generación de un nuevo conjunto de datos en [!DNL Experience Platform] para recibir los resultados o en la inserción de nuevas filas en un conjunto de datos existente.

## Acceso a un campo específico dentro de un objeto

Para acceder a un campo dentro de un objeto de la consulta, puede utilizar la notación de puntos (`.`) o la notación de corchetes (`[]`). La siguiente instrucción SQL utiliza la notación de puntos para recorrer el objeto `endUserIds` hasta el objeto `mcid`.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | El nombre de la tabla de análisis. |

La siguiente sentencia SQL utiliza la notación de corchetes para recorrer el objeto `endUserIds` hacia abajo hasta el objeto `mcid`.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | El nombre de la tabla de análisis. |

>[!NOTE]
>
>Dado que cada tipo de anotación devuelve los mismos resultados, el que elija utilizar dependerá de sus preferencias.

Las dos consultas de ejemplo anteriores devuelven un objeto acoplado, en lugar de un solo valor:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

El objeto `endUserIds._experience.mcid` devuelto contiene los valores correspondientes para los siguientes parámetros:

- `id`
- `namespace`
- `primary`

Cuando la columna solo se declara en el objeto, devuelve el objeto entero como una cadena. Para ver solo el ID, utilice:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Comillas

Las comillas simples, las comillas dobles y las comillas invertidas tienen usos diferentes dentro de las consultas del servicio de consulta.

### Comillas simples

La comilla simple (`'`) se utiliza para crear cadenas de texto. Por ejemplo, se puede utilizar en la instrucción `SELECT` para devolver un valor de texto estático en el resultado y en la cláusula `WHERE` para evaluar el contenido de una columna.

La siguiente consulta declara un valor de texto estático (`'datasetA'`) para una columna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

La siguiente consulta utiliza una cadena entre comillas simples (`'homepage'`) en su cláusula WHERE para devolver eventos para una página específica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Comillas dobles

La comilla doble (`"`) se utiliza para declarar un identificador con espacios.

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
>Las comillas dobles **no pueden** utilizarse con acceso al campo de notación de puntos.

### comillas invertidas

La comilla trasera `` ` `` se utiliza para omitir los nombres de columna reservados **only** cuando se utiliza la sintaxis de notación de puntos. Por ejemplo, como `order` es una palabra reservada en SQL, debe utilizar comillas invertidas para acceder al campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Las comillas invertidas también se utilizan para acceder a un campo que comienza con un número. Por ejemplo, para acceder al campo `30_day_value`, debe utilizar la notación de comillas invertidas.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Las comillas de fondo **no** son necesarias si utiliza la notación de corchetes.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Visualización de la información de la tabla

Después de conectarse al servicio de consulta, puede ver todas las tablas disponibles en Platform mediante los comandos `\d` o `SHOW TABLES`.

### Vista de tabla estándar

El comando `\d` muestra la vista PostgreSQL estándar para listar tablas. A continuación se puede ver un ejemplo de la salida de este comando:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Vista detallada de la tabla

`SHOW TABLES` es un comando personalizado que proporciona información más detallada sobre las tablas. A continuación se puede ver un ejemplo de la salida de este comando:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Información del esquema

Para ver información más detallada sobre los esquemas dentro de la tabla, puede utilizar el comando `\d {TABLE_NAME}`, donde `{TABLE_NAME}` es el nombre de la tabla cuya información de esquema desea ver.

El siguiente ejemplo muestra la información de esquema de la tabla `luma_midvalues`, que se vería mediante `\d luma_midvalues`:

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

Además, puede obtener más información sobre una columna en particular anexando el nombre de la columna al nombre de la tabla. Esto se escribiría con el formato `\d {TABLE_NAME}_{COLUMN}`.

En el siguiente ejemplo se muestra información adicional para la columna `web` y se invoca mediante el siguiente comando: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Combinación de conjuntos de datos

Puede unir varios conjuntos de datos para incluir datos de otros conjuntos de datos en la consulta.

El siguiente ejemplo se uniría a los dos conjuntos de datos siguientes (`your_analytics_table` y `custom_operating_system_lookup`) y crea una instrucción `SELECT` para los 50 sistemas operativos principales por número de vistas de página.

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

| Sistema operativo | Vistas de página |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| Mobile iOS 6.1.3 | 119069,0 |
| Linux | 56516,0 |
| OSX 10.6.8 | 53652,0 |
| Android 4.0.4 | 46167,0 |
| Android 4.0.3 | 31852,0 |
| Windows Server 2003 y XP x64 Edition | 28883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Anulación de duplicación

El servicio de consulta admite la deduplicación de datos o la eliminación de filas duplicadas de los datos. Para obtener más información sobre la deduplicación, lea la [Guía de deduplicación del servicio de consulta](./deduplication.md).

## Pasos siguientes

Al leer este documento, se le han introducido algunas consideraciones importantes al escribir consultas con [!DNL Query Service]. Para obtener más información sobre cómo utilizar la sintaxis SQL para escribir sus propias consultas, lea la [documentación de sintaxis SQL](../sql/syntax.md).

Para obtener más ejemplos de consultas que se pueden utilizar dentro del servicio de consulta, lea las guías sobre [Adobe Analytics sample queries](./adobe-analytics.md), [Adobe Target sample queries](./adobe-target.md) o [ExperienceEvent sample queries](./experience-event-queries.md).
