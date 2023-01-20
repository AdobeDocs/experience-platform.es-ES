---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;deduplicación de datos;deduplicación;
solution: Experience Platform
title: Deduplicación de datos en el servicio de consulta
type: Tutorial
description: 'Este documento describe ejemplos de consultas de muestra completa y subselección para deduplicar tres casos de uso comunes: eventos de experiencias, compras y métricas.'
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Deduplicación de datos en [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] admite la deduplicación de datos. La deduplicación de datos se puede realizar cuando sea necesario eliminar una fila entera de un cálculo o ignorar un conjunto específico de campos, ya que solo parte de los datos de la fila es información duplicada.

La deduplicación suele implicar el uso de `ROW_NUMBER()` en una ventana para un ID (o un par de ID) a lo largo del tiempo ordenado, que devuelve un nuevo campo que representa el número de veces que se ha detectado un duplicado. La hora a menudo se representa usando la variable [!DNL Experience Data Model] (XDM) `timestamp` campo .

Cuando el valor de la variable `ROW_NUMBER()` es `1`, hace referencia a la instancia original. Por lo general, ese es el caso que desea utilizar. Esto se hará generalmente dentro de una subselección donde la deduplicación se realiza en un nivel superior `SELECT` como realizar un recuento acumulado.

Los casos de uso de deduplicación pueden ser globales o estar limitados a un único usuario o ID de usuario final dentro del `identityMap`.

Este documento describe cómo realizar la deduplicación en tres casos de uso comunes: Eventos de experiencias, compras y métricas.

Cada ejemplo incluye el ámbito, la clave de ventana y un esquema del método de deduplicación, así como la consulta SQL completa.

## Eventos de experiencias {#experience-events}

En el caso de los eventos de experiencia duplicados, es probable que desee ignorar toda la fila.

>[!CAUTION]
>
>Muchos conjuntos de datos en [!DNL Experience Platform], incluidas las producidas por el conector de datos de Adobe Analytics, ya tienen aplicada la deduplicación en el nivel de evento de experiencia. Por lo tanto, volver a aplicar este nivel de deduplicación es innecesario y ralentizará la consulta.
>
>Es importante comprender la fuente de sus conjuntos de datos y saber si ya se ha aplicado la deduplicación en el nivel de Experience-Event. Para cualquier conjunto de datos que se transmita (por ejemplo, los de Adobe Target), puede **will** debe aplicar deduplicación en el nivel de evento de experiencia, ya que esas fuentes de datos tienen semántica &quot;al menos una vez&quot;.

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

Si tiene compras duplicadas, es probable que desee conservar la mayor parte de la variable [!DNL Experience Event] , pero omita los campos vinculados a la compra (como el `commerce.orders` métrica). Las compras contienen un campo especial para el ID de compra, que es `commerce.order.purchaseID`.

Se recomienda utilizar `purchaseID` dentro del ámbito del visitante, ya que es el campo semántico estándar para los ID de compra dentro de XDM. Se recomienda el ámbito del visitante para eliminar los datos de compra duplicados, ya que la consulta es más rápida que el uso del ámbito global y es poco probable que se duplique un ID de compra en varios ID de visitante.

**Ámbito:** Visitante

**Tecla de ventana:** identityMap[$NAMESPACE].id y commerce.order.purchaseID

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
>En algunos casos en los que los datos originales de Analytics tienen ID de compra duplicados en los ID de visitante, puede **may** es necesario ejecutar el recuento de duplicados del ID de compra en todos los visitantes. Cuando el ID de compra no está presente, este método requiere que incluya una condición que, en su lugar, utilice el ID de evento para mantener la consulta lo más rápido posible.

### Ejemplo completo

El ejemplo siguiente utiliza una cláusula de condición para utilizar el ID de evento en caso de que el ID de compra no esté presente.

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

En XDM, casi todas las métricas utilizan la variable `Measure` tipo de datos que incluye una `id` que puede utilizar para la deduplicación.

**Ámbito:** Visitante

**Tecla de ventana:** identityMap[$NAMESPACE].id e id del objeto Measure

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

En este documento se proporcionan ejemplos de deduplicación de datos y se describe cómo realizar la deduplicación de datos dentro de Query Service. Para conocer las prácticas recomendadas al escribir consultas mediante el servicio de consulta, lea la [guía de escritura de consultas](../best-practices/writing-queries.md).
