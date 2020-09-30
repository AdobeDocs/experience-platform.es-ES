---
keywords: Experience Platform;home;popular topics;query service;Query service;data deduplication;deduplication;
solution: Experience Platform
title: Deduplicación de datos
topic: queries
type: Tutorial
description: Este documento describe ejemplos de consulta de muestra completa y subselección para anular la duplicación de tres casos de uso comunes de ExperienceEvents, compras y métricas.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---


# Deduplicación de datos en [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] admite la deduplicación de datos cuando se requiera quitar una fila completa de un cálculo o ignorar un conjunto específico de campos porque sólo una parte de los datos de la fila es un duplicado. El patrón común para la deduplicación implica el uso de la `ROW_NUMBER()` función en una ventana para un ID, o par de ID, durante el tiempo pedido (mediante el campo [!DNL Experience Data Model] (XDM) `timestamp` ) para devolver un nuevo campo que representa el número de veces que se ha detectado un duplicado. Cuando este valor es `1`, hace referencia a la instancia original y, en la mayoría de los casos, a la instancia que desea utilizar, ignorando todas las demás instancias. Esto generalmente se realiza dentro de una subselección donde la deduplicación se realiza en un nivel superior `SELECT` como realizar un recuento acumulado.

## Casos de uso

Algunos casos de uso para la deduplicación son globales en el intervalo de fechas y algunos están restringidos a un solo visitante o ID de usuario final dentro del `identityMap`.

Este documento describe ejemplos de consulta de muestra completos y subselección para la desduplicación de tres casos de uso común:
- [ExperienceEvents](#experienceevents)
- [Compras](#purchases)
- [Métricas](#metrics)

### ExperienceEvents {#experienceevents}

En el caso de duplicado ExperienceEvents, es probable que desee omitir toda la fila.

>[!CAUTION]
>
>Muchos DataSets de [!DNL Experience Platform], incluidos los producidos por el conector de datos de Adobe Analytics, ya tienen aplicada la deduplicación de nivel de ExperienceEvent. Por lo tanto, volver a aplicar este nivel de deduplicación es innecesario y ralentizará la consulta. Es importante comprender la fuente de los DataSets y saber si ya se ha aplicado la deduplicación en el nivel de ExperienceEvent. Para todos los conjuntos de datos que se transmiten (por ejemplo, los de Adobe Target), deberá aplicar la deduplicación de nivel de ExperienceEvent porque dichos orígenes de datos tienen una semántica &#39;al menos una vez&#39;.

**Ámbito:** Global

**Tecla de ventana:** id

#### Subselección

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### Ejemplo completo

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

### Compras {#purchases}

Si tiene compras de duplicados, es probable que desee mantener la mayor parte de la fila ExperienceEvent, pero omitir los campos vinculados a la compra (como la `commerce.orders` métrica). Para las compras, hay un campo especial para el ID de compra. Este campo es `commerce.order.purchaseID`.

**Ámbito:** Visitante

**Tecla de ventana:** identityMap[$ÁREA DE NOMBRES].id &amp; commerce.order.purchaseID

#### Subselección

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

#### Ejemplo completo

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

### Métricas {#metrics}

Si tiene una métrica que utiliza el ID único opcional y aparece un duplicado de dicho ID, es probable que desee omitir ese valor de métrica y mantener el resto del evento ExperienceEvent. En XDM, casi todas las métricas utilizan el tipo `Measure` de datos que incluye un campo opcional `id` que puede utilizar para la deduplicación.

**Ámbito:** Visitante

**Tecla de ventana:** identityMap[$ÁREA DE NOMBRES].id y objeto id of Measure

#### Subselección

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

#### Ejemplo completo

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
