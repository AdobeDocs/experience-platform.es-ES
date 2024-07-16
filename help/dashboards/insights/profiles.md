---
title: Perspectivas de perfil
description: Descubra el SQL que alimenta las perspectivas de perfil y utilice estas consultas para generar perspectivas personalizadas que exploren aún más a sus clientes y sus experiencias como consumidores.
exl-id: f3792076-3e01-4e26-8788-32927202a2e5
source-git-commit: 34eb9151cc6bb8551553b0a8427e58871acb4dbb
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 3%

---

# Perspectivas de perfil

Las perspectivas derivadas del análisis del modelo de datos hacen que los datos de Adobe Real-time Customer Data Platform sean más accesibles, comprensibles e impactantes para la toma de decisiones.

Comprenda sus perspectivas de perfil accediendo al SQL que las alimenta y, a continuación, genere sus propias perspectivas para explorar aún más a sus clientes y a sus experiencias de consumidor que conforman sus perfiles. Transforme los datos sin procesar en nuevas perspectivas procesables mediante el uso del modelo de datos SQL de Real-Time CDP existente como inspiración para crear consultas para sus necesidades comerciales únicas.

Consulte la [Documentación de vista de SQL](../view-sql.md) para obtener más información sobre cómo adaptar el SQL de sus perspectivas directamente a través de la interfaz de usuario de Platform.

Las siguientes perspectivas están disponibles para que las use como parte del [panel de perfiles](../guides/profiles.md) o un [panel personalizado definido por el usuario](../user-defined-dashboards.md). Consulte la [descripción general de la personalización](../customize/overview.md) para obtener instrucciones sobre cómo personalizar el tablero o [crear y editar nuevos widgets](../customize/custom-widgets.md) en la biblioteca de widgets y [tablero definido por el usuario](../user-defined-dashboards.md#create-widget).

## Superposición de público por política de combinación {#audience-overlap-by-merge-policy}

Preguntas respondidas por esta perspectiva:

- ¿Qué perfiles son comunes a ambas audiencias?
- ¿Cómo afecta la superposición a las tasas de participación o conversión?
- ¿Cómo se pueden adaptar las estrategias de marketing al segmento superpuesto?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1333234510
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1559754729)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1559754729
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1333234510))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1333234510
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1559754729 ) a;
```

+++

Consulte la [documentación del widget de política de combinación que se superpone con la audiencia](../guides/profiles.md#audience-overlap-by-merge-policy) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Informe de superposición de público {#audience-overlap-report}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son las 50 audiencias más superpuestas?
- ¿Cuáles son las 50 audiencias menos superpuestas?
- ¿Cómo cambia el patrón superpuesto según la política de combinación?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT source_segment_name,
        source_segment_id,
        overlap_segment_name,
        overlap_segment_id,
        max(source_segment_audience_count) source_segment_audience_count,
        max(overlap_segment_audience_count) overlap_segment_audience_count,
        max(overlap_audience_count) overlap_audience_count,
        CASE
            WHEN (max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) > 0 THEN (cast(max(overlap_audience_count) AS DECIMAL(18, 2)) / cast((max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) AS DECIMAL(18, 2))) * 100::DECIMAL(9, 2)
            ELSE 100.00
        END overlapping_percentage
  FROM
    (SELECT adwh_fact_profile_overlap_of_segments.Segment1 source_segment_id,
            adwh_fact_profile_overlap_of_segments.Segment2 overlap_segment_id,
            Sum(count_of_overlap) overlap_audience_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment2 ,
              qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment1) a
  INNER JOIN
    (SELECT sum(count_of_profiles) source_segment_audience_count,
            adwh_dim_segments.segment_name source_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment1
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_dim_segments.segment_id = qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) b ON a.source_segment_id = b.segment1
  INNER JOIN
    (SELECT sum(count_of_profiles) overlap_segment_audience_count,
            adwh_dim_segments.segment_name overlap_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment2
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_dim_segments.segment_id = adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) c ON a.overlap_segment_id = c.segment2
  GROUP BY source_segment_name,
          source_segment_id,
          overlap_segment_name,
          overlap_segment_id
  ORDER BY overlapping_percentage DESC
  LIMIT 5;
```

