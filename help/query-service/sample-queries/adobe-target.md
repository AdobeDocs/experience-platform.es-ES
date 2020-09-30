---
keywords: Experience Platform;home;popular topics;query service;Query service;sample queries;sample query;adobe target;
solution: Experience Platform
title: Consultas de muestra
topic: queries
description: Los datos de Adobe Target se transforman en esquema XDM de Experience Evento y se ingieren en Experience Platform como conjuntos de datos para usted. Este documento contiene consultas de muestra para usar el servicio de Consulta con sus conjuntos de datos de Adobe Target.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 2%

---


# Consultas de muestra para datos de Adobe Target

Los datos de Adobe Target se transforman en esquema XDM de Experience Evento y se ingieren [!DNL Experience Platform] como conjuntos de datos. Existen muchos casos de uso para [!DNL Query Service] estos datos y las siguientes consultas de muestra deberían funcionar con sus conjuntos de datos de Adobe Target.

>[!NOTE]
>
>En los siguientes ejemplos, deberá editar SQL para completar los parámetros esperados para sus consultas en función del conjunto de datos, las variables o el intervalo de tiempo que desee evaluar. Proporcione parámetros donde quiera que vea `{ }` en SQL.

## Nombre de conjunto de datos estándar para la fuente de datos de Destinatario en [!DNL Platform]:

eventos de experiencias de Adobe Target (nombre descriptivo) <br>`adobe_target_experience_events` (nombre que se debe utilizar en la consulta)

## Asignación parcial de campo XDM de alto nivel

El uso de `[ ]` denota una matriz

| Nombre | Campo XDM | Notas |
| ---- | --------- | ----- |
| mboxName | `_experience.target.mboxname` |  |
| ID de actividad | `_experience.target.activities.activityID` |  |
| ID de la experiencia | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` |  |
| ID del segmento | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` |  |
| Ámbito de evento | `_experience.target.activities[].activityEvents[].eventScope` | Rastrea nuevos Visitantes y visitas |
| ID del paso | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | ID de paso personalizado para Campaña |
| Precio total | `commerce.order.priceTotal` |  |

## Recuentos de actividad por hora para un día determinado

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
  WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

## Detalles por hora de una actividad específica de un día determinado

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
    TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

## ID de experiencia para una actividad específica de un día determinado

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
      TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

## Devolver una lista de ámbitos de Evento (visitante, visita, impresión) por instancias por ID de Actividad para un día determinado

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
      TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

## Recuento de devoluciones de visitantes, visitas e impresiones por actividad para un día determinado

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
    TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

## Visitantes de retorno, visitas, impresiones para ID de experiencia, ID de segmento y EventScope para un día determinado

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
        TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}') AND 
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

## Devolver nombres de mbox y recuento de registros para un día determinado

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
