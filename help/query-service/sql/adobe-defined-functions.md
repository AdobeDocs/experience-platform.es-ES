---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;funciones definidas por adobe;sql;
solution: Experience Platform
title: Funciones definidas por Adobe
topic: functions
description: Este documento proporciona información sobre las funciones definidas por Adobes disponibles en el servicio de Consulta.
translation-type: tm+mt
source-git-commit: e15229601d35d1155fc9a8ab9296f8c41811ebf9
workflow-type: tm+mt
source-wordcount: '2902'
ht-degree: 2%

---


# Funciones definidas por Adobe

Las funciones definidas por Adobes, en este caso denominadas ADF, son funciones precompiladas en el Servicio de Consulta de Adobe Experience Platform que ayudan a realizar tareas comunes relacionadas con el negocio en datos [!DNL Experience Event]. Entre ellas se incluyen funciones para [sesionización](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) y [atribución](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) como las que se encuentran en Adobe Analytics.

Este documento proporciona información para las funciones definidas por Adobe disponibles en [!DNL Query Service].

## Funciones de ventana {#window-functions}

La mayoría de la lógica empresarial requiere reunir los puntos de contacto para un cliente y solicitarlos por tiempo. Este soporte es proporcionado por [!DNL Spark] SQL en forma de funciones de ventana. Las funciones de ventana forman parte de SQL estándar y son compatibles con muchos otros motores SQL.

Una función de ventana actualiza una agregación y devuelve un solo elemento por cada fila del subconjunto ordenado. La función de agregación más básica es `SUM()`. `SUM()` toma las filas y le da un total. Si en su lugar aplica `SUM()` a una ventana, convirtiéndola en una función de ventana, recibirá una suma acumulativa con cada fila.

La mayoría de los asistentes de SQL [!DNL Spark] son funciones de ventana que actualizan cada fila de la ventana, con el estado de esa fila agregado.

**Sintaxis de consulta**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `{PARTITION}` | Un subgrupo de filas basadas en una columna o en un campo disponible. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Columna o campo disponible utilizado para ordenar el subconjunto o las filas. | `ORDER BY timestamp` |
| `{FRAME}` | Un subgrupo de las filas de una partición. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sesionización

Cuando se trabaja con datos [!DNL Experience Event] procedentes de un sitio web, una aplicación móvil, un sistema interactivo de respuesta de voz o cualquier otro canal de interacción con el cliente, ayuda que los eventos se puedan agrupar en torno a un período de actividad relacionado. Generalmente, tiene una intención específica de conducir su actividad, como investigar un producto, pagar una factura, comprobar el saldo de la cuenta, rellenar una solicitud, etc.

Esta agrupación, o sesionización de datos, ayuda a asociar los eventos para descubrir más contexto sobre la experiencia del cliente.

