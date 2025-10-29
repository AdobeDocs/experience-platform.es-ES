---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;funciones definidas por adobe;sql;
solution: Experience Platform
title: Funciones SQL definidas por Adobe en el servicio de consultas
description: Este documento proporciona información sobre las funciones definidas por Adobe disponibles en Adobe Experience Platform Query Service.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 2%

---

# Funciones SQL definidas por Adobe en el servicio de consultas

Las funciones definidas por Adobe, denominadas en este documento ADF, son funciones prediseñadas en Adobe Experience Platform Query Service que ayudan a realizar tareas comunes relacionadas con la empresa en datos de [!DNL Experience Event]. Estas incluyen funciones para [Sessionization](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) y [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) como las que se encuentran en Adobe Analytics.

Este documento proporciona información para las funciones definidas por Adobe disponibles en [!DNL Query Service].

>[!NOTE]
>
>El Experience Cloud ID (ECID) también se conoce como MCID y sigue utilizándose en áreas de nombres.

## Funciones de ventana {#window-functions}

La mayor parte de la lógica empresarial requiere recopilar los puntos de contacto de un cliente y pedirlos por tiempo. Esta compatibilidad la proporciona [!DNL Spark] SQL en forma de funciones de ventana. Las funciones de ventana forman parte de SQL estándar y son compatibles con muchos otros motores SQL.

Una función de ventana actualiza una agregación y devuelve un solo elemento para cada fila del subconjunto ordenado. La función de agregación más básica es `SUM()`. `SUM()` toma sus filas y le proporciona un total. Si en su lugar aplica `SUM()` a una ventana, convirtiéndola en una función de ventana, recibirá una suma acumulativa con cada fila.

La mayoría de los [!DNL Spark] ayudantes de SQL son funciones de ventana que actualizan cada fila de la ventana, con el estado de esa fila agregado.

**Sintaxis de consulta**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `{PARTITION}` | Subgrupo de filas basado en una columna o campo disponible. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Columna o campo disponible que se utiliza para ordenar el subconjunto o las filas. | `ORDER BY timestamp` |
| `{FRAME}` | Un subgrupo de las filas de una partición. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionization

Cuando trabaja con datos de [!DNL Experience Event] procedentes de un sitio web, una aplicación móvil, un sistema de respuesta de voz interactivo o cualquier otro canal de interacción de clientes, resulta útil agrupar los eventos en torno a un período de actividad relacionado. Normalmente, tiene una intención específica que impulsa su actividad como investigar un producto, pagar una factura, comprobar el saldo de la cuenta, rellenar una solicitud, etc.

Esta agrupación, o sesionización de datos, ayuda a asociar los eventos para descubrir más contexto sobre la experiencia del cliente.

