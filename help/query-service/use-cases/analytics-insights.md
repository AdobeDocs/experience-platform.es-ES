---
title: Perspectivas de Analytics para interacciones web y móviles
description: En este documento se explica cómo utilizar el servicio de consulta para crear perspectivas procesables a partir de datos de Adobe Analytics ingestados.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# Perspectivas de Analytics para interacciones web y móviles

Adobe Experience Platform le permite introducir datos de grupos de informes de Adobe Analytics mediante campos del Modelo de datos de experiencia (XDM) para rellenar conjuntos de datos. Estos datos de análisis se modifican para ajustarse al [!DNL XDM ExperienceEvent] Clase . A continuación, el servicio de consulta puede utilizar estos datos ejecutando consultas SQL para generar perspectivas valiosas a partir del comportamiento de un usuario en las plataformas digitales.

Este documento proporciona una variedad de consultas SQL de ejemplo que muestran casos de uso comunes al crear perspectivas a partir de datos de Analytics web y móviles.

Consulte la [Documentación de asignaciones de campos de Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) para obtener más información sobre la ingesta y asignación de datos de análisis.

## Primeros pasos

Para cada uno de los siguientes casos de uso, se proporciona un ejemplo de consulta SQL parametrizada como plantilla que puede personalizar. Proporcione parámetros donde quiera que vea `{ }` en los ejemplos SQL para el conjunto de datos, el eVar, el evento o el lapso de tiempo que le interese evaluar.

## Objetivos

Los siguientes ejemplos muestran consultas SQL para casos de uso comunes a fin de analizar los datos de Adobe Analytics.

### Generar el recuento de visitantes para cada hora de un día determinado

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Identificar las 10 páginas más vistas de un día determinado

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### Identificación de los 10 usuarios más activos

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Identificar las 10 ciudades más deseadas según la actividad del usuario

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Identificar los 10 productos más vistos

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Identificar los 10 ingresos de pedidos más altos

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```