Para obtener más información sobre la sesionización en Adobe Analytics, consulte la documentación sobre [sesiones contextual](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html.

**Sintaxis de consulta**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{EXPIRATION_IN_SECONDS}` | Cantidad de segundos que se necesitan entre eventos para calificar el final de la sesión actual y el inicio de una nueva sesión. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `session`. La columna `session` está formada por los siguientes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parámetros | Descripción |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Diferencia en tiempo, en segundos, entre el registro actual y el registro anterior. |
| `{NUM}` | Un número de sesión único, comenzando en 1, para la clave definida en la `PARTITION BY` de la función de ventana. |
| `{IS_NEW}` | Un booleano que se utiliza para identificar si un registro es el primero de una sesión. |
| `{DEPTH}` | Profundidad del registro actual dentro de la sesión. |

### SESS_INICIO_IF

Esta consulta devuelve el estado de la sesión de la fila actual, según la marca de tiempo actual y la expresión proporcionada, y inicio una nueva sesión con la fila actual.

**Sintaxis de consulta**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{TEST_EXPRESSION}` | Expresión con la que desea comprobar los campos de los datos. Por ejemplo, `application.launches > 0`. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultados**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `session`. La columna `session` está formada por los siguientes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parámetros | Descripción |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Diferencia en tiempo, en segundos, entre el registro actual y el registro anterior. |
| `{NUM}` | Un número de sesión único, comenzando en 1, para la clave definida en la `PARTITION BY` de la función de ventana. |
| `{IS_NEW}` | Un booleano que se utiliza para identificar si un registro es el primero de una sesión. |
| `{DEPTH}` | Profundidad del registro actual dentro de la sesión. |

### SESS_END_IF

Esta consulta devuelve el estado de la sesión de la fila actual, según la marca de tiempo actual y la expresión proporcionada, finaliza la sesión actual y inicio una nueva sesión en la fila siguiente.

**Sintaxis de consulta**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{TEST_EXPRESSION}` | Expresión con la que desea comprobar los campos de los datos. Por ejemplo, `application.launches > 0`. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultados**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `session`. La columna `session` está formada por los siguientes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parámetros | Descripción |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Diferencia en tiempo, en segundos, entre el registro actual y el registro anterior. |
| `{NUM}` | Un número de sesión único, comenzando en 1, para la clave definida en la `PARTITION BY` de la función de ventana. |
| `{IS_NEW}` | Un booleano que se utiliza para identificar si un registro es el primero de una sesión. |
| `{DEPTH}` | Profundidad del registro actual dentro de la sesión. |

## Atribución

Asociar las acciones de los clientes con el éxito es una parte importante para comprender los factores que influyen en las experiencias de los clientes. Las siguientes ADF admiten atribución de primer toque y atribución de último toque con diferentes ajustes de caducidad.

Para obtener más información sobre la atribución en Adobe Analytics, consulte la [información general de la Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html) en la guía del panel Atribución [!DNL Analytics].

### Atribución de primer toque

Esta consulta devuelve el valor de atribución de primer toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL Experience Event]. La consulta devuelve un objeto `struct` con el valor de primer toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver qué interacción ha llevado a una serie de acciones de los clientes. En el ejemplo que se muestra a continuación, el código de seguimiento inicial (`em:946426`) en los datos [!DNL Experience Event] se atribuye 100% (`1.0`) responsabilidad por las acciones del cliente, ya que fue la primera interacción.

**Sintaxis de consulta**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{CHANNEL_NAME}` | Etiqueta del objeto devuelto. |
| `{CHANNEL_VALUE}` | Columna o campo que es el canal de destinatario de la consulta. |

Encontrará una explicación de los parámetros dentro de `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `first_touch`. La columna `first_touch` está formada por los siguientes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{NAME}` | El `{CHANNEL_NAME}`, que se introdujo como etiqueta en el ADF. |
| `{VALUE}` | El valor de `{CHANNEL_VALUE}` que es el primer toque en el [!DNL Experience Event] |
| `{TIMESTAMP}` | Marca de hora del [!DNL Experience Event] donde se produjo el primer toque. |
| `{FRACTION}` | Atribución del primer toque, expresada como fracción decimal. |

### Atribución de último toque

Esta consulta devuelve el valor de atribución de último toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL Experience Event]. La consulta devuelve un objeto `struct` con el valor de último toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver la interacción final en una serie de acciones de cliente. En el ejemplo que se muestra a continuación, el código de seguimiento en el objeto devuelto es la última interacción en cada registro [!DNL Experience Event]. A cada código se le atribuye una responsabilidad del 100 % (`1.0`) por las acciones del cliente, ya que fue la última interacción.

