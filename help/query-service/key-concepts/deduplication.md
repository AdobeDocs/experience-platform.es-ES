---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;desduplicación de datos;desduplicación;
solution: Experience Platform
title: Deduplicación de datos en el servicio de consultas
type: Tutorial
description: 'Este documento describe ejemplos de consultas de subselección y de muestra completa para deduplicar tres casos de uso comunes: eventos de experiencia, compras y métricas.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Deduplicación de datos en [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] admite la deduplicación de datos. La deduplicación de datos se puede realizar cuando es necesario quitar una fila completa de un cálculo o ignorar un conjunto específico de campos porque solo parte de los datos de la fila es información duplicada.

La deduplicación suele implicar el uso de `ROW_NUMBER()` función en una ventana para un ID (o un par de ID) a lo largo del tiempo, lo que devuelve un nuevo campo que representa el número de veces que se ha detectado un duplicado. El tiempo suele representarse mediante el uso de la variable [!DNL Experience Data Model] (XDM) `timestamp` field.

Cuando el valor de la variable `ROW_NUMBER()` es `1`, hace referencia a la instancia original. Por lo general, esa es la instancia que desea utilizar. Esto se suele hacer dentro de una subselección en la que la deduplicación se realiza en un nivel superior `SELECT` como realizar un recuento acumulado.

Los casos de uso de deduplicación pueden ser globales o restringirse a un único ID de usuario o de usuario final dentro de la `identityMap`.

Este documento describe cómo realizar la anulación de duplicación para tres casos de uso comunes: Eventos de experiencia, compras y métricas.

Cada ejemplo incluye el ámbito, la clave de la ventana, una descripción del método de deduplicación, así como la consulta SQL completa.

## Eventos de experiencia {#experience-events}

En el caso de eventos de experiencia duplicados, es probable que desee ignorar toda la fila.

>[!CAUTION]
>
>Muchos conjuntos de datos en [!DNL Experience Platform], incluidas las que produce Adobe Analytics Data Connector, ya tienen aplicada la deduplicación a nivel de evento de experiencia. Por lo tanto, la reaplicación de este nivel de deduplicación es innecesaria y ralentiza la consulta.
>
>Es importante comprender el origen de los conjuntos de datos y saber si ya se ha aplicado la anulación de duplicación a nivel de Experience-Event. Para cualquier conjunto de datos que se transmita por secuencias (por ejemplo, los de Adobe Target), debe **testamento** Es necesario aplicar la deduplicación en el nivel de evento de experiencia, ya que esas fuentes de datos tienen una semántica de &quot;al menos una vez&quot;.

**Ámbito:** Global

**Clave de ventana:** `id`

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

Si tiene compras duplicadas, es probable que desee conservar la mayoría de las [!DNL Experience Event] fila, pero ignore los campos vinculados a la compra (como los `commerce.orders` métrica). Las compras contienen un campo especial para el ID de compra, que es `commerce.order.purchaseID`.

Se recomienda utilizar `purchaseID` dentro del ámbito del visitante, ya que es el campo semántico estándar para los ID de compra dentro de XDM. Se recomienda el ámbito del visitante para eliminar los datos de compra duplicados porque la consulta es más rápida que el ámbito global y es poco probable que un ID de compra se duplique en varios ID de visitante.

**Ámbito:** Visitante

**Clave de ventana:** identityMap[$NAMESPACE].id y commerce.order.purchaseID

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

>[!NOTE]
>
>En algunos casos en los que los datos originales de Analytics tienen ID de compra duplicados en los ID de visitante, puede **mayo** Debe ejecutar el recuento de duplicados del ID de compra en todos los visitantes. Cuando el ID de compra no está presente, este método requiere que incluya una condición que, en su lugar, utilice el ID de evento para mantener la consulta lo más rápido posible.

### Ejemplo completo

El ejemplo siguiente utiliza una cláusula de condición para utilizar el ID de evento en el caso de que el ID de compra no esté presente.

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

Si tiene una métrica que utiliza el ID único opcional y aparece un duplicado de ese ID, probablemente quiera ignorar ese valor de métrica y mantener el resto del Evento de experiencia.

En XDM, casi todas las métricas utilizan el `Measure` tipo de datos que incluye un `id` que puede utilizar para la deduplicación.

**Ámbito:** Visitante

**Clave de ventana:** identityMap[$NAMESPACE].id e id del objeto Measure

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

Este documento proporciona ejemplos de deduplicación de datos y describe cómo realizar la deduplicación de datos dentro del servicio de consultas. Para conocer las prácticas recomendadas al escribir consultas mediante el servicio de consultas, lea la [guía de escritura de consultas](../best-practices/writing-queries.md).