+++

Consulte la [documentación del widget de informe de superposición de audiencias](../guides/profiles.md#audience-overlap-report) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Audiencias (recuento) {#audiences}

Preguntas respondidas por esta perspectiva:

- ¿Qué política de combinación se utiliza predominantemente para la segmentación?
- ¿Cuál es la distribución de audiencias entre políticas de combinación?
- ¿Hay algún cambio significativo en los números de audiencia para las políticas de combinación específicas a lo largo del tiempo?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT count(DISTINCT a.segment_id) count_of_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) b ON a.merge_policy_id= b.merge_policy_id
  AND a.date_key = b.last_process_date
  WHERE a.merge_policy_id= 2027892989;
```

+++

Consulte la [documentación del widget de audiencias](../guides/profiles.md#audiences) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Público asignado al estado de destino {#audiences-mapped-to-destination-status}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la distribución general de audiencias entre destinos asignados y no asignados?
- ¿Qué destinos específicos tienen el número más alto de audiencias asignadas?
- ¿Qué proporción del total de audiencias permanece sin asignar?
- De estas audiencias sin asignar, ¿hay patrones o tendencias asociadas?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT COUNT(DISTINCT (y.segment_id)) AS count_mapped_segments,
        COUNT(DISTINCT (x.segment_id)) - COUNT(DISTINCT (y.segment_id)) AS count_unmapped_segments,
        COUNT(DISTINCT (x.segment_id)) AS total_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  LEFT JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations y ON x.segment_id = y.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) z ON x.merge_policy_id = z.merge_policy_id
  AND x.date_key = z.last_process_date
  WHERE x.merge_policy_id = 2027892989;
```

+++

Consulte la [documentación de audiencias asignadas al widget de estado de destino](../guides/profiles.md#audiences-mapped-to-destination-status) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Tamaño de público {#audiences-size}

Preguntas respondidas por esta perspectiva:

- ¿Qué segmento de audiencia tiene el tamaño más grande?
- ¿Cuáles son las cinco audiencias más grandes?
- ¿Cómo cambia la distribución del tamaño de la audiencia con el paso del tiempo para la audiencia principal?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
        qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
        qsaccel.profile_agg.adwh_dim_segments.segment,
        qsaccel.profile_agg.adwh_dim_segments.segment_name,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles)count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id= 2027892989
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
          qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
          qsaccel.profile_agg.adwh_dim_segments.segment,
          qsaccel.profile_agg.adwh_dim_segments.segment_name
  ORDER BY count_of_profiles DESC
  LIMIT 20;