**Sintaxis de consulta**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{CHANNEL_NAME}` | Etiqueta del objeto devuelto. |
| `{CHANNEL_VALUE}` | Columna o campo que es el canal de destinatario de la consulta. |

Encontrará una explicación de los parámetros dentro de `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `last_touch`. La columna `last_touch` está formada por los siguientes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parámetros | Descripción |
| ---------- | ----------- |
| `{NAME}` | El `{CHANNEL_NAME}`, que se introdujo como etiqueta en el ADF. |
| `{VALUE}` | El valor de `{CHANNEL_VALUE}` que es el último toque del [!DNL Experience Event] |
| `{TIMESTAMP}` | Marca de tiempo del [!DNL Experience Event] donde se utilizó el `channelValue`. |
| `{FRACTION}` | Atribución del último toque, expresada como fracción decimal. |

### Atribución de primer toque con condición de caducidad

Esta consulta devuelve el valor de atribución de primer toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL Experience Event], que caducan después o antes de una condición. La consulta devuelve un objeto `struct` con el valor de primer toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver qué interacción llevó a una serie de acciones del cliente dentro de una porción del conjunto de datos [!DNL Experience Event] determinado por una condición de su elección. En el ejemplo que se muestra a continuación, se registra una compra (`commerce.purchases.value IS NOT NULL`) en cada uno de los cuatro días mostrados en los resultados (15, 21, 23 y 29 de julio) y el código de seguimiento inicial de cada día se atribuye al 100% (`1.0`) responsabilidad por las acciones del cliente.

**Sintaxis de consulta**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{CHANNEL_NAME}` | Etiqueta del objeto devuelto. |
| `{CHANNEL_VALUE}` | Columna o campo que es el canal de destinatario de la consulta. |
| `{EXP_CONDITION}` | Condición que determina el punto de caducidad del canal. |
| `{EXP_BEFORE}` | Un valor booleano que indica si el canal caduca antes o después de que se cumpla la condición especificada, `{EXP_CONDITION}`. Esto se habilita principalmente para las condiciones de caducidad de una sesión, para garantizar que el primer toque no se seleccione en una sesión anterior. De forma predeterminada, este valor se establece en `false`. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `first_touch`. La columna `first_touch` está formada por los siguientes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parámetros | Descripción |
| ---------- | ----------- |
| `{NAME}` | El `{CHANNEL_NAME}`, que se introdujo como etiqueta en el ADF. |
| `{VALUE}` | El valor de `CHANNEL_VALUE}` que es el primer toque de [!DNL Experience Event], antes de `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Marca de hora del [!DNL Experience Event] donde se produjo el primer toque. |
| `{FRACTION}` | Atribución del primer toque, expresada como fracción decimal. |

### Atribución de primer toque con tiempo de espera de caducidad

Esta consulta devuelve el valor de atribución de primer toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL Experience Event] para un período de tiempo especificado. La consulta devuelve un objeto `struct` con el valor de primer toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver qué interacción, dentro de un intervalo de tiempo seleccionado, llevó a una acción del cliente. En el ejemplo que se muestra a continuación, el primer toque que se devuelve para cada acción del cliente es la interacción más temprana en los siete días anteriores (`expTimeout = 86400 * 7`).

