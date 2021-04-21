---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;deduplicación de datos;deduplicación;
solution: Experience Platform
title: Deduplicación de datos en el servicio de consulta
topic-legacy: queries
type: Tutorial
description: 'Este documento describe ejemplos de consultas de muestra completa y subselección para deduplicar tres casos de uso comunes: eventos de experiencias, compras y métricas.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Deduplicación de datos en [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] admite la deduplicación de datos. La deduplicación de datos se puede realizar cuando sea necesario eliminar una fila entera de un cálculo o ignorar un conjunto específico de campos, ya que solo parte de los datos de la fila es información duplicada.

La deduplicación suele implicar el uso de la función `ROW_NUMBER()` en una ventana para un ID (o un par de ID) durante un tiempo ordenado, lo que devuelve un nuevo campo que representa el número de veces que se ha detectado un duplicado. El tiempo se representa a menudo utilizando el campo [!DNL Experience Data Model] (XDM) `timestamp`.

Cuando el valor de `ROW_NUMBER()` es `1`, hace referencia a la instancia original. Por lo general, ese es el caso que desea utilizar. Esto se hará generalmente dentro de una subselección donde la deduplicación se realiza en un `SELECT` de nivel superior, como realizar un recuento agregado.

Los casos de uso de deduplicación pueden ser globales o restringidos a un único usuario o ID de usuario final dentro de `identityMap`.

Este documento describe cómo realizar la deduplicación en tres casos de uso comunes: Eventos de experiencias, compras y métricas.

Cada ejemplo incluye el ámbito, la clave de ventana y un esquema del método de deduplicación, así como la consulta SQL completa.

## Eventos de experiencia {#experience-events}

En el caso de los eventos de experiencia duplicados, es probable que desee ignorar toda la fila.

>[!CAUTION]
>
>Muchos conjuntos de datos de [!DNL Experience Platform], incluidos los producidos por el conector de datos de Adobe Analytics, ya tienen aplicada la deduplicación en el nivel de evento de experiencia. Por lo tanto, volver a aplicar este nivel de deduplicación es innecesario y ralentizará la consulta.
>
>Es importante comprender la fuente de sus conjuntos de datos y saber si ya se ha aplicado la deduplicación en el nivel de Experience-Event. Para cualquier conjunto de datos que se transmita (por ejemplo, los de Adobe Target), **necesitará** aplicar la deduplicación en el nivel de Evento de experiencia, ya que esas fuentes de datos tienen semántica &quot;al menos una vez&quot;.

**Ámbito:** global

**Tecla de ventana:** `id`

### Ejemplo de deduplicación

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Ejemplo completo

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## Compras {#purchases}

Si tiene compras duplicadas, es probable que desee conservar la mayor parte de la fila Evento de experiencia , pero ignore los campos vinculados a la compra (como la métrica `commerce.orders`). Las compras contienen un campo especial para el ID de compra, que es `commerce.order.purchaseID`.

**Ámbito:** Visitante

**Clave de ventana:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Ejemplo de deduplicación

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

### Ejemplo completo

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## Métricas {#metrics}

Si tiene una métrica que utiliza el ID único opcional y aparece un duplicado de ese ID, es probable que desee ignorar ese valor de métrica y mantener el resto del Evento de experiencia.

En XDM, casi todas las métricas utilizan el tipo de datos `Measure` que incluye un campo opcional `id` que puede utilizar para la deduplicación.

**Ámbito:** Visitante

**Clave de ventana:** identityMap[$NAMESPACE].id y objeto id of Measure

### Ejemplo de deduplicación

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### Ejemplo completo

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## Pasos siguientes

Este documento describe cómo realizar la deduplicación de datos dentro del servicio de consulta, así como ejemplos de deduplicación de datos. Para conocer las prácticas recomendadas al escribir consultas mediante el servicio de consulta, lea la [guía de escritura de consultas](./writing-queries.md).