```

+++

Consulte la [documentación del widget de tamaño de audiencias](../guides/profiles.md#audiences-size) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Distribución de puntuaciones de inteligencia artificial aplicada al cliente {#customer-ai-distribution-of-scores}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la distribución de puntuaciones entre bloques para cada uno de mis modelos de inteligencia artificial aplicada al cliente?
- ¿Cuál es la distribución de las puntuaciones por puntuación alta, media y baja?
- ¿Cuál es el desglose de la distribución de puntuación por política de combinación?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT b.model_name,
     b.model_type,
     CASE
         WHEN score >= 0
              AND score < 25 THEN 'LOW'
         WHEN score >= 25
              AND score < 75 THEN 'MEDIUM'
         WHEN score >= 75
              AND score <= 100 THEN 'HIGH'
     END bucket_name,
     CASE
         WHEN score >= 0
              AND score < 5 THEN '02.50'
         WHEN score >= 5
              AND score < 10 THEN '07.50'
         WHEN score >= 10
              AND score < 15 THEN '12.50'
         WHEN score >= 15
              AND score < 20 THEN '17.50'
         WHEN score >= 20
              AND score < 25 THEN '22.50'
         WHEN score >= 25
              AND score < 30 THEN '27.50'
         WHEN score >= 30
              AND score < 35 THEN '32.50'
         WHEN score >= 35
              AND score < 40 THEN '37.50'
         WHEN score >= 40
              AND score < 45 THEN '42.50'
         WHEN score >= 45
              AND score < 50 THEN '47.50'
         WHEN score >= 50
              AND score < 55 THEN '52.50'
         WHEN score >= 55
              AND score < 60 THEN '57.50'
         WHEN score >= 60
              AND score < 65 THEN '62.50'
         WHEN score >= 65
              AND score < 70 THEN '67.50'
         WHEN score >= 70
              AND score < 75 THEN '72.50'
         WHEN score >= 75
              AND score < 80 THEN '77.50'
         WHEN score >= 80
              AND score < 85 THEN '82.50'
         WHEN score >= 85
              AND score < 90 THEN '87.50'
         WHEN score >= 90
              AND score < 95 THEN '92.50'
         WHEN score >= 95
              AND score <= 100 THEN '97.50'
     END score_bins,
     Sum(CASE
             WHEN score >= 0
                  AND score < 25 THEN count_of_profiles
             WHEN score >= 25
                  AND score < 75 THEN count_of_profiles
             WHEN score >= 75
                  AND score <= 100 THEN count_of_profiles
         END) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
  AND a.model_id = b.model_id
  WHERE a.merge_policy_id = 2027892989
    AND a.model_id = 1829081696
    AND score_date =
      (SELECT Max(score_date)
       FROM qsaccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
          model_type,
          CASE
              WHEN score >= 0
                   AND score < 25 THEN 'LOW'
              WHEN score >= 25
                   AND score < 75 THEN 'MEDIUM'
              WHEN score >= 75
                   AND score <= 100 THEN 'HIGH'
          END,
          CASE
              WHEN score >= 0
                   AND score < 5 THEN '02.50'
              WHEN score >= 5
                   AND score < 10 THEN '07.50'
              WHEN score >= 10
                   AND score < 15 THEN '12.50'
              WHEN score >= 15
                   AND score < 20 THEN '17.50'
              WHEN score >= 20
                   AND score < 25 THEN '22.50'
              WHEN score >= 25
                   AND score < 30 THEN '27.50'
              WHEN score >= 30
                   AND score < 35 THEN '32.50'
              WHEN score >= 35
                   AND score < 40 THEN '37.50'
              WHEN score >= 40
                   AND score < 45 THEN '42.50'
              WHEN score >= 45
                   AND score < 50 THEN '47.50'
              WHEN score >= 50
                   AND score < 55 THEN '52.50'
              WHEN score >= 55
                   AND score < 60 THEN '57.50'
              WHEN score >= 60
                   AND score < 65 THEN '62.50'
              WHEN score >= 65
                   AND score < 70 THEN '67.50'
              WHEN score >= 70
                   AND score < 75 THEN '72.50'
              WHEN score >= 75
                   AND score < 80 THEN '77.50'
              WHEN score >= 80
                   AND score < 85 THEN '82.50'
              WHEN score >= 85
                   AND score < 90 THEN '87.50'
              WHEN score >= 90
                   AND score < 95 THEN '92.50'
              WHEN score >= 95
                   AND score <= 100 THEN '97.50'
          END;
```

+++