**Especificación**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{CHANNEL_NAME}` | Etiqueta del objeto devuelto. |
| `{CHANNEL_VALUE}` | Columna o campo que es el canal de destinatario de la consulta. |
| `{EXP_TIMEOUT}` | La ventana de tiempo anterior al evento de canal, en segundos, que la consulta busca un evento de primer toque. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `first_touch`. La columna `first_touch` está formada por los siguientes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parámetros | Descripción |
| ---------- | ----------- |
| `{NAME}` | El `{CHANNEL_NAME}`, que se introdujo como etiqueta en el ADF. |
| `{VALUE}` | El valor de `CHANNEL_VALUE}` que es el primer toque dentro del intervalo especificado `{EXP_TIMEOUT}`. |
| `{TIMESTAMP}` | Marca de hora del [!DNL Experience Event] donde se produjo el primer toque. |
| `{FRACTION}` | Atribución del primer toque, expresada como fracción decimal. |

### Atribución de último toque con condición de caducidad

Esta consulta devuelve el valor de atribución de último toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL Experience Event], que caducan después o antes de una condición. La consulta devuelve un objeto `struct` con el valor de último toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver la última interacción en una serie de acciones del cliente dentro de una porción del conjunto de datos [!DNL Experience Event] determinado por una condición de su elección. En el ejemplo que se muestra a continuación, se registra una compra (`commerce.purchases.value IS NOT NULL`) en cada uno de los cuatro días mostrados en los resultados (15, 21, 23 y 29 de julio) y el último código de seguimiento de cada día se atribuye al 100% (`1.0`) responsabilidad por las acciones del cliente.

**Sintaxis de consulta**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{CHANNEL_NAME}` | Etiqueta del objeto devuelto. |
| `{CHANNEL_VALUE}` | Columna o campo que es el canal de destinatario de la consulta. |
| `{EXP_CONDITION}` | Condición que determina el punto de caducidad del canal. |
| `{EXP_BEFORE}` | Un valor booleano que indica si el canal caduca antes o después de que se cumpla la condición especificada, `{EXP_CONDITION}`. Esto se habilita principalmente para las condiciones de caducidad de una sesión, para garantizar que el primer toque no se seleccione en una sesión anterior. De forma predeterminada, este valor se establece en `false`. |

**Consulta de ejemplo**

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

**Resultados de ejemplo**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `last_touch`. La columna `last_touch` está formada por los siguientes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parámetros | Descripción |
| ---------- | ----------- |
| `{NAME}` | El `{CHANNEL_NAME}`, que se introdujo como etiqueta en el ADF. |
| `{VALUE}` | El valor de `{CHANNEL_VALUE}` que es el último toque en el [!DNL Experience Event], antes del `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Marca de hora del [!DNL Experience Event] donde se produjo el último toque. |
| `{FRACTION}` | Atribución del último toque, expresada como fracción decimal. |

### Atribución de último toque con tiempo de espera de caducidad

Esta consulta devuelve el valor de atribución de último toque y los detalles de un solo canal en el conjunto de datos de destinatario [!DNL Experience Event] para un período de tiempo especificado. La consulta devuelve un objeto `struct` con el valor de último toque, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

Esta consulta es útil si desea ver la última interacción dentro de un intervalo de tiempo seleccionado. En el ejemplo que se muestra a continuación, el último toque que se devuelve para cada acción del cliente es la interacción final en los siete días siguientes (`expTimeout = 86400 * 7`).

**Sintaxis de consulta**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos. |
| `{CHANNEL_NAME}` | Etiqueta del objeto devuelto |
| `{CHANNEL_VALUE}` | Columna o campo que es el canal de destinatario de la consulta |
| `{EXP_TIMEOUT}` | La ventana de tiempo posterior al evento de canal, en segundos, que la consulta busca un evento de último toque. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `last_touch`. La columna `last_touch` está formada por los siguientes componentes:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parámetros | Descripción |
| ---------- | ----------- |
| `{NAME}` | El `{CHANNEL_NAME}`, introducido como etiqueta en el ADF. |
| `{VALUE}` | El valor de `{CHANNEL_VALUE}` que es el último toque dentro del intervalo especificado `{EXP_TIMEOUT}` |
| `{TIMESTAMP}` | Marca de hora del [!DNL Experience Event] donde se produjo el último toque |
| `{FRACTION}` | Atribución del último toque, expresada como fracción decimal. |

## Control de rutas

Las rutas se pueden utilizar para comprender la profundidad de compromiso del cliente, confirmar que los pasos que se pretenden dar a una experiencia funcionan según lo diseñado e identificar los posibles puntos molestos que afectan al cliente.

Las siguientes FDA admiten el establecimiento de vistas de rutas a partir de sus relaciones anteriores y siguientes. Podrá crear páginas anteriores y páginas siguientes, o pasar por varios eventos para crear rutas.

### Página anterior

Determina el valor anterior de un campo concreto a un número definido de pasos dentro de la ventana. Observe en el ejemplo que la función `WINDOW` está configurada con un marco de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` configuración de ADF para ver la fila actual y todas las filas posteriores.

