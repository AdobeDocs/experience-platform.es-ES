---
title: Audiences Insights
description: Descubra el SQL que alimenta las perspectivas de audiencia y utilice estas consultas para generar perspectivas personalizadas y explorar aún más los datos de audiencia de Adobe Experience Platform.
exl-id: 99624234-c4e1-44bb-9567-505bc0c4723e
source-git-commit: 34eb9151cc6bb8551553b0a8427e58871acb4dbb
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 3%

---

# Perspectivas de audiencias

Las perspectivas derivadas del análisis del modelo de datos hacen que los datos de Adobe Real-time Customer Data Platform sean más accesibles, comprensibles e impactantes para la toma de decisiones.

Comprenda sus perspectivas de audiencia accediendo al SQL que las alimenta y, a continuación, genere sus propias perspectivas para explorar aún más las identidades y perfiles que conforman sus audiencias. Transforme los datos sin procesar en nuevas perspectivas procesables mediante el uso del modelo de datos SQL de Real-Time CDP existente como inspiración para crear consultas para sus necesidades comerciales únicas.

Consulte la [Documentación de vista de SQL](../view-sql.md) para obtener más información sobre cómo adaptar el SQL de sus perspectivas directamente a través de la IU de PLatform.

Las siguientes perspectivas están disponibles para que las use como parte del [tablero de audiencias](../guides/audiences.md) o un [tablero personalizado definido por el usuario](../user-defined-dashboards.md). Consulte la [descripción general de la personalización](../customize/overview.md) para obtener instrucciones sobre cómo personalizar el tablero o [crear y editar nuevos widgets](../customize/custom-widgets.md) en la biblioteca de widgets y [tablero definido por el usuario](../user-defined-dashboards.md#create-widget).

Las siguientes perspectivas están disponibles para que las use como parte del [tablero de audiencias](../guides/audiences.md) o un tablero personalizado.

## Informe de superposición de público {#audience-overlap-report}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son las 50 audiencias superpuestas más comunes de una audiencia filtrada concreta?
- ¿Cuáles son las 50 audiencias menos superpuestas de una audiencia filtrada concreta?
- ¿Cómo cambia el patrón superpuesto para una audiencia filtrada diferente?

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

Consulte la [documentación del widget de informe de superposición de audiencias](../guides/audiences.md#audience-overlap-report) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Superposición de público {#audience-overlap}

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
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1870062812
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=2080256533)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=2080256533
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1870062812))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1870062812
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 2080256533 ) a;
```

+++

Consulte la [documentación del widget de superposición de audiencias](../guides/audiences.md#audience-overlap) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Tend. cambio tmñ público {#audience-size-change-trend}

Preguntas respondidas por esta perspectiva:

- ¿Ha habido picos o caídas significativos en el tamaño de la audiencia en los últimos 30 días, 90 días o 12 meses?
- ¿Cómo cambia el tamaño de la audiencia durante días específicos?
- ¿Se han detectado anomalías o patrones repetidos de picos o caídas en los últimos 12 meses?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT date_key,
      Profiles_added
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                                ORDER BY date_key))Profiles_added
    FROM
      (SELECT date_key,
              sum(x.count_of_profiles)count_of_profiles,
              row_number() OVER (
                                  ORDER BY date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
        INNER JOIN
          (SELECT MAX(process_date) last_process_date,
                  merge_policy_id
          FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
          WHERE process_name = 'FACT_TABLES_PROCESSING'
            AND process_status = 'SUCCESSFUL'
          GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
        WHERE segment_id = 1333234510
          AND x.date_key >= dateadd(DAY, -30 -1, y.last_process_date)
        GROUP BY x.date_key) a)b
  WHERE rn_num > 1;
```

+++