Para obtener más información acerca de la creación de sesiones en Adobe Analytics, consulte la documentación de [sesiones según el contexto](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Sintaxis de consulta**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | El campo de marca de tiempo se encuentra en el conjunto de datos. |
| `{EXPIRATION_IN_SECONDS}` | La cantidad de segundos necesarios entre los eventos para calificar el final de la sesión actual y el inicio de una nueva sesión. |

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
|----------------------------------+-----------------------+--------------------
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

Para la consulta de ejemplo dada, los resultados se dan en la columna `session`. La columna `session` está compuesta por los siguientes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parámetros | Descripción |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Diferencia de tiempo, en segundos, entre el registro actual y el anterior. |
| `{NUM}` | Un número de sesión único, que comienza en 1, para la clave definida en `PARTITION BY` de la función de ventana. |
| `{IS_NEW}` | Un booleano utilizado para identificar si un registro es el primero de una sesión. |
| `{DEPTH}` | Profundidad del registro actual dentro de la sesión. |

### SESS_START_IF

Esta consulta devuelve el estado de la sesión de la fila actual, en función de la marca de tiempo actual y la expresión dada, e inicia una nueva sesión con la fila actual.

**Sintaxis de consulta**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | El campo de marca de tiempo se encuentra en el conjunto de datos. |
| `{TEST_EXPRESSION}` | Expresión con la que se desea comprobar los campos de los datos. Por ejemplo, `application.launches > 0`. |

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
|----------------------------------+-----------------------+----------+--------------------
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

Para la consulta de ejemplo dada, los resultados se dan en la columna `session`. La columna `session` está compuesta por los siguientes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parámetros | Descripción |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Diferencia de tiempo, en segundos, entre el registro actual y el anterior. |
| `{NUM}` | Un número de sesión único, que comienza en 1, para la clave definida en `PARTITION BY` de la función de ventana. |
| `{IS_NEW}` | Un booleano utilizado para identificar si un registro es el primero de una sesión. |
| `{DEPTH}` | Profundidad del registro actual dentro de la sesión. |

### SESS_END_IF

Esta consulta devuelve el estado de la sesión de la fila actual, en función de la marca de tiempo actual y la expresión dada, finaliza la sesión actual e inicia una nueva sesión en la fila siguiente.

**Sintaxis de consulta**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | El campo de marca de tiempo se encuentra en el conjunto de datos. |
| `{TEST_EXPRESSION}` | Expresión con la que se desea comprobar los campos de los datos. Por ejemplo, `application.launches > 0`. |

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
|----------------------------------+-----------------------+----------+--------------------
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

Para la consulta de ejemplo dada, los resultados se dan en la columna `session`. La columna `session` está compuesta por los siguientes componentes:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parámetros | Descripción |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Diferencia de tiempo, en segundos, entre el registro actual y el anterior. |
| `{NUM}` | Un número de sesión único, que comienza en 1, para la clave definida en `PARTITION BY` de la función de ventana. |
| `{IS_NEW}` | Un booleano utilizado para identificar si un registro es el primero de una sesión. |
| `{DEPTH}` | Profundidad del registro actual dentro de la sesión. |


## Control de rutas

Las rutas se pueden utilizar para comprender la profundidad de la participación del cliente, confirmar que los pasos previstos de una experiencia funcionan según lo diseñado e identificar los posibles puntos problemáticos que afectan al cliente.

Los siguientes ADF admiten el establecimiento de vistas de rutas desde sus relaciones anteriores y siguientes. Podrá crear páginas anteriores y páginas siguientes, o recorrer varios eventos para crear rutas.

### Página anterior

Determina el valor anterior de un campo concreto a una cantidad definida de pasos de distancia dentro de la ventana. Observe en el ejemplo que la función `WINDOW` está configurada con un fotograma de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` que configura el ADF para que observe la fila actual y todas las filas subsiguientes.

**Sintaxis de consulta**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{KEY}` | La columna o campo del evento. |
| `{SHIFT}` | (Opcional) El número de eventos que no están en el evento actual. El valor predeterminado es 1. |
| `{IGNORE_NULLS}` | (Opcional) Un booleano que indica si se deben ignorar los valores nulos de `{KEY}`. De manera predeterminada, el valor es `false`. |

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
|-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
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

Para la consulta de ejemplo dada, los resultados se dan en la columna `previous_page`. El valor dentro de la columna `previous_page` se basa en `{KEY}` utilizado en el ADF.

### Página siguiente

Determina el siguiente valor de un campo concreto a un número definido de pasos de distancia dentro de la ventana. Observe en el ejemplo que la función `WINDOW` está configurada con un fotograma de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` que configura el ADF para que observe la fila actual y todas las filas subsiguientes.

**Sintaxis de consulta**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{KEY}` | La columna o campo del evento. |
| `{SHIFT}` | (Opcional) El número de eventos que no están en el evento actual. El valor predeterminado es 1. |
| `{IGNORE_NULLS}` | (Opcional) Un booleano que indica si se deben ignorar los valores nulos de `{KEY}`. De manera predeterminada, el valor es `false`. |

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
|-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
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

Para la consulta de ejemplo dada, los resultados se dan en la columna `previous_page`. El valor dentro de la columna `previous_page` se basa en `{KEY}` utilizado en el ADF.

## Tiempo-entre

El intervalo de tiempo permite explorar el comportamiento latente del cliente en un período de tiempo determinado antes o después de que se produzca un evento.

### Tiempo entre la coincidencia anterior

Esta consulta devuelve un número que representa la unidad de tiempo desde que se vio el evento coincidente anterior. Si no se encuentra ningún evento coincidente, devuelve nulo.

**Sintaxis de consulta**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Se ha encontrado un campo de marca de tiempo en el conjunto de datos rellenado en todos los eventos. |
| `{EVENT_DEFINITION}` | La expresión para calificar el evento anterior. |
| `{TIME_UNIT}` | La unidad de salida. Los valores posibles incluyen días, horas, minutos y segundos. De forma predeterminada, el valor es segundos. |

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
|-----------------------------------+------------------------------------
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

Para la consulta de ejemplo dada, los resultados se dan en la columna `average_minutes_since_registration`. El valor dentro de la columna `average_minutes_since_registration` es la diferencia de tiempo entre los eventos actuales y anteriores. La unidad de tiempo se definió previamente en `{TIME_UNIT}`.

### Tiempo entre la siguiente coincidencia

Esta consulta devuelve un número negativo que representa la unidad de tiempo detrás del siguiente evento coincidente. Si no se encuentra un evento coincidente, se devuelve nulo.

**Sintaxis de consulta**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TIMESTAMP}` | Se ha encontrado un campo de marca de tiempo en el conjunto de datos rellenado en todos los eventos. |
| `{EVENT_DEFINITION}` | La expresión para calificar el siguiente evento. |
| `{TIME_UNIT}` | (Opcional) La unidad de salida. Los valores posibles incluyen días, horas, minutos y segundos. De forma predeterminada, el valor es segundos. |

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
|-----------------------------------+------------------------------------------
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

Para la consulta de ejemplo dada, los resultados se dan en la columna `average_minutes_until_order_confirmation`. El valor dentro de la columna `average_minutes_until_order_confirmation` es la diferencia de tiempo entre los eventos actual y siguiente. La unidad de tiempo se definió previamente en `{TIME_UNIT}`.

## Próximos pasos

Con las funciones descritas aquí, puede escribir consultas para acceder a sus propios conjuntos de datos de [!DNL Experience Event] mediante [!DNL Query Service]. Para obtener más información sobre la creación de consultas en [!DNL Query Service], consulte la documentación sobre [creación de consultas](../best-practices/writing-queries.md).

## Recursos adicionales

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente SQL. Además, el vídeo también utiliza ejemplos que implican propiedades individuales en un objeto XDM, utilizando funciones definidas por Adobe y utilizando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
