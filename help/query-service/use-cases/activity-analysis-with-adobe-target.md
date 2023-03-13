---
title: Análisis De Actividades Con Adobe Target
description: En este documento se explica cómo utilizar el servicio de consultas para crear perspectivas procesables a partir de conjuntos de datos creados con los datos de Adobe Target.
exl-id: a5181ee2-1e1c-405d-8dfe-5a32c28ac9f1
source-git-commit: d573c01a0aa9989f581796a0be4aec6904ffc569
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Análisis de actividades con Adobe Target

Adobe Experience Platform le permite introducir datos de Adobe Target mediante los campos del Modelo de datos de experiencia (XDM) para crear conjuntos de datos y utilizarlos con el Servicio de consultas. Dado que Adobe Target está diseñado para personalizar el contenido y las experiencias del usuario, las consultas ejecutadas en estos conjuntos de datos permiten perspectivas altamente personalizadas y enfocadas al analizar la actividad del usuario a través de SQL.

Este documento proporciona una variedad de consultas SQL de ejemplo que muestran casos de uso comunes basados en los comportamientos y características de los clientes.

## Primeros pasos

Para cada uno de los siguientes casos de uso, se proporciona un ejemplo de consulta SQL parametrizado como plantilla para que la personalice. Proporcione parámetros dondequiera que vea `{ }` en los ejemplos SQL que le interese evaluar.

## Asignación de campo XDM parcial de alto nivel

En la siguiente tabla se enumeran los campos de Target comunes y los campos XDM correspondientes a los que se asignan.

>[!NOTE]
>
>El uso de `[ ]` dentro del campo XDM indica una matriz.

| Nombre del campo de destino | Nombre de campo XDM | Notas |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | N/A |
| ID de actividad | `_experience.target.activities.activityID` | N/A |
| ID de la experiencia | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | N/A |
| ID del segmento | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | N/A |
| Ámbito del evento | `_experience.target.activities[].activityEvents[].eventScope` | Este campo realiza el seguimiento de nuevos visitantes y visitas. |
| ID de paso | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Este campo es un ID de paso personalizado para Adobe Campaign. |
| Precio total | commerce.order.priceTotal | N/A |

>[!IMPORTANT]
>
>El nombre de un conjunto de datos creado automáticamente con datos de Target es &quot;Eventos de experiencia de Adobe Target&quot;. Cuando utilice este conjunto de datos con consultas, utilice el nombre `adobe_target_experience_events`.

## Objetivos

Al analizar las actividades del usuario, se puede personalizar el contenido para una audiencia específica y probar distintas versiones del contenido para una entidad individual. Además, al analizar una actividad específica durante un periodo determinado o para usuarios individuales, el rendimiento de cada actividad individual puede entenderse con mayor claridad. Los resultados de este análisis combinado pueden utilizarse para comprender el rendimiento de cada actividad individual.

Los siguientes casos de uso de personalización se crean con datos de Adobe Target y se centran en actividades del usuario para crear perspectivas valiosas sobre el comportamiento de los clientes en las aplicaciones comerciales.

Esta guía ilustra los siguientes conceptos clave a través de los ejemplos de casos de uso:

* Para comprender el rendimiento de un ID de actividad durante un día determinado, como el recuento, los detalles y los ID de experiencia asociados.
* Para determinar el alcance de visitante y evento de una actividad.
* Para recopilar el recuento de visitantes, visitas e información de impresiones para el Experience ID, el ID del segmento y el ID de actividad.

### Generar un recuento de actividades por hora para un día determinado

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

### Generar detalles por hora para un determinado

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

### Determine la lista de ID de experiencia para una actividad específica para un día determinado

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

### Devolver una lista de ámbitos del evento (visitante, visita e impresión) por instancias y por ID de actividad para un día determinado

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

### Determine el recuento de visitantes, visitas e impresiones por actividad para un día determinado

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

### Determine los visitantes, las visitas y las impresiones para el Experience ID, el Segment ID y el EventScope de un día determinado

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
