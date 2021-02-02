---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;deduplicación de datos;deduplicación;
solution: Experience Platform
title: Deduplicación de datos
topic: queries
type: Tutorial
description: Este documento describe ejemplos de consulta de muestra completa y subselección para anular la duplicación de tres casos de uso común Eventos de experiencia, compras y métricas.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Deduplicación de datos en [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] admite la deduplicación de datos. La deduplicación de datos se puede realizar cuando se requiere eliminar una fila completa de un cálculo o ignorar un conjunto específico de campos porque sólo una parte de los datos de la fila es información de duplicado.

La deduplicación suele implicar el uso de la función `ROW_NUMBER()` en una ventana para un ID (o un par de ID) a lo largo del tiempo ordenado, que devuelve un nuevo campo que representa el número de veces que se ha detectado un duplicado. El tiempo suele representarse mediante el campo [!DNL Experience Data Model] (XDM) `timestamp`.

Cuando el valor de `ROW_NUMBER()` es `1`, hace referencia a la instancia original. En general, es la instancia que desea utilizar. Esto generalmente se realiza dentro de una subselección donde la deduplicación se realiza en un `SELECT` nivel superior, como realizar un recuento acumulado.

Los casos de uso de deduplicación pueden ser globales o restringidos a un único ID de usuario o usuario final dentro de `identityMap`.

Este documento describe cómo realizar la deduplicación en tres casos de uso común: Eventos, compras y métricas de experiencia.

Cada ejemplo incluye el ámbito, la clave de ventana y un esquema del método de deduplicación, así como la consulta SQL completa.

## Eventos de experiencias {#experience-events}

En el caso de los Eventos de experiencias de duplicado, es probable que desee omitir toda la fila.

>[!CAUTION]
>
>Muchos conjuntos de datos de [!DNL Experience Platform], incluidos los producidos por el conector de datos de Adobe Analytics, ya tienen aplicada la deduplicación de nivel de Evento de experiencias. Por lo tanto, volver a aplicar este nivel de deduplicación es innecesario y ralentizará la consulta.
>
>Es importante comprender el origen de los conjuntos de datos y saber si ya se ha aplicado la deduplicación en el nivel de Evento de experiencias. Para todos los conjuntos de datos que se transmiten (por ejemplo, los de Adobe Target), **deberá** aplicar la deduplicación de nivel de Evento de experiencia, ya que dichos orígenes de datos tienen semántica &quot;al menos una vez&quot;.

**Ámbito:** Global

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

Si tiene compras de duplicados, es probable que desee mantener la mayor parte de la fila del Evento de experiencias, pero omitir los campos vinculados a la compra (como la métrica `commerce.orders`). Las compras contienen un campo especial para la ID de compra, que es `commerce.order.purchaseID`.

**Ámbito:** Visitante

**Clave de ventana:** identityMap[$ÁREA DE NOMBRES].id &amp; commerce.order.purchaseID

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

Si tiene una métrica que utiliza el ID único opcional y aparece un duplicado de dicho ID, es probable que desee omitir ese valor de métrica y mantener el resto del Evento de experiencias.

En XDM, casi todas las métricas utilizan el tipo de datos `Measure` que incluye un campo `id` opcional que puede utilizar para la deduplicación.

**Ámbito:** Visitante

**Clave de ventana:** identityMap[$ÁREA DE NOMBRES].id y objeto id de medida

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

Este documento describe cómo realizar la deduplicación de datos dentro del servicio de Consulta, así como ejemplos de deduplicación de datos. Para obtener más información sobre las prácticas recomendadas al escribir consultas mediante el servicio de Consulta, lea la [guía de consultas de escritura](./writing-queries.md).