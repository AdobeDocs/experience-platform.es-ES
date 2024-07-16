---
title: Perspectivas de destinos
description: Descubra el SQL que alimenta las perspectivas de sus destinos y utilice estas consultas para generar perspectivas personalizadas y explorar aún más la activación de datos de Adobe Experience Platform.
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: d4baf6cfaa772e5d46cef470fb35818c7af868b1
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 3%

---

# Perspectivas de destinos

Las perspectivas derivadas del análisis del modelo de datos hacen que los datos de Adobe Real-time Customer Data Platform sean más accesibles, comprensibles e impactantes para la toma de decisiones.

Comprenda sus perspectivas de destino accediendo al SQL que las alimenta y, a continuación, genere sus propias perspectivas para explorar aún más la activación de datos de Adobe Experience Platform a sus plataformas de destino. Transforme los datos sin procesar en nuevas perspectivas procesables mediante el uso del modelo de datos SQL de Real-Time CDP existente como inspiración para crear consultas para sus necesidades comerciales únicas.

Consulte la [Documentación de vista de SQL](../view-sql.md) para obtener más información sobre cómo adaptar el SQL de sus perspectivas directamente a través de la IU de PLatform.

Las siguientes perspectivas están disponibles para que las uses como parte del [panel de destinos](../guides/destinations.md) o un [panel personalizado definido por el usuario](../user-defined-dashboards.md). Consulte la [descripción general de la personalización](../customize/overview.md) para obtener instrucciones sobre cómo personalizar el tablero o [crear y editar nuevos widgets](../customize/custom-widgets.md) en la biblioteca de widgets y [tablero definido por el usuario](../user-defined-dashboards.md#create-widget).

## Públicos activados {#activated-audiences}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el recuento total de audiencias activadas filtradas por un destino particular?
- ¿Cuál es el recuento de audiencias activadas por cada destino?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

Consulte la [documentación del widget de audiencias activadas](../guides/destinations.md#activated-audiences) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Públicos activados en todos los destinos {#activated-audiences-across-all-destinations}

Preguntas respondidas por esta perspectiva:

- ¿Cuántas audiencias se activan en todos los destinos?
- ¿Cuál es el recuento total de audiencias activadas?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

Consulte la [documentación del widget de audiencias activadas en todos los destinos](../guides/destinations.md#activated-audiences-across-all-destinations) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Destinos activos por plataforma de destino {#active-destinations-by-destination-platform}

Preguntas respondidas por esta perspectiva:

- ¿Cuántos destinos hay activos?
- ¿Cuál es el desglose de los destinos activos por plataforma de destino?
- ¿Cuál es el recuento de destinos activos desglosados por cada plataforma de destino?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

Consulte la [documentación del widget de destinos activos por plataforma de destino](../guides/destinations.md#active-destinations-by-destination-platform) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Tendencia de tamaño de audiencia {#audience-size-trend}

Preguntas respondidas por esta perspectiva:

- ¿Cómo ha cambiado el tamaño de la audiencia con el paso del tiempo, incluidas las anomalías de una audiencia asignada a un destino?
- ¿Cómo encuentro la tendencia general en el tamaño de la audiencia, por destino, durante los periodos especificados de 30 días, 90 días y 12 meses?
- ¿Cuáles son las características clave de la audiencia que contribuyen al tamaño, por ejemplo, los picos en relación con cualquier campaña de marketing por correo electrónico?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

Consulte la [documentación del widget de tendencia de tamaño de audiencia](../guides/destinations.md#audience-size-trend) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Públicos comunes {#common-audiences}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son las audiencias comunes entre dos destinos diferentes?
- ¿Cuántos perfiles tiene cada una de las audiencias comunes entre dos destinos diferentes?
- ¿Cuál es la audiencia más grande a la que se asignan dos destinos?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

Consulte la [documentación del widget de audiencias comunes](../guides/destinations.md#common-audiences) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Estado del destino {#destination-status}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el número total de destinos habilitados para su uso?
- ¿Cuál es el número total de destinos desactivados?
- ¿Cuál es el porcentaje de división entre destinos habilitados y deshabilitados?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Consulte la [documentación del widget de estado de destino](../guides/destinations.md#destination-status) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Recuento de destinos {#destinations-count}

Preguntas respondidas por esta perspectiva:

- ¿Cuántos destinos hay configurados actualmente?
- ¿Cómo ha cambiado el recuento total de destinos a lo largo del tiempo?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Consulte la [documentación del widget de recuento de destinos](../guides/destinations.md#destinations-count) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Estado de público asignado {#mapped-audience-health}

Preguntas respondidas por esta perspectiva:

- ¿Qué audiencias asignadas a un destino tienen variaciones significativas en los últimos 30 días?
- ¿Cuál es el tamaño más reciente de una audiencia asignada y si ha cambiado en el último mes?
- ¿Cómo hago una lista de todas las audiencias asignadas a un destino según la gravedad de los cambios de tamaño que tuvieron en el último mes?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

Consulte la [documentación del widget de estado de audiencia asignada](../guides/destinations.md#mapped-audience-health) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Públicos asignados {#mapped-audiences}

Preguntas respondidas por esta perspectiva:

- ¿Cuántas audiencias se asignan a un destino determinado?
- ¿Cómo ha cambiado el recuento de audiencias asignadas con el paso del tiempo?
- ¿Dónde puedo comparar dos destinos para ver la superposición de audiencias asignada a cada destino?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Consulte la [documentación del widget de audiencias asignadas](../guides/destinations.md#mapped-audiences) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## Destinos más utilizados {#most-used-destinations}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son los destinos más utilizados?
- ¿Cuántas audiencias se asignan a cada destino, ordenadas de la mayor a la menor?
- ¿Cómo cambia la asignación de audiencias a destinos de una instantánea a otra?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

Consulte la [documentación del widget de destinos más usados](../guides/destinations.md#most-used-destinations) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Públicos activados recientemente {#recently-activated-audiences}

Preguntas respondidas por esta perspectiva:

- ¿A qué destino se activó más recientemente una audiencia?
- ¿Cómo encuentro una lista de todos los destinos ordenados por la última fecha de actualización?
- ¿Cómo puedo comparar dos destinos en función de las activaciones más recientes?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

Consulte la [Documentación del widget de audiencias activadas recientemente](../guides/destinations.md#recently-activated-audiences) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Públicos activados recientemente por destino {#recently-activated-audiences-by-destination}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son las audiencias activadas en un destino particular?
- ¿Cómo encuentro una lista de audiencias activadas por una audiencia en particular desde la más reciente hasta la menos reciente?
- ¿Cómo encuentro una lista de audiencias en la fecha en que se activó para un destino específico?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

Consulte la [documentación de audiencias activadas recientemente por el widget de destino](../guides/destinations.md#recently-activated-audiences-by-destination) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Destinos creados recientemente {#recently-created-destinations}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son los destinos creados más recientemente?
- ¿Cómo encuentro una lista de destinos con la fecha de creación?
- ¿Qué nuevo destino se ha creado recientemente?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

Consulte la [Documentación del widget de destinos creados recientemente](../guides/destinations.md#recently-created-destinations) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## Pasos siguientes {#next-steps}

Al leer este documento, ahora comprende el SQL que genera perspectivas del panel y qué preguntas comunes resuelve este análisis. Ahora puede editar e iterar estas consultas SQL para generar sus propias perspectivas.

Consulte la [Documentación de vista de SQL](../view-sql.md) para obtener más información sobre cómo adaptar el SQL de sus perspectivas directamente a través de la IU de PLatform.

También puede leer y comprender el SQL que genera perspectivas para los paneles de [Perfiles](./profiles.md), [Perfiles de cuenta](./account-profiles.md) y [Audiencias](./audiences.md).
