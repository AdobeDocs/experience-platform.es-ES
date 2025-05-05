---
title: Perspectivas del perfil de cuenta
description: Descubra el SQL que alimenta las perspectivas de su perfil de cuenta y utilice estas consultas para generar perspectivas personalizadas que exploren aún más a sus clientes y sus experiencias como consumidores.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edición B2P" type="Informative" url="https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Datos del perfil de cuenta

[Los perfiles de cuenta](../../rtcdp/accounts/account-profile-overview.md) se utilizan para consolidar información de cuenta de varias fuentes, incluidos varios canales de marketing y sistemas organizativos. Esta vista unificada permite comprender las cuentas de los clientes y mejorar las campañas de marketing B2B. Las perspectivas derivadas del análisis del modelo de datos hacen que los datos B2B de Adobe Real-Time CDP sean más accesibles, comprensibles e impactantes para la toma de decisiones.

Con acceso al SQL que alimenta sus perspectivas, puede comprender mejor sus datos B2B y generar sus propias perspectivas reutilizables altamente personalizadas para explorar aún más la información de su cuenta de cliente. Transforme los datos sin procesar en nuevas perspectivas procesables mediante el uso del modelo de datos SQL de Real-Time CDP existente como inspiración para crear consultas para sus necesidades comerciales únicas.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Las siguientes perspectivas están disponibles para que las use como parte del [panel de perfiles de cuenta](../guides/account-profiles.md) o un [panel personalizado](../standard-dashboards.md). Consulte la [descripción general de la personalización](../customize/overview.md) para obtener instrucciones sobre cómo personalizar el tablero o [crear y editar nuevos widgets](../customize/custom-widgets.md) en la biblioteca de widgets y [tablero definido por el usuario](../standard-dashboards.md#create-widget).

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

## Nuevas cuentas por sector {#accounts-by-industry}

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

## Nuevas cuentas por tipo {#accounts-by-type}

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

## Nuevas oportunidades por función de persona {#opportunities-by-person-role}

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

## Nuevas oportunidades por ingresos {#opportunities-by-revenue}

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

## Nuevas oportunidades por estado y etapa {#opportunities-by-status-and-stage}

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

## Nuevas oportunidades ganadas {#opportunities-won}

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

## Resumen de clientes por cuenta {#customers-per-account-overview}

>[!NOTE]
>
>El gráfico [!UICONTROL Información general de clientes por cuenta] incluye tres detalles de obtención de detalles: [!UICONTROL Clientes por detalle de cuenta], [!UICONTROL Información general de oportunidades por cuenta] y [!UICONTROL Oportunidades por detalle de cuenta]. Estos desgloses de detalles proporcionan perspectivas más granulares, desglosando los recuentos de clientes y oportunidades por categorías (como clientes directos e indirectos) e intervalos (como clientes y bandas de recuento de oportunidades). Estos gráficos no se ven afectados por los filtros de fecha globales que haya establecido.

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la distribución de las cuentas en función de si tienen clientes directos o indirectos?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH LatestDate AS (SELECT MAX(inserted_date) AS max_inserted_date FROM adwh_b2b_account_person_association),
     CategorizedData AS (
         SELECT CASE 
                    WHEN is_direct = 'true' AND person_count = 0 THEN 'Accounts without Direct Customers' 
                    WHEN is_direct = 'false' AND person_count = 0 THEN 'Accounts without Indirect Customers' 
                    WHEN is_direct = 'true' AND person_count > 0 THEN 'Accounts with Direct Customers' 
                    WHEN is_direct = 'false' AND person_count > 0 THEN 'Accounts with Indirect Customers' 
                END AS Account_Category, 
                account_count 
         FROM adwh_b2b_account_person_association 
         WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
     ),
     AggregatedData AS (
         SELECT Account_Category, SUM(account_count) AS Accounts 
         FROM CategorizedData 
         GROUP BY Account_Category
     ),
     AllCategories AS (
         SELECT 'Accounts without Direct Customers' AS Account_Category 
         UNION ALL SELECT 'Accounts without Indirect Customers' 
         UNION ALL SELECT 'Accounts with Direct Customers' 
         UNION ALL SELECT 'Accounts with Indirect Customers'
     )
SELECT ac.Account_Category AS Account_Category, COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad ON ac.Account_Category = ad.Account_Category 
ORDER BY ac.Account_Category;
```

+++

## Clientes por detalle de cuenta {#customers-per-account-detail}

>[!NOTE]
>
>Esta perspectiva no se ve afectada por los filtros de fecha globales.

Preguntas respondidas por esta perspectiva:

- ¿Cuántas cuentas tienen distintos rangos de clientes directos o indirectos?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH customer_ranges AS (
    SELECT 'Direct Customer' AS customer_type, '1-10 Customers' AS person_range 
    UNION ALL
    SELECT 'Direct Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '1000+ Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1-10 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1000+ Customers'
)
SELECT 
    cr.customer_type, 
    cr.person_range, 
    COALESCE(SUM(ap.account_count), 0) AS Accounts
FROM customer_ranges cr
LEFT JOIN (
    SELECT 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END AS customer_type,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END AS person_range,
        SUM(account_count) AS account_count
    FROM adwh_b2b_account_person_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_person_association) 
    GROUP BY 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END
) ap ON cr.customer_type = ap.customer_type AND cr.person_range = ap.person_range
GROUP BY cr.customer_type, cr.person_range
ORDER BY cr.customer_type, 
    CASE cr.person_range 
        WHEN '1-10 Customers' THEN 1 
        WHEN '11-100 Customers' THEN 2 
        WHEN '101-1000 Customers' THEN 3 
        WHEN '1000+ Customers' THEN 4 
    END;
```

+++

## Resumen de oportunidades por cuenta {#opportunities-per-account-overview}

>[!NOTE]
>
>Esta perspectiva no se ve afectada por los filtros de fecha globales.

Preguntas respondidas por esta perspectiva:

- ¿Cuál es la distribución de las cuentas en función de si tienen oportunidades asociadas?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH LatestDate AS (
    SELECT MAX(inserted_date) AS max_inserted_date 
    FROM adwh_b2b_account_opportunity_association
),
CategorizedData AS (
    SELECT 
        CASE 
            WHEN opportunity_count = 0 THEN 'Accounts without Opportunities'
            WHEN opportunity_count > 0 THEN 'Accounts with Opportunities'
        END AS Opportunity_Category, 
        account_count 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
),
AggregatedData AS (
    SELECT 
        Opportunity_Category,
        SUM(account_count) AS Accounts 
    FROM CategorizedData 
    GROUP BY Opportunity_Category
),
AllCategories AS (
    SELECT 'Accounts without Opportunities' AS Opportunity_Category 
    UNION ALL 
    SELECT 'Accounts with Opportunities'
)
SELECT 
    ac.Opportunity_Category AS Opportunity_Category, 
    COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad 
    ON ac.Opportunity_Category = ad.Opportunity_Category 
ORDER BY ac.Opportunity_Category;
```

+++

## Oportunidades por detalle de cuenta {#opportunities-per-account-detail}

>[!NOTE]
>
>Esta perspectiva no se ve afectada por los filtros de fecha globales.

Preguntas respondidas por esta perspectiva:

- ¿Cuántas cuentas tienen diferentes rangos de oportunidades asociadas?

+++Seleccione para mostrar el SQL que genera esta perspectiva

```sql
WITH opportunity_ranges AS (
    SELECT '1-10 Opportunities' AS opportunity_range 
    UNION ALL 
    SELECT '11-50 Opportunities' 
    UNION ALL 
    SELECT '51-100 Opportunities' 
    UNION ALL 
    SELECT '100+ Opportunities'
)
SELECT opportunity_ranges.opportunity_range AS OPPORTUNITIES, 
       COALESCE(SUM(accounts.total_accounts), 0) AS ACCOUNTS 
FROM opportunity_ranges 
LEFT JOIN (
    SELECT 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END AS opportunity_range, 
        SUM(account_count) AS total_accounts 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_opportunity_association) 
      AND opportunity_count > 0 
    GROUP BY 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END
) AS accounts ON opportunity_ranges.opportunity_range = accounts.opportunity_range 
GROUP BY opportunity_ranges.opportunity_range 
ORDER BY CASE opportunity_ranges.opportunity_range 
            WHEN '1-10 Opportunities' THEN 1 
            WHEN '11-50 Opportunities' THEN 2 
            WHEN '51-100 Opportunities' THEN 3 
            WHEN '100+ Opportunities' THEN 4 
        END;
```

+++

## Pasos siguientes

Al leer este documento, ahora comprende el SQL que genera las perspectivas del panel de perfiles de cuenta y qué preguntas comunes resuelve este análisis. Ahora puede editar e iterar en SQL para generar sus propias perspectivas. Consulte la [descripción general del modo Query Pro](../sql-insights-query-pro-mode/overview.md) para obtener información sobre cómo generar perspectivas personalizadas con SQL.

También puede leer y comprender el SQL que genera perspectivas para los paneles de [Perfiles](./profiles.md), [Audiencias](./audiences.md) y [Destinos](./destinations.md).