Consulte la [documentación del widget de distribución de puntuaciones de inteligencia artificial aplicada al cliente](../guides/profiles.md#customer-ai-distribution-of-scores) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Resumen de puntuaciones de la inteligencia artificial aplicada al cliente {#customer-ai-scoring-summary}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el resumen de puntuación para cada uno de mis modelos de inteligencia artificial aplicada al cliente?
- ¿Cómo cambian mis puntuaciones de tendencia de inteligencia artificial aplicada al cliente para diferentes audiencias?
- ¿Cómo cambia mi resumen de puntuación en comparación con otros KPI en la descripción general de los perfiles?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT model_name,
         model_type,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  WHERE a.merge_policy_id=2027892989
    AND a.model_id =1829081696
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Consulte la [documentación del widget de resumen de puntuación de inteligencia artificial aplicada al cliente](../guides/profiles.md#customer-ai-scoring-summary) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Superposición de identidad {#identity-overlap}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la intersección común entre [!UICONTROL Tipo de identidad A] y [!UICONTROL Tipo de identidad B]?
- ¿Cómo puedo refinar las audiencias de los clientes en función de la superposición de tipos de identidad específicos para mejorar las estrategias de marketing dirigidas?
- ¿Qué perspectivas se pueden obtener de la evaluación del rendimiento de la campaña dentro de las áreas de intersección?
- Con esta perspectiva del rendimiento de la campaña, ¿cómo se pueden optimizar los esfuerzos de marketing futuros?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

Consulte la [documentación del widget de superposición de identidad](../guides/profiles.md#identity-overlap) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Recuento de perfiles {#profile-count}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el recuento general de perfiles en Adobe Real-time Customer Data Platform?
- ¿Cómo se distribuyen los perfiles en función de las políticas de combinación?
- ¿Qué política de combinación tiene el recuento de perfiles más alto?

El SQL que genera estas perspectivas es el siguiente:

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

Encontrará información completa sobre el aspecto y la funcionalidad de esta perspectiva en la [guía del widget de recuento de perfiles](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count).

Consulte la [documentación del widget de recuento de perfiles](../guides/profiles.md#profile-count) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Cambio de recuento de perfiles {#profile-count-change}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la tendencia de los cambios generales de recuento de perfiles?
- ¿Qué causó picos o caídas significativos en el recuento de perfiles?
- ¿Existen políticas de combinación específicas que impulsan el cambio en el recuento de perfiles?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT (sum(count_of_profiles) - sum(count_of_profiles_days_ago)) profiles_added
  FROM
    (SELECT sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) count_of_profiles,
            0 count_of_profiles_days_ago
    FROM qsaccel.profile_agg.adwh_fact_profile
    WHERE qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile.date_key = '2024-01-10'
    UNION ALL SELECT 0 count_of_profiles,
                      CASE
                          WHEN sum(cntondatediff) =0 THEN sum(cntmin)
                          ELSE sum(cntondatediff)
                      END AS count_of_profiles_days_ago
    FROM
      (SELECT coalesce(sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles), 0) cntondatediff,
              0 cntmin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =dateadd(DAY, - 30, '2024-01-10')
        UNION ALL SELECT 0 cntondatediff,
                        sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) countMin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =
            (SELECT min(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) col
            FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
            WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >= dateadd(DAY, - 30, '2024-01-10')
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles IS NOT NULL) )b) a;
```

+++

Consulte la [documentación del widget de cambio de recuento de perfiles](../guides/profiles.md#profile-count-change) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Tendencia de cambio de recuento de perfiles {#profile-count-change-trend}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la tendencia general del cambio en el recuento de perfiles en los últimos 12 meses en función de la política de combinación?
- ¿Hay patrones específicos o fluctuaciones en el cambio del recuento de perfiles en los últimos 30 días que requieren atención?
- ¿En qué se diferencia el recuento de perfiles de los últimos 90 días de la tendencia general?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Consulte la [documentación del widget de tendencia de cambio de recuento de perfiles](../guides/profiles.md#profile-count-change-trend) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Tendencia de recuento de perfiles {#profile-count-trend}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la tendencia general en el recuento de perfiles en función de la política de combinación durante los últimos 30 días?
- En base a esta tendencia, ¿cómo se compara con las tendencias a largo plazo (por ejemplo, 90 días y 12 meses)?
- ¿Qué política de combinación contribuye más al aumento o la disminución del recuento de perfiles en los periodos de tiempo especificados (30 días, 90 días y 12 meses)?
- ¿Hay algún pico o caída específicos en el recuento de perfiles que se correlacionan con determinados eventos o periodos dentro del periodo de tiempo de 30 días?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT date_key,
       sum(count_of_profiles) AS count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -365, y.last_process_date)
    AND x.merge_policy_id = 2027892989
  GROUP BY date_key;
```

+++

Consulte la [documentación del widget de tendencia de recuento de perfiles](../guides/profiles.md#profile-count-trend) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Perfiles por identidad {#profiles-by-identity}

Preguntas respondidas por esta perspectiva:

- Entre el recuento total de perfiles, ¿qué tipo de identidad tiene una proporción más alta?
- ¿Existen diferencias significativas entre los tipos de identidad?
- ¿Cuál es la distribución general de los tipos de identidad?
- ¿Existen disparidades o anomalías significativas en los recuentos de identidad?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Consulte la [documentación del widget Perfiles por identidad](../guides/profiles.md#profiles-by-identity) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Tendencia de cambio de recuento de perfiles {#profiles-count-change-trend}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la tendencia general en el cambio del recuento de perfiles en los últimos 12 meses, según la política de combinación?
- ¿Hay patrones específicos o fluctuaciones en el cambio del recuento de perfiles en los últimos 30 días que requieren atención?
- ¿En qué se diferencia el cambio en el recuento de perfiles durante los últimos 90 días de la tendencia general?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Consulte la [documentación del widget de tendencia de cambio de recuento de perfiles](../guides/profiles.md#profiles-count-change-trend) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Tendencia de cambio de recuento de perfiles por identidad {#profiles-count-change-trend-by-identity}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la tendencia general en el cambio del recuento de perfiles en diferentes identidades durante los últimos 12 meses?
- ¿Existen tendencias de identidad específicas que muestren cambios significativos en los últimos 30 días?
- ¿En qué se diferencian los cambios en el recuento de perfiles al comparar las tendencias de 30 días, 90 días y 12 meses para una identidad particular?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT date_key,
        namespace_description,
        profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            namespace_description,
            (count_of_profiles - lag(count_of_profiles, 1, 0) over(PARTITION BY namespace_description
                                                                  ORDER BY date_key)) profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
              qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (PARTITION BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
                                  ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
        LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
        AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id= -1042977439
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key >= dateadd(DAY, - 30 -1, '2024-01-10')
        GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
                adwh_dim_namespaces.namespace_description)a)b
  WHERE rn_num > 1;
```

+++

Consulte la [Tendencia de cambio de recuento de perfiles por documentación del widget de identidad](../guides/profiles.md#profiles-count-change-trend-by-identity) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Perfiles de identidad únicos {#single-identity-profiles}

Preguntas respondidas por esta perspectiva:

- ¿Mis datos de identidad de clientes se representan de forma coherente con identidades únicas?
- ¿Qué porcentaje de mi base de usuarios consta de perfiles con un solo tipo de identidad?
- De los perfiles con un solo tipo de identidad, ¿cómo afecta esto a la integridad del perfil?
- ¿Existe una correlación entre el tipo de identidad más común y el recuento de perfiles de identidad único?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Consulte la [documentación del widget de perfiles de identidad única](../guides/profiles.md#single-identity-profiles) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Perfiles de identidad únicos por identidad {#single-identity-profiles-by-identity}

Preguntas respondidas por esta perspectiva:

- ¿Cuántos clientes únicos se han registrado con una sola identidad (por ejemplo, correo electrónico o número de teléfono)?
- ¿Cuál es la distribución de perfiles de identidad única entre diferentes tipos de identidad, como correo electrónico o números de teléfono?
- ¿Hay patrones de identidad emergentes o cambios dentro de los perfiles de identidad únicos?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
```

+++

Consulte la [documentación del widget de identidad ](../guides/profiles.md#single-identity-profiles-by-identity) con perfiles de identidad únicos para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Perfiles no segmentados {#unsegmented-profiles}

Preguntas respondidas por esta perspectiva:

- ¿Cuántos perfiles no forman parte de una audiencia?
- ¿Qué porcentaje de la audiencia total está representado por perfiles no segmentados?
- ¿Contribuye alguna política de combinación a un gran número de perfiles no segmentados?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Orphan_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Consulte la [documentación del widget de perfiles no segmentados](../guides/profiles.md#unsegmented-profiles) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Pasos siguientes

Al leer este documento, ahora comprende el SQL que genera perspectivas del panel y qué preguntas comunes resuelve este análisis. Ahora puede editar e iterar en SQL para generar sus propias perspectivas.

Consulte la [Documentación de vista de SQL](../view-sql.md) para obtener más información sobre cómo adaptar el SQL de sus perspectivas directamente a través de la IU de PLatform.

También puede leer y comprender el SQL que genera perspectivas para los paneles de [Audiencias](./audiences.md), [Perfiles de cuenta](./account-profiles.md) y [Destinos](./destinations.md).