Consulte la [documentación del widget de tendencia de cambio de tamaño de audiencia](../guides/audiences.md#audience-size-change-trend) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Tendencia del tamaño del público por identidad {#audience-size-trend-by-identity}

Preguntas respondidas por esta perspectiva:

- ¿Mi audiencia crece, se estabiliza o experimenta fluctuaciones de forma constante?
- ¿Hay alguna identidad específica que tenga picos o caídas en el crecimiento de la audiencia con el paso del tiempo?
- ¿Hay alguna anomalía en el crecimiento de mi identidad a lo largo del tiempo?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT sum(count_of_profiles) AS identities,
        date_key
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_namespaces z ON x.namespace_id = z.namespace_id
  AND x.merge_policy_id = z.merge_policy_id
  WHERE x.date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
    AND z.namespace_description = 'crmid'
  GROUP BY date_key;
```

+++

Consulte la [tendencia de tamaño de audiencia según la documentación del widget de identidad](../guides/audiences.md#audience-size-trend-by-identity) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Tendencia de tamaño de audiencia {#audience-size-trend}

Preguntas respondidas por esta perspectiva:

- ¿Cómo ha cambiado el tamaño de la audiencia con el paso del tiempo, incluidas las anomalías?
- ¿Cómo puedo encontrar la tendencia general en el tamaño de la audiencia en los períodos de: 30 días, 90 días y 12 meses?
- ¿Cuáles son las características clave de la audiencia que contribuyen a su tamaño? Por ejemplo, los picos debidos a campañas de marketing por correo electrónico.

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT date_key,
        sum(count_of_profiles) AS audience_size
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
  GROUP BY date_key,
          segment_id;
```

+++

Consulte la [documentación del widget de tendencia de tamaño de audiencia](../guides/audiences.md#audience-size-trend) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Tamaño de público {#audience-size}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el tamaño total actual de la audiencia?
- ¿En qué se diferencia el tamaño de audiencia actual de períodos anteriores o de audiencias específicas?
- ¿Cuál es el impacto de las campañas de marketing recientes en el tamaño de la audiencia?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT
  sum(
    qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles
  ) count_of_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
WHERE
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = -1323307941
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1914917902
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-12';
```

+++

Consulte la [documentación del widget de tamaño de audiencia](../guides/audiences.md#audience-size) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Distribución de puntuaciones de inteligencia artificial aplicada al cliente {#customer-ai-distribution-of-scores}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la distribución de puntuación para cada bloque de mi modelo de inteligencia artificial aplicada al cliente, filtrado por una audiencia seleccionada?
- ¿Cuál es la distribución de puntuación de alta, media y baja para una audiencia concreta?
- ¿Cuál es el desglose de la distribución de puntuación por distintas audiencias de interés?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT b.model_name,
      b.model_type,
      c.segment_name,
      c.segment_id,
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
   FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
          JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
     AND a.model_id = b.model_id
          JOIN qsaccel.profile_agg.adwh_dim_segments c ON a.segment_id = c.segment_id
   WHERE a.merge_policy_id = 1133248113
     AND a.model_id = 1829081696
     AND a.segment_id = 1870062812
     AND score_date =
         (SELECT MAX(score_date)
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
          WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
             b.model_type,
             c.segment_name,
             c.segment_id,
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

Consulte la [documentación del widget de distribución de puntuaciones de inteligencia artificial aplicada al cliente](../guides/audiences.md#customer-ai-distribution-of-scores) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Resumen de puntuaciones de la inteligencia artificial aplicada al cliente {#customer-ai-scoring-summary}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el resumen de puntuación de cada uno de mis modelos de inteligencia artificial aplicada al cliente para una audiencia concreta?
- ¿Cómo cambian mis puntuaciones de tendencia de inteligencia artificial aplicada al cliente para diferentes audiencias?
- ¿En qué se diferencia mi resumen de puntuación de los demás KPI de la información general de audiencia?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT model_name,
         model_type,
         segment_name,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  JOIN QSAccel.profile_agg.adwh_dim_segments c ON a.segment_id=c.segment_id
  WHERE a.merge_policy_id=1133248113
    AND a.model_id =1829081696
    AND a.segment_id=1870062812
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           segment_name,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Consulte la [documentación del widget de resumen de puntuación de inteligencia artificial aplicada al cliente](../guides/audiences.md#customer-ai-scoring-summary) para obtener información sobre la apariencia y la funcionalidad de esta perspectiva.

## Superposición de identidad {#identity-overlap}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la intersección común entre [!UICONTROL Tipo de identidad A] y [!UICONTROL Tipo de identidad B] para una audiencia filtrada?
- ¿Cómo refino las audiencias de los clientes en función de la superposición de tipos de identidad específicos para mejorar las estrategias de marketing segmentadas?
- ¿Qué perspectivas se pueden obtener de la evaluación del rendimiento de la campaña dentro de las áreas de intersección?
- En función de estas perspectivas, ¿cómo se pueden optimizar los esfuerzos de marketing futuros?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 1709997014
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('crmid',
                                                                                          'email')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'email'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10' ) a;
```

+++

Consulte la [documentación del widget de superposición de identidad](../guides/audiences.md#identity-overlap) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Perfiles por identidad {#profiles-by-identity}

Preguntas respondidas por esta perspectiva:

- ¿Qué tipo de identidad tiene la mayor proporción dentro del recuento total de perfiles para una audiencia seleccionada?
- ¿Existen disparidades significativas entre los tipos de identidad para una audiencia seleccionada?
- ¿Cuál es la distribución general de los tipos de identidad por audiencia?
- ¿Existen disparidades o anomalías significativas en los recuentos de identidad para distintas audiencias?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Consulte la [documentación del widget Perfiles por identidad](../guides/audiences.md#profiles-by-identity) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Activaciones programadas {#scheduled-activations}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son las fechas de inicio y finalización de las activaciones de mayor rendimiento para una audiencia concreta en una plataforma específica?
- ¿Qué plataformas se utilizaron más para las activaciones programadas de una audiencia concreta?
- ¿Hay algún patrón en el uso de la plataforma que pueda guiar las decisiones sobre la priorización o diversificación de las estrategias de activación para una audiencia específica?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT p.destination_platform ,
       p.destination_platform_name AS platform ,
       d.destination_name ,
       d.destination ,
       br.start_date ,
       CASE
           WHEN br.end_date = '9999-12-31' THEN 'Ongoing'
           ELSE br.end_date
       END AS end_date
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations br
  JOIN qsaccel.profile_agg.adwh_dim_destination d ON br.destination_id = d.destination_id
  JOIN qsaccel.profile_agg.adwh_dim_destination_platform p ON d.destination_platform_id = p.destination_platform_id
  JOIN
    (SELECT MAX(process_date) AS last_process_date
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) lpd ON lpd.last_process_date BETWEEN br.start_date AND br.end_date
  AND br.segment_id = 1333234510;
```

+++

Consulte la [documentación del widget de activaciones programadas](../guides/audiences.md#scheduled-activations) para obtener información sobre el aspecto y la funcionalidad de esta perspectiva.

## Pasos siguientes

Al leer este documento, ahora comprende el SQL que genera perspectivas del panel y qué preguntas comunes resuelve este análisis. Ahora puede editar e iterar en SQL para generar sus propias perspectivas.

Consulte la [Documentación de vista de SQL](../view-sql.md) para obtener más información sobre cómo adaptar el SQL de sus perspectivas directamente a través de la IU de PLatform.

También puede leer y comprender el SQL que genera perspectivas para los paneles de [Perfiles](./profiles.md), [Perfiles de cuenta](./account-profiles.md) y [Destinos](./destinations.md).
