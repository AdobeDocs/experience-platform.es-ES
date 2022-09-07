---
title: Análisis de atribución
description: En este documento se explica cómo utilizar el servicio de consulta para crear una técnica de medición de la eficacia de marketing basada en el modelo de atribución de marketing de primer y último contacto.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# Análisis de atribución

La atribución es un concepto analítico que ayuda a determinar las tácticas de marketing, como canales, ofertas y mensajes, que contribuyen a las ventas o conversiones del negocio. Este concepto evalúa el recorrido del consumidor (el proceso mediante el cual un cliente interactúa con una empresa para lograr un objetivo) que resulta en una compra o adquisición basada en puntos de contacto del cliente (cada vez que un consumidor interactúa con su marca). A través del análisis de atribución, los especialistas en marketing pueden evaluar el retorno de la inversión de los canales que los conectan con un cliente potencial.

## Primeros pasos

Los ejemplos SQL de este documento son consultas que normalmente se utilizan con datos de Adobe Analytics. Este tutorial requiere una comprensión práctica de los siguientes componentes:

* [Información general sobre el conector de origen de Adobe Analytics para los datos del grupo de informes](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [La documentación de asignaciones de campos de Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) proporciona más información sobre la ingesta y asignación de datos de análisis para su uso con el servicio de consulta.
* [Información general sobre la Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=es)
* [La guía del panel Atribución de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=es).

Una explicación de los parámetros dentro de la variable `OVER()` se puede encontrar en la variable [sección funciones de ventana](../sql/adobe-defined-functions.md#window-functions). La variable [Glosario de términos comerciales y de marketing de Adobe](https://business.adobe.com/glossary/index.html) también puede ser de uso.

Para cada uno de los siguientes casos de uso, se proporciona un ejemplo de consulta SQL parametrizada como plantilla que puede personalizar. Proporcione parámetros donde quiera que vea `{ }` en los ejemplos SQL que le interesen evaluar.

## Objetivos

Un caso de uso de atribución utiliza datos de Adobe Analytics para ayudar a asociar acciones de clientes a un resultado exitoso. Esta asociación es una parte fundamental para comprender los factores que influyen en las experiencias de los clientes. Los datos de análisis de atribución se pueden utilizar para comprender la importancia del punto de contacto de un cliente durante el recorrido con él.

Los ejemplos de consultas contenidos en este documento admiten varios casos de uso para la atribución de primer toque y de último toque con diferentes configuraciones de caducidad. Esta guía ilustra los siguientes conceptos clave:

* Atribución de primer contacto y último contacto.
* Atribución de primer contacto y último contacto con tiempo de espera de caducidad.
* Atribución de primer contacto y último contacto con condición de caducidad.

## Parámetros de consulta de atribución {#attribution-query-parameters}

La tabla siguiente proporciona un desglose de los parámetros y sus descripciones utilizados en las consultas de atribución de primer contacto y último contacto:

| Parámetro | Descripción |
|---|---|
| `{TIMESTAMP}` | Campo de marca de tiempo encontrado en el conjunto de datos. |
| `{CHANNEL_NAME}` | Etiqueta del objeto devuelto. |
| `{CHANNEL_VALUE}` | La columna o campo que es el canal de destino de la consulta. |
| `{EXP_TIMEOUT}` | Período de tiempo previo al evento de canal, en segundos, que la consulta busca un evento de primer contacto. |
| `{EXP_CONDITION}` | Condición que determina el punto de caducidad del canal. |
| `{EXP_BEFORE}` | Un booleano que indica si el canal caduca antes o después de la condición especificada, `{EXP_CONDITION}`, se cumple. Esto se habilita principalmente para las condiciones de caducidad de una sesión, para garantizar que no se seleccione el primer contacto de una sesión anterior. De forma predeterminada, este valor se establece en `false`. |

## Componentes de columna de resultados de consulta {#query-result-column-components}

Los resultados de las consultas de atribución se proporcionan en la variable `first_touch` o `last_touch` para abrir el Navegador. Estas columnas están formadas por los siguientes componentes:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parámetros | Descripción |
| ---------- | ----------- |
| `{NAME}` | La variable `{CHANNEL_NAME}`, introducido como etiqueta en Azure Data Factory (ADF). |
| `{VALUE}` | El valor de `{CHANNEL_VALUE}` que es el último contacto dentro del `{EXP_TIMEOUT}` intervalo |
| `{TIMESTAMP}` | La marca de tiempo del [!DNL Experience Event] donde se produjo el último contacto |
| `{FRACTION}` | Atribución del último contacto, expresada como fracción decimal. |

### Atribución de primer contacto {#first-touch}

La atribución de primer contacto acredita el 100% de la responsabilidad por un resultado exitoso en el canal inicial que encontró el consumidor. Este ejemplo SQL se utiliza para resaltar la interacción que condujo a una serie posterior de acciones del cliente.

La siguiente consulta devuelve el valor de atribución de primer contacto y los detalles del canal en el destino [!DNL Experience Event] conjunto de datos. También devuelve un valor `struct` para el canal seleccionado con el valor de primer contacto, la marca de tiempo y la atribución para cada fila.

>[!NOTE]
>
>El ID de Experience Cloud (ECID) también se conoce como MCID y se sigue utilizando en áreas de nombres.

**Sintaxis de la consulta**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Para obtener una lista completa de los parámetros potencialmente necesarios y sus descripciones, consulte la [sección parámetros de consulta de atribución](#attribution-query-parameters).

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

En los resultados siguientes, el código de seguimiento inicial `em:946426` se toma de la variable [!DNL Experience Event] conjunto de datos. Este código de seguimiento se atribuye al 100 % (`1.0`) de la responsabilidad de las acciones del cliente porque fue la primera interacción.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obtener un desglose de los resultados mostrados en la variable `first_touch` , consulte la [sección de componentes de columna](#query-result-column-components).

### Atribución de último contacto {#second-touch}

La atribución de último contacto acredita el 100% de la responsabilidad por un resultado exitoso al último canal con el que se encontró el consumidor. Este ejemplo SQL se utiliza para resaltar la interacción final en una serie de acciones del cliente.

La consulta devuelve el valor de atribución de último contacto y los detalles del canal en el destino [!DNL Experience Event] conjunto de datos. También devuelve un valor `struct` para el canal seleccionado con el valor de último contacto, la marca de tiempo y la atribución para cada fila.

**Sintaxis de la consulta**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

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

En los resultados mostrados a continuación, el código de seguimiento del objeto devuelto es la última interacción de cada [!DNL Experience Event] registro. Cada código se atribuye al 100% (`1.0`) responsabilidad por las acciones del cliente, ya que fue la última interacción.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
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

Para obtener un desglose de los resultados mostrados en la variable `last_touch` , consulte la [sección de componentes de columna](#query-result-column-components).

### Atribución de primer contacto con condición de caducidad {#first-touch-attribution-with-expiration-condition}

Esta consulta se utiliza para ver qué interacción llevó a una serie de acciones del cliente dentro de una parte del [!DNL Experience Event] conjunto de datos determinado por una condición de su elección.

La consulta devuelve el valor de atribución de primer contacto y los detalles de un solo canal en el destino [!DNL Experience Event] conjunto de datos, que caduca después o antes de una condición. También devuelve un valor `struct` objeto con el valor de primer contacto, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

**Sintaxis de la consulta**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obtener una lista completa de los parámetros potencialmente necesarios y sus descripciones, consulte la [sección parámetros de consulta de atribución](#attribution-query-parameters).

**Consulta de ejemplo**

En el ejemplo que se muestra a continuación, se registra una compra (`commerce.purchases.value IS NOT NULL`) en cada uno de los cuatro días que se muestran en los resultados (15, 21, 23 y 29 de julio), y el código de seguimiento inicial de cada día se atribuye al 100 % (`1.0`) responsabilidad por las acciones del cliente.

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
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obtener un desglose de los resultados mostrados en la variable `first_touch` , consulte la [sección de componentes de columna](#query-result-column-components).

### Atribución de primer contacto con tiempo de espera de caducidad {#first-touch-attribution-with-expiration-timeout}

Esta consulta se utiliza para encontrar la interacción, dentro de un período de tiempo seleccionado, que condujo a la acción correcta del cliente.

La siguiente consulta devuelve el valor de atribución de primer contacto y los detalles de un solo canal en el destino [!DNL Experience Event] conjunto de datos de un período de tiempo especificado. La consulta devuelve un valor `struct` objeto con el valor de primer contacto, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

**Sintaxis de la consulta**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obtener una lista completa de los parámetros potencialmente necesarios y sus descripciones, consulte la [sección parámetros de consulta de atribución](#attribution-query-parameters).

**Consulta de ejemplo**

En el ejemplo que se muestra a continuación, el primer contacto devuelto para cada acción del cliente es la primera interacción dentro de los siete días anteriores (expTimeout = 86400 * 7).

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
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Para obtener un desglose de los resultados mostrados en la variable `first_touch` , consulte la [sección de componentes de columna](#query-result-column-components).

### Atribución de último contacto con condición de caducidad {#last-touch-attribution-with-expiration-condition}

Esta consulta se utiliza para encontrar la última interacción en una serie de acciones del cliente dentro de una parte de la variable [!DNL Experience Event] conjunto de datos determinado por una condición de su elección.

La siguiente consulta devuelve el valor de atribución de último contacto y los detalles de un solo canal en el destino [!DNL Experience Event] conjunto de datos, que caduca después o antes de una condición. La consulta devuelve un valor `struct` objeto con el valor de último contacto, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

**Sintaxis de la consulta**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obtener una lista completa de los parámetros potencialmente necesarios y sus descripciones, consulte la [sección parámetros de consulta de atribución](#attribution-query-parameters).

**Consulta de ejemplo**

En el ejemplo que se muestra a continuación, se registra una compra (`commerce.purchases.value IS NOT NULL`) en cada uno de los cuatro días que se muestran en los resultados (15, 21, 23 y 29 de julio), y el último código de seguimiento de cada día se atribuye al 100 % (`1.0`) responsabilidad por las acciones del cliente.

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
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
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

Para obtener un desglose de los resultados mostrados en la variable `last_touch` , consulte la [sección de componentes de columna](#query-result-column-components).

### Atribución de último contacto con tiempo de espera de caducidad {#last-touch-attribution-with-expiration-timeout}

Esta consulta se utiliza para encontrar la última interacción dentro de un intervalo de tiempo seleccionado. La consulta devuelve el valor de atribución de último contacto y los detalles de un solo canal en el destino [!DNL Experience Event] conjunto de datos de un período de tiempo especificado. La consulta devuelve un valor `struct` objeto con el valor de último contacto, la marca de tiempo y la atribución para cada fila devuelta para el canal seleccionado.

**Sintaxis de la consulta**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Para obtener una lista completa de los parámetros potencialmente necesarios y sus descripciones, consulte la [sección parámetros de consulta de atribución](#attribution-query-parameters).

**Consulta de ejemplo**

En el ejemplo que se muestra a continuación, el último contacto devuelto para cada acción del cliente es la interacción final en los siete días siguientes (`expTimeout = 86400 * 7`).

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

Para obtener un desglose de los resultados mostrados en la variable `last_touch` , consulte la [sección de componentes de columna](#query-result-column-components).
