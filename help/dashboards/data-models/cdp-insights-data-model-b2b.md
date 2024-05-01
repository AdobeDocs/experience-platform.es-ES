---
title: Real-time Customer Data Platform Insights Data Model edición B2B
description: Aprenda a utilizar las consultas SQL con los modelos de datos de Real-time Customer Data Platform Insights (edición B2B) para personalizar sus propios informes de Real-Time CDP para los casos de uso de KPI y marketing.
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edición B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: 52f67037756af97bac97908d4736a3cbafce6844
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Real-time Customer Data Platform Insights Data Model B2B Edition

El modelo de datos de Real-time Customer Data Platform Insights para la edición B2B expone los modelos de datos y SQL que alimentan las perspectivas para [perfiles de cuenta](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview). Puede personalizar estas plantillas de consulta SQL para crear informes de Real-Time CDP para los casos de uso de indicadores clave de rendimiento (KPI) y marketing B2B. Estas perspectivas pueden utilizarse como widgets personalizados para los paneles.

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el paquete Real-Time CDP Prime y Ultimate. Consulte la documentación sobre las [Ediciones de Real-Time CDP](../../rtcdp/overview.md#rtcdp-editions) para obtener más información, o póngase en contacto con el representante del Adobe.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/customizable-insights/reporting-insights-data-model.md).
 -->

## Requisitos previos

Esta guía requiere una comprensión práctica de los paneles personalizados. Lea la documentación sobre [cómo crear un tablero personalizado](../user-defined-dashboards.md) antes de continuar con esta guía.

## Informes de perspectivas y casos de uso de Real-Time CDP B2B {#B2B-insight-reports-and-use-cases}

Los informes de Real-Time CDP B2B proporcionan perspectivas sobre los datos de perfiles de su cuenta y la relación entre las cuentas y las oportunidades. Los siguientes modelos de esquema de estrella se desarrollaron para responder a una variedad de casos de uso de marketing comunes y cada modelo de datos puede admitir varios casos de uso.

>[!IMPORTANT]
>
>Los datos utilizados para los informes B2B de Real-Time CDP son precisos para una política de combinación elegida y a partir de la instantánea diaria más reciente.

### Modelo de perfil de cuenta {#account-profile-model}

El modelo Perfil de cuenta consta de ocho conjuntos de datos:

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

El diagrama siguiente muestra los campos de datos relevantes en cada conjunto de datos, su tipo de datos y las claves externas que vinculan los conjuntos de datos.

![El diagrama relacional de entidades para el modelo de perfil de cuenta.](../images/data-models/account-profile-model.png)

#### Las cuentas por caso de uso del sector {#accounts-by-industry}

La lógica utilizada para la variable [!UICONTROL Cuentas por sector] insight devuelve los cinco sectores principales según el número de perfiles de cuenta y el tamaño relativo entre ellos. Consulte la [[!UICONTROL Cuentas por sector] documentación del widget](../guides/account-profiles.md#accounts-by-industry) para obtener más información.

>[!TIP]
>
>Puede personalizar esta consulta SQL para que devuelva más o menos que las cinco industrias principales.

El SQL que genera el [!UICONTROL Cuentas por sector] la información se puede ver en la sección plegable a continuación.

+++Consulta SQL

```sql
WITH RankedIndustries AS (
    SELECT
        i.industry,
        SUM(f.counts) AS total_accounts,
        ROW_NUMBER() OVER (ORDER BY SUM(f.counts) DESC) AS industry_rank
    FROM
        adwh_fact_account f
    INNER JOIN adwh_dim_industry i ON f.industry_id = i.industry_id
    WHERE f.accounts_created_date between UPPER(COALESCE('$START_DATE', '')) and UPPER(COALESCE('$END_DATE', ''))
    GROUP BY
        i.industry
)
SELECT
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END AS industry_group,
    SUM(total_accounts) AS total_accounts
FROM
    RankedIndustries
GROUP BY
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END
ORDER BY
    total_accounts DESC
LIMIT 5000;
```

+++

#### El caso de uso Cuentas por tipo {#accounts-by-type}

La lógica utilizada para la variable [!UICONTROL Cuentas por tipo] insight devuelve el desglose numérico de las cuentas por tipo. Esta perspectiva puede ayudar a guiar la estrategia y las operaciones empresariales, incluidas las estrategias de asignación de recursos o marketing. Consulte la [[!UICONTROL Cuentas por tipo] documentación del widget](../guides/account-profiles.md#accounts-by-type) para obtener más información.

El SQL que genera el [!UICONTROL Cuentas por tipo] la información se puede ver en la sección plegable a continuación.

+++Consulta SQL

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

### Modelo de oportunidad {#opportunity-model}

El modelo de oportunidad consta de siete conjuntos de datos:

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

El diagrama siguiente muestra los campos de datos relevantes en cada conjunto de datos.

![El diagrama relacional de entidades para el modelo de oportunidad.](../images/data-models/opportunity-model.png)
