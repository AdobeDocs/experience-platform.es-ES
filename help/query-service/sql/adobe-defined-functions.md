---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: Funciones definidas por Adobe
topic: functions
description: Este documento proporciona información sobre las funciones definidas por Adobes disponibles en el servicio de Consulta.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 4%

---


# Funciones definidas por Adobe

Las funciones definidas por Adobe (ADF) son funciones prediseñadas en [!DNL Query Service] que ayudan a realizar tareas comunes relacionadas con el negocio en [!DNL ExperienceEvent] los datos. Estas funciones incluyen funciones de sesionización y atribución como las que se encuentran en Adobe Analytics. Consulte la documentación [de](https://docs.adobe.com/content/help/es-ES/analytics/landing/home.html) Adobe Analytics para obtener más información sobre Adobe Analytics y los conceptos subyacentes a las FDA definidas en esta página. Este documento proporciona información para las funciones definidas por Adobe disponibles en [!DNL Query Service].

## Funciones de ventana

La mayoría de la lógica empresarial requiere reunir los puntos de contacto para un cliente y solicitarlos por tiempo. Esta compatibilidad la proporciona [!DNL Spark] SQL en forma de funciones de ventana. Las funciones de ventana forman parte de SQL estándar y son compatibles con muchos otros motores SQL.

Una función de ventana actualiza una agregación y devuelve un solo elemento por cada fila del subconjunto ordenado. La función de agregación más básica es `SUM()`. `SUM()` toma las filas y le da un total. Si, en cambio, aplica `SUM()` a una ventana, convirtiéndola en una función de ventana, recibirá una suma acumulativa con cada fila.

La mayoría de los asistentes de [!DNL Spark] SQL son funciones de ventana que actualizan cada fila de la ventana, con el estado de esa fila añadido.

### Especificación

Sintaxis: `OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| [partición] | Un subgrupo de las filas basadas en una columna o en un campo disponible. Ejemplo, `PARTITION BY endUserIds._experience.mcid.id` |
| [order] | Columna o campo disponible utilizado para ordenar el subconjunto o las filas. Ejemplo, `ORDER BY timestamp` |
| [frame] | Un subgrupo de las filas de una partición. Ejemplo, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sesionización

Cuando se trabaja con [!DNL ExperienceEvent] datos procedentes de un sitio web, una aplicación móvil, un sistema interactivo de respuesta de voz o cualquier otro canal de interacción con el cliente, ayuda que los eventos se puedan agrupar en torno a un período de actividad relacionado. Generalmente, tiene una intención específica de conducir su actividad, como investigar un producto, pagar una factura, comprobar el saldo de la cuenta, rellenar una solicitud, etc. Esta agrupación ayuda a asociar los eventos para descubrir más contexto sobre la experiencia del cliente.

Para obtener más información acerca de la sesionización en Adobe Analytics, consulte la documentación sobre las sesiones [](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)contextual.

### Especificación

Sintaxis: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de hora encontrado en el conjunto de datos |
| `expirationInSeconds` | Cantidad de segundos necesarios entre eventos para calificar el final de la sesión actual y el inicio de una nueva sesión |

| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `timestamp_diff` | Tiempo en segundos entre el registro actual y el registro anterior |
| `num` | Un número de sesión único, comenzando en 1, para la clave definida en la función `PARTITION BY` de ventana. |
| `is_new` | Un booleano que se utiliza para identificar si un registro es el primero de una sesión |
| `depth` | Profundidad del registro actual dentro de la sesión |

#### Consulta de ejemplo

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

#### Resultados

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

## Atribución

Asociar las acciones de los clientes con el éxito es una parte importante para comprender los factores que influyen en la experiencia de los clientes. Las siguientes FDA admiten la atribución primera y última con diferentes configuraciones de caducidad.

Para obtener más información sobre la atribución en Adobe Analytics, consulte la descripción general [de la](https://docs.adobe.com/content/help/es-ES/analytics/analyze/analysis-workspace/panels/attribution.html) Attribution IQ en la Guía [!DNL Analytics] de análisis.

### Atribución de primer toque

Devuelve el valor de atribución de primer toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL ExperienceEvent] . La consulta devuelve un `struct` objeto con el valor de primer toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver qué interacción ha llevado a una serie de acciones de los clientes. En el ejemplo que se muestra a continuación, el código de seguimiento inicial (`em:946426`) de los [!DNL ExperienceEvent] datos se atribuye 100% (`1.0`) de responsabilidad por las acciones del cliente, ya que fue la primera interacción.

### Especificación

Sintaxis: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de hora encontrado en el conjunto de datos |
| `channelName` | Nombre descriptivo que se utilizará como etiqueta en el objeto devuelto |
| `channelValue` | Columna o campo que es el canal de destinatario de la consulta |


| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `name` | La etiqueta `channelName` introducida en el ADF |
| `value` | El valor de `channelValue` ese es el primer toque de la variable [!DNL ExperienceEvent] |
| `timestamp` | Marca de hora del [!DNL ExperienceEvent] lugar en el que se produjo el primer toque |
| `fraction` | Atribución del primer toque expresada como crédito fraccional |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

#### Resultados

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

### Atribución de último toque

Devuelve el valor de atribución de último toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL ExperienceEvent] . La consulta devuelve un `struct` objeto con el valor de último toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver la interacción final en una serie de acciones de cliente. En el ejemplo que se muestra a continuación, el código de seguimiento del objeto devuelto es la última interacción de cada [!DNL ExperienceEvent] registro. A cada código se le atribuye una (`1.0`) responsabilidad del 100 % por las acciones del cliente, ya que fue la última interacción.

### Especificación

Sintaxis: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de hora encontrado en el conjunto de datos |
| `channelName` | Nombre descriptivo que se utilizará como etiqueta en el objeto devuelto |
| `channelValue` | Columna o campo que es el canal de destinatario de la consulta |


| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `name` | La etiqueta `channelName` introducida en el ADF |
| `value` | El valor de `channelValue` ese es el último toque de la variable [!DNL ExperienceEvent] |
| `timestamp` | La marca de tiempo del [!DNL ExperienceEvent] lugar donde se `channelValue` utilizó el |
| `fraction` | Atribución del último toque expresado como crédito fraccional |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Resultados

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

### Atribución de primer toque con condición de caducidad

Devuelve el primer valor de atribución de toque y los detalles de un solo canal del conjunto de datos de destinatario [!DNL ExperienceEvent] , que caducan después o antes de una condición. La consulta devuelve un `struct` objeto con el valor de primer toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver qué interacción llevó a una serie de acciones del cliente dentro de una porción del [!DNL ExperienceEvent] conjunto de datos determinada por una condición de su selección. En el ejemplo que se muestra a continuación, se registra una compra (`commerce.purchases.value IS NOT NULL`) en cada uno de los cuatro días mostrados en los resultados (15, 21, 23 y 29 de julio) y se atribuye al código de seguimiento inicial de cada día la responsabilidad del 100% (`1.0`) por las acciones del cliente.

#### Especificación

Sintaxis: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de hora encontrado en el conjunto de datos |
| `channelName` | Nombre descriptivo que se utilizará como etiqueta en el objeto devuelto |
| `channelValue` | Columna o campo que es el canal de destinatario de la consulta |
| `expCondition` | Condición que determina el punto de caducidad del canal |
| `expBefore` | El valor predeterminado es `false`. Boolean que indica si el canal caduca antes o después de que se cumpla la condición especificada. Principalmente habilitado para condiciones de caducidad de sesión (por ejemplo, `sess.depth = 1, true`), para garantizar que el primer toque no se seleccione de una sesión anterior. |

| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `name` | La etiqueta `channelName` introducida en el ADF |
| `value` | El valor de `channelValue` ese es el primer toque en la [!DNL ExperienceEvent] sección anterior a `expCondition` |
| `timestamp` | Marca de hora del [!DNL ExperienceEvent] lugar en el que se produjo el primer toque |
| `fraction` | Atribución del primer toque expresada como crédito fraccional |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Resultados

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### Atribución de primer toque con tiempo de espera de caducidad

Devuelve el primer valor de atribución de toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL ExperienceEvent] para un período de tiempo especificado. La consulta devuelve un `struct` objeto con el valor de primer toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado. Esta consulta es útil si desea ver qué interacción, dentro de un intervalo de tiempo seleccionado, llevó a una acción del cliente. En el ejemplo que se muestra a continuación, el primer toque que se devuelve para cada acción del cliente es la interacción más temprana en los siete días anteriores (`expTimeout = 86400 * 7`).

#### Especificación

Sintaxis: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de hora encontrado en el conjunto de datos |
| `channelName` | Nombre descriptivo que se utilizará como etiqueta en el objeto devuelto |
| `channelValue` | Columna o campo que es el canal de destinatario de la consulta |
| `expTimeout` | La ventana de tiempo (en segundos) anterior al evento de canal en la que la consulta busca un evento de primer toque |

| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `name` | La etiqueta `channelName` introducida en el ADF |
| `value` | El valor de `channelValue` ese es el primer toque dentro del `expTimeout` intervalo especificado |
| `timestamp` | Marca de hora del [!DNL ExperienceEvent] lugar en el que se produjo el primer toque |
| `fraction` | Atribución del primer toque expresada como crédito fraccional |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Resultados

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### Atribución de último toque con condición de caducidad

Devuelve el valor de atribución de último toque y los detalles de un solo canal del conjunto de datos de destinatario [!DNL ExperienceEvent] , que caducan después o antes de una condición. La consulta devuelve un `struct` objeto con el valor de último toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado. Esta consulta es útil si desea ver la última interacción en una serie de acciones del cliente dentro de una porción del conjunto de datos [!DNL ExperienceEvent] determinada por una condición de su selección. En el ejemplo que se muestra a continuación, se registra una compra (`commerce.purchases.value IS NOT NULL`) en cada uno de los cuatro días mostrados en los resultados (15, 21, 23 y 29 de julio) y se atribuye al último código de seguimiento de cada día la responsabilidad del 100% (`1.0`) por las acciones del cliente.

#### Especificación

Sintaxis: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de hora encontrado en el conjunto de datos |
| `channelName` | Nombre descriptivo que se utilizará como etiqueta en el objeto devuelto |
| `channelValue` | Columna o campo que es el canal de destinatario de la consulta |
| `expCondition` | Condición que determina el punto de caducidad del canal |
| `expBefore` | El valor predeterminado es `false`. Boolean que indica si el canal caduca antes o después de que se cumpla la condición especificada. Principalmente habilitado para condiciones de caducidad de sesión (por ejemplo, `sess.depth = 1, true`), para garantizar que el último toque no se seleccione de una sesión anterior. |

| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `name` | La etiqueta `channelName` introducida en el ADF |
| `value` | El valor de `channelValue` ese es el último toque en la [!DNL ExperienceEvent] sección anterior a `expCondition` |
| `timestamp` | Marca de hora del [!DNL ExperienceEvent] lugar donde se produjo el último toque |
| `percentage` | Atribución del último toque expresado como crédito fraccional |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Resultados

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### Atribución de último toque con tiempo de espera de caducidad

Devuelve el valor de atribución de último toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL ExperienceEvent] para un período de tiempo especificado. La consulta devuelve un `struct` objeto con el valor de último toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado. Esta consulta es útil si desea ver la última interacción dentro de un intervalo de tiempo seleccionado. En el ejemplo que se muestra a continuación, el último toque que se devuelve para cada acción del cliente es la interacción final en los siete días siguientes (`expTimeout = 86400 * 7`).

#### Especificación

Sintaxis: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de hora encontrado en el conjunto de datos |
| `channelName` | Nombre descriptivo que se utilizará como etiqueta en el objeto devuelto |
| `channelValue` | Columna o campo que es el canal de destinatario de la consulta |
| `expTimeout` | La ventana de tiempo (en segundos) posterior al evento de canal en el que la consulta busca un evento de último toque |

| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `name` | La etiqueta `channelName` introducida en el ADF |
| `value` | El valor de `channelValue` ese es el último toque dentro del `expTimeout` intervalo especificado |
| `timestamp` | Marca de hora del [!DNL ExperienceEvent] lugar donde se produjo el último toque |
| `percentage` | Atribución del último toque expresado como crédito fraccional |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Resultados

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

## Toque anterior/siguiente

Es importante comprender cómo navegan los clientes dentro de una experiencia. Se puede utilizar para comprender la profundidad de compromiso del cliente, confirmar que los pasos que se pretenden dar a una experiencia funcionen según lo diseñado e identificar los posibles puntos molestos que afectan al cliente. Las siguientes FDA admiten el establecimiento de vistas de rutas a partir de sus relaciones Anterior y Siguiente. Podrá crear Página anterior y Página siguiente, o pasar por varios eventos para crear Rutas.

### Toque anterior

Determina el valor anterior de un campo concreto a un número definido de pasos dentro de la ventana. Observe en el ejemplo que la `WINDOW` Función está configurada con un marco de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` configuración de ADF para ver la fila actual y todo lo anterior.

#### Especificación

Sintaxis: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `key` | Columna o campo del evento. |
| `shift` | (opcional) El número de eventos que se alejan del evento actual. El valor predeterminado es 1. |
| `ingnoreNulls` | Boolean para indicar si se deben ignorar `key` los valores nulos. El valor predeterminado es `false`. |


| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `value` | El valor basado en el `key` utilizado en el ADF |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### Resultados

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

### Siguiente toque

Determina el siguiente valor de un campo concreto un número definido de pasos dentro de la ventana. Observe en el ejemplo que la `WINDOW` Función está configurada con un marco de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` configuración de ADF para ver la fila actual y todo después.

#### Especificación

Sintaxis: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `key` | Columna o campo del evento |
| `shift` | (opcional) El número de eventos que se alejan del evento actual. El valor predeterminado es 1. |
| `ingnoreNulls` | Boolean para indicar si se deben ignorar `key` los valores nulos. El valor predeterminado es `false`. |


| Parámetros de objeto devueltos | Descripción |
| ---------------------- | ------------- |
| `value` | El valor basado en el `key` utilizado en el ADF |

#### Consulta de ejemplo

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### Resultados

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

## Tiempo transcurrido

El intervalo de tiempo le permite explorar el comportamiento latente del cliente dentro de un período antes o después de que se produzca un evento. Observe los eventos en un plazo de 7 días después de una campaña u otro tipo de evento en todos sus clientes.

### Coincidencia anterior entre el tiempo

Proporciona una nueva dimensión que mide el tiempo transcurrido desde un incidente en particular.

#### Especificación

Sintaxis: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de tiempo encontrado en el conjunto de datos rellenado en todos los eventos. |
| `eventDefintion` | Expresión para calificar el evento anterior. |
| `timeUnit` | Unidad de producto: días, horas, minutos y segundos. El valor predeterminado es segundos. |

Salida: Devuelve un número que representa la unidad de tiempo desde que se vio el evento coincidente anterior o permanece nulo si no se encontró ningún evento coincidente.

#### Consulta de ejemplo

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

#### Resultados

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

### Tiempo transcurrido entre la próxima coincidencia

Proporciona una nueva dimensión que mide el tiempo antes de que se produzca un evento en particular.

#### Especificación

Sintaxis: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])` 

| Parámetro | Descripción |
| --- | --- |
| `timestamp` | Campo de marca de tiempo encontrado en el conjunto de datos rellenado en todos los eventos. |
| `eventDefintion` | Expresión para calificar el próximo evento. |
| `timeUnit` | Unidad de producto: días, horas, minutos y segundos. El valor predeterminado es segundos. |

Salida: Devuelve un número negativo que representa la unidad de tiempo detrás del siguiente evento coincidente o permanece nulo si no se encuentra un evento coincidente.

#### Consulta de ejemplo

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

#### Resultados

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

## Pasos siguientes

Mediante las funciones descritas aquí, puede escribir consultas para acceder a sus propios [!DNL ExperienceEvent] conjuntos de datos mediante [!DNL Query Service]. Para obtener más información sobre la creación de consultas en [!DNL Query Service], consulte la documentación sobre la [creación de consultas](../creating-queries/creating-queries.md).
