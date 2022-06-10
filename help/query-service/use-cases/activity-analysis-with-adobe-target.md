---
title: Análisis De Actividad Con Adobe Target
description: En este documento se explica cómo utilizar el servicio de consulta para crear perspectivas procesables a partir de conjuntos de datos creados con los datos de Adobe Target.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Análisis de actividades con Adobe Target

Adobe Experience Platform le permite introducir datos de Adobe Target mediante campos del Modelo de datos de experiencia (XDM) para crear conjuntos de datos para utilizarlos con el servicio de consulta. Como Adobe Target está diseñado para personalizar el contenido y las experiencias de los usuarios, las consultas que se ejecutan en estos conjuntos de datos permiten perspectivas altamente personalizadas y centradas mediante el análisis de la actividad de los usuarios a través de SQL.

Este documento proporciona una variedad de consultas SQL de muestra que muestran casos de uso comunes en función de los comportamientos y características de los clientes.

## Primeros pasos

Para cada uno de los siguientes casos de uso, se proporciona un ejemplo de consulta SQL parametrizada como plantilla que puede personalizar. Proporcione parámetros donde quiera que vea `{ }` en los ejemplos SQL que le interesen evaluar.

## Asignación parcial de campos XDM de alto nivel

En la tabla siguiente se enumeran los campos comunes de Target y los campos XDM correspondientes a los que se asignan.

>[!NOTE]
>
>El uso de `[ ]` en el campo XDM denota una matriz.

| Nombre del campo de destino | Nombre de campo XDM | Notas |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | N/A |
| ID de actividad | `_experience.target.activities.activityID` | N/D |
| ID de la experiencia | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | N/D |
| ID de segmento | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | N/D |
| Alcance del evento | `_experience.target.activities[].activityEvents[].eventScope` | Este campo rastrea nuevos visitantes y visitas. |
| ID de paso | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Este campo es un ID de paso personalizado para Adobe Campaign. |
| Precio total | commerce.order.priceTotal | N/D |

>[!IMPORTANT]
>
>El nombre de un conjunto de datos creado automáticamente con datos de Target es &quot;Adobe Target Experience Events&quot;. Cuando utilice este conjunto de datos con consultas, utilice el nombre `adobe_target_experience_events`.

## Objetivos

Al analizar las actividades de los usuarios, puede personalizar el contenido para una audiencia específica y probar distintas versiones del contenido para una entidad individual. Además, analizando una actividad específica durante un período de tiempo determinado o para usuarios individuales, el rendimiento de cada actividad individual puede entenderse con mayor claridad. Los resultados de este análisis combinado se pueden utilizar para comprender el rendimiento de cada actividad individual.

Los siguientes casos de uso de personalización se crean con datos de Adobe Target y se centran en las actividades de los usuarios para crear perspectivas valiosas sobre el comportamiento de los clientes en las aplicaciones empresariales.

Esta guía ilustra los siguientes conceptos clave a través de los ejemplos de casos de uso:

* Para comprender el rendimiento de un ID de actividad de un día determinado, como el recuento, los detalles y los ID de experiencia asociados.
* Para determinar el ámbito del visitante y del evento de una actividad.
* Para recopilar el recuento de visitantes, visitas e información de impresión para el ID de experiencia, el ID de segmento y el ID de actividad.

### Generar recuento de actividad por hora para un día determinado

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### Generar detalles por hora para un particular específico

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### Determine la lista de ID de experiencia para una actividad específica de un día determinado

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Devolver una lista de ámbitos de eventos (visitante, visita, impresión) por instancias por ID de actividad para un día determinado

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Determinar el recuento de visitantes, visitas e impresiones por actividad durante un día determinado

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Determinar los visitantes, las visitas y las impresiones del ID de experiencia, el ID de segmento y el EventScope de un día determinado

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

### Devolver nombres de mbox y recuento de registros para un día determinado

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
