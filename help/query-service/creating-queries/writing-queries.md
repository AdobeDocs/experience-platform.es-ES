---
keywords: Experience Platform;home;popular topics;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: Escritura de consultas
topic: queries
type: Tutorial
description: Este documento detalla detalles importantes que deben conocerse al escribir consultas en el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---


# Directrices generales para la ejecución de consultas en [!DNL Query Service]

Este documento detalla detalles importantes que deben conocerse al escribir consultas en Adobe Experience Platform [!DNL Query Service].

Para obtener información detallada sobre la sintaxis SQL utilizada en [!DNL Query Service], lea la documentación [de sintaxis](../sql/syntax.md)SQL.

## Modelos de ejecución de consulta

Adobe Experience Platform [!DNL Query Service] tiene dos modelos de ejecución de consultas: interactiva y no interactiva. La ejecución interactiva se utiliza para el desarrollo de consultas y la generación de informes en las herramientas de inteligencia empresarial, mientras que la no interactiva se utiliza para trabajos más grandes y consultas operativas como parte de un flujo de trabajo de procesamiento de datos.

### Ejecución de consultas interactivas

Las consultas se pueden ejecutar de forma interactiva enviándolas a través de la [!DNL Query Service] interfaz de usuario o [a través de un cliente](../clients/overview.md)conectado. Cuando se ejecuta [!DNL Query Service] a través de un cliente conectado, se ejecuta una sesión activa entre el cliente y [!DNL Query Service] hasta que se devuelve o se agota el tiempo de espera de la consulta enviada.

La ejecución de consultas interactivas tiene las siguientes limitaciones:

| Parámetro | Limitación |
| --------- | ---------- |
| Tiempo de espera de consulta | 10 minutos |
| Máximo de filas devueltas | 50,000 |
| Consultas simultáneas máximas | 5 |

>[!NOTE]
>
>Para anular la limitación máxima de filas, incluya `LIMIT 0` en la consulta. El tiempo de espera de consulta de 10 minutos sigue siendo válido.

De forma predeterminada, los resultados de las consultas interactivas se devuelven al cliente y **no se mantienen** . Para mantener los resultados como un conjunto de datos en [!DNL Experience Platform], la consulta debe utilizar la `CREATE TABLE AS SELECT` sintaxis.

### Ejecución de consultas no interactivas

Las consultas enviadas a través de la [!DNL Query Service] API se ejecutan de forma no interactiva. La ejecución no interactiva significa que [!DNL Query Service] recibe la llamada de API y ejecuta la consulta en el orden en que se recibe. Las consultas no interactivas siempre resultan en la generación de un nuevo conjunto de datos en [!DNL Experience Platform] para recibir los resultados o en la inserción de nuevas filas en un conjunto de datos existente.

## Acceso a un campo específico dentro de un objeto

Para acceder a un campo dentro de un objeto de la consulta, puede utilizar la notación de puntos (`.`) o la notación de corchetes (`[]`). La instrucción SQL siguiente utiliza la notación de puntos para recorrer el `endUserIds` objeto hasta el `mcid` objeto.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | El nombre de la tabla de análisis. |

La instrucción SQL siguiente utiliza la notación de corchetes para recorrer el `endUserIds` objeto hasta el `mcid` objeto.

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
>Dado que cada tipo de anotación devuelve los mismos resultados, el que elija utilizar estará a su preferencia.

Las dos consultas de ejemplo anteriores devuelven un objeto acoplado en lugar de un solo valor:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

El `endUserIds._experience.mcid` objeto devuelto contiene los valores correspondientes para los parámetros siguientes:

- `id`
- `namespace`
- `primary`

Cuando la columna solo se declara en el objeto, devuelve el objeto entero como una cadena. Para vista solo del ID, utilice:

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

## Cuándo utilizar comillas simples, comillas de doble y comillas

En esta sección se explica cuándo utilizar comillas simples, comillas de doble y comillas en consultas.

### Comillas únicas

La comilla simple (`'`) se utiliza para crear cadenas de texto. Por ejemplo, se puede utilizar en la `SELECT` instrucción para devolver un valor de texto estático en el resultado y en la cláusula `WHERE` para evaluar el contenido de una columna.

La siguiente consulta declara un valor de texto estático (`'datasetA'`) para una columna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

La siguiente consulta utiliza una cadena con un solo comillas (`'homepage'`) en su cláusula WHERE para devolver eventos para una página específica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Comillas de doble

La comilla de doble (`"`) se utiliza para declarar un identificador con espacios.

La siguiente consulta utiliza comillas de doble para devolver valores de columnas especificadas cuando una columna contiene un espacio en su identificador:

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
>Las comillas de doble **no se pueden** utilizar con acceso a campo de notación de puntos.

### Comillas secundarias

La comilla `` ` `` trasera se utiliza para omitir los nombres de columna reservados **únicamente** cuando se utiliza la sintaxis de notación de puntos. Por ejemplo, como `order` es una palabra reservada en SQL, debe utilizar comillas para acceder al campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

También se utilizan comillas dobles para acceder a un campo que inicio con un número. Por ejemplo, para acceder al campo `30_day_value`, debe utilizar la notación de comillas invertidas.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Las comillas tipográficas **no son** necesarias si utiliza la notación de corchetes.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Pasos siguientes

Al leer este documento, se le han presentado algunas consideraciones importantes al escribir consultas usando [!DNL Query Service]. Para obtener más información sobre cómo utilizar la sintaxis SQL para escribir sus propias consultas, lea la documentación [de sintaxis](../sql/syntax.md)SQL.