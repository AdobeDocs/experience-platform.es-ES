---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consultas de ejemplo;consulta de ejemplo;adobe target;
solution: Experience Platform
title: Consultas de ejemplo para datos de Adobe Target
topic-legacy: queries
description: Los datos de Adobe Target se transforman en un esquema XDM de Evento de experiencia y se incorporan en Experience Platform como conjuntos de datos para usted. Este documento contiene consultas de ejemplo para usar el servicio de consulta con sus conjuntos de datos de Adobe Target.
exl-id: 0ab3cd6e-25ed-43dc-b8f0-a2b71621ae50
source-git-commit: 76847d8286776a554e55209fa1b334c98b02d76b
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Consultas de ejemplo para datos de Adobe Target

Los datos introducidos desde Adobe Target se transforman en un esquema XDM de Evento de experiencia y se incorporan en Adobe Experience Platform como conjuntos de datos. El servicio de consulta de Adobe Experience Platform facilita muchos casos de uso para estos datos, y las siguientes consultas de ejemplo deberían funcionar con sus conjuntos de datos de Adobe Target.

En Experience Platform, el nombre de un conjunto de datos creado automáticamente es &quot;Adobe Target Experience Events&quot;. Cuando utilice este conjunto de datos con consultas, utilice el nombre `adobe_target_experience_events`.

## Asignación parcial de campos XDM de alto nivel

La siguiente lista muestra los campos de Target que se asignan a los campos XDM correspondientes.

>[!NOTE]
>
> El uso de `[ ]` en el campo XDM denota una matriz.

- mboxName: `_experience.target.mboxname`
- ID de actividad: `_experience.target.activities.activityID`
- ID de la experiencia: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- ID de segmento: `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- Alcance del evento: `_experience.target.activities[].activityEvents[].eventScope`
   - Este campo rastrea nuevos visitantes y visitas.
- ID de paso: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - Este campo es un ID de paso personalizado para Adobe Campaign.
- Precio total: `commerce.order.priceTotal`

## Consultas de ejemplo

Las siguientes consultas muestran ejemplos de consultas comúnmente utilizadas con Adobe Target.

En los ejemplos siguientes, deberá editar el SQL para rellenar los parámetros esperados para sus consultas en función del conjunto de datos, las variables o el intervalo de tiempo que desee evaluar. Proporcione parámetros donde quiera que vea `{ }` en SQL.

### Recuentos de actividad por hora para un día determinado

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

### Detalles por hora para una actividad específica de un día determinado

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

### ID de experiencia para una actividad específica de un día determinado

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
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
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
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### Recuento de visitantes, visitas e impresiones por actividad durante un día determinado

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### Visitantes de retorno, visitas, impresiones para el ID de experiencia, ID de segmento y EventScope de un día determinado

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