**Sintaxis de consulta**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{KEY}` | Columna o campo del evento. |
| `{SHIFT}` | (Opcional) El número de eventos fuera del evento actual. De forma predeterminada, el valor es 1. |
| `{IGNORE_NULLS}` | (Opcional) Un valor booleano que indica si se deben ignorar los valores nulos `{KEY}`. De forma predeterminada, el valor es `false`. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `previous_page`. El valor de la columna `previous_page` se basa en el `{KEY}` utilizado en el ADF.

### Página siguiente

Determina el siguiente valor de un campo concreto un número definido de pasos dentro de la ventana. Observe en el ejemplo que la función `WINDOW` está configurada con un marco de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` configuración de ADF para ver la fila actual y todas las filas posteriores.

**Sintaxis de consulta**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{KEY}` | Columna o campo del evento. |
| `{SHIFT}` | (Opcional) El número de eventos fuera del evento actual. De forma predeterminada, el valor es 1. |
| `{IGNORE_NULLS}` | (Opcional) Un valor booleano que indica si se deben ignorar los valores nulos `{KEY}`. De forma predeterminada, el valor es `false`. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `previous_page`. El valor de la columna `previous_page` se basa en el `{KEY}` utilizado en el ADF.

## Tiempo transcurrido

El intervalo de tiempo le permite explorar el comportamiento latente del cliente en un período de tiempo determinado antes o después de que se produzca un evento.

### Coincidencia anterior entre el tiempo

Esta consulta devuelve un número que representa la unidad de tiempo desde que se vio el evento coincidente anterior. Si no se encontró ningún evento coincidente, devuelve null.

**Sintaxis de consulta**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos rellenado en todos los eventos. |
| `{EVENT_DEFINITION}` | La expresión de calificar el evento anterior. |
| `{TIME_UNIT}` | Unidad de salida. El valor posible incluye días, horas, minutos y segundos. De forma predeterminada, el valor es segundos. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `average_minutes_since_registration`. El valor de la columna `average_minutes_since_registration` es la diferencia en tiempo entre los eventos actuales y anteriores. La unidad de tiempo se definió anteriormente en `{TIME_UNIT}`.

### Tiempo transcurrido entre la próxima coincidencia

Esta consulta devuelve un número negativo que representa la unidad de tiempo detrás del siguiente evento coincidente. Si no se encuentra un evento coincidente, se devuelve null.

**Sintaxis de consulta**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Campo de marca de hora que se encuentra en el conjunto de datos rellenado en todos los eventos. |
| `{EVENT_DEFINITION}` | La expresión para calificar al próximo evento. |
| `{TIME_UNIT}` | (Opcional) Unidad de salida. El valor posible incluye días, horas, minutos y segundos. De forma predeterminada, el valor es segundos. |

Encontrará una explicación de los parámetros dentro de la función `OVER()` en la sección [funciones de ventana](#window-functions).

**Consulta de ejemplo**

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

**Resultados**

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

Para la consulta de muestra proporcionada, los resultados se proporcionan en la columna `average_minutes_until_order_confirmation`. El valor de la columna `average_minutes_until_order_confirmation` es la diferencia en tiempo entre los eventos actuales y los siguientes. La unidad de tiempo se definió anteriormente en `{TIME_UNIT}`.

## Pasos siguientes

Mediante las funciones descritas aquí, puede escribir consultas para acceder a sus propios [!DNL Experience Event] conjuntos de datos mediante [!DNL Query Service]. Para obtener más información sobre la creación de consultas en [!DNL Query Service], consulte la documentación sobre [creación de consultas](../best-practices/writing-queries.md).

## Recursos adicionales

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente PSQL. Además, en el vídeo también se utilizan ejemplos de propiedades individuales en un objeto XDM, mediante funciones definidas por Adobe y mediante CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)