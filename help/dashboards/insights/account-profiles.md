---
title: Perspectivas del perfil de cuenta
description: Descubra el SQL que alimenta las perspectivas de su perfil de cuenta y utilice estas consultas para generar perspectivas personalizadas que exploren aún más a sus clientes y sus experiencias como consumidores.
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edición B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: b7875128592b17044b068d8064de082bf00a8309
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Datos del perfil de cuenta

[Perfiles de cuenta](../../rtcdp/accounts/account-profile-overview.md) se utilizan para consolidar información de cuentas de varias fuentes, incluidos varios canales de marketing y sistemas organizativos. Esta vista unificada permite comprender las cuentas de los clientes y mejorar las campañas de marketing B2B. Las perspectivas derivadas del análisis del modelo de datos hacen que los datos B2B de Adobe Real-time Customer Data Platform sean más accesibles, comprensibles e impactantes para la toma de decisiones.

Con acceso al SQL que alimenta sus perspectivas, puede comprender mejor sus datos B2B y generar sus propias perspectivas reutilizables altamente personalizadas para explorar aún más la información de su cuenta de cliente. Transforme los datos sin procesar en nuevas perspectivas procesables mediante el uso del modelo de datos SQL de Real-Time CDP existente como inspiración para crear consultas para sus necesidades comerciales únicas.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Las siguientes perspectivas están disponibles para que las utilice como parte de [Panel de perfiles de cuenta](../guides/account-profiles.md) o una [panel personalizado](../user-defined-dashboards.md). Consulte la [información general sobre personalización](../customize/overview.md) para obtener instrucciones sobre cómo personalizar el tablero o [crear y editar widgets nuevos](../customize/custom-widgets.md) en la biblioteca de widgets y [tablero definido por el usuario](../user-defined-dashboards.md#create-widget).

## Perfiles de cuenta añadidos {#account-profiles-added}

Preguntas respondidas por esta perspectiva:

- ¿Cuántos perfiles de cuenta se han añadido durante un periodo determinado?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## Cuentas por sector {#accounts-by-industry}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son los cinco sectores principales a los que pertenecen los perfiles de cuenta?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## Cuentas por tipo {#accounts-by-type}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el recuento de cuentas por tipo?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

## Oportunidades añadidas {#opportunities-added}

Preguntas respondidas por esta perspectiva:

- ¿Cuántas oportunidades se han agregado en un período determinado?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## Oportunidades por función de persona {#opportunities-by-person-role}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el tamaño relativo y el recuento de las distintas funciones de una oportunidad?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## Oportunidades por ingresos {#opportunities-by-revenue}

Preguntas respondidas por esta perspectiva:

- ¿Cuáles son las 20 oportunidades clasificadas por sus ingresos (en USD)?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## Oportunidades por estado y etapa {#opportunities-by-status-and-stage}

Preguntas respondidas por esta perspectiva:

- ¿Qué oportunidades abiertas existen y en qué fase del canal de ventas o marketing se encuentran?
- ¿Qué oportunidades cerradas existen y en qué fase del canal de ventas o marketing se encuentran?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## Oportunidades ganadas {#opportunities-won}

Preguntas respondidas por esta perspectiva:

- ¿Cuál es el recuento de oportunidades que se han cerrado o finalizado correctamente?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## Oportunidades ganadas (gráfico de líneas) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Preguntas respondidas por esta perspectiva:

- ¿Cuántas oportunidades se han cerrado o finalizado correctamente (ganadas) durante un periodo determinado?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## Pasos siguientes

Al leer este documento, ahora comprende el SQL que genera las perspectivas del panel de perfiles de cuenta y qué preguntas comunes resuelve este análisis. Ahora puede editar e iterar en SQL para generar sus propias perspectivas.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

También puede leer y comprender el SQL que genera perspectivas para [Perfiles](./profiles.md), [Audiencias](./audiences.md), y [Destinos](./destinations.md) paneles.
