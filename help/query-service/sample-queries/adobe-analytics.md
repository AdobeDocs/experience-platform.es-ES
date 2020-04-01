---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: consultas de muestra
topic: queries
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# consultas de muestra para datos de Adobe Analytics

Los datos de los grupos de informes de Adobe Analytics seleccionados se transforman en eventos de experiencia XDM y se transfieren a la plataforma de Adobe Experience como conjuntos de datos para usted. Este documento describe una serie de casos de uso en los que el servicio de Consulta de la plataforma de experiencia de Adobe hace uso de estos datos, y las consultas de muestra incluidas deberían funcionar con sus conjuntos de datos de Adobe Analytics. Consulte la documentación [de asignación de campos de](../../source-connectors/ui/adobe-applications/analytics-mapping.md) Analytics para obtener más información sobre la asignación a ExperienceEvents de XDM.

## Primeros pasos

Los ejemplos SQL de este documento requieren que edite el SQL y rellene los parámetros esperados para sus consultas en función del conjunto de datos, eVar, evento o intervalo de tiempo que le interese evaluar. Proporcione parámetros donde quiera que vea `{ }` en los siguientes ejemplos de SQL.

## Ejemplos SQL que se utilizan habitualmente

### Recuento de visitantes por hora para un día determinado

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### Las 10 páginas más visitadas de un día determinado

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Los 10 usuarios más activos

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Principales 10 ciudades por actividad del usuario

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Los 10 productos más vistos

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 10 ingresos totales principales de pedidos

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Recuentos de Eventos por día

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## Variables de comercialización (sintaxis del producto)

En Adobe Analytics, los datos personalizados de nivel de producto se pueden recopilar mediante variables configuradas especialmente llamadas &quot;Variables de comercialización&quot;. Se basan en una eVar o en un Evento personalizado. La diferencia entre estas variables y su uso estándar es que representan un valor por separado para cada producto encontrado en la visita, en lugar de representar un solo valor para la visita. Estas variables se denominan variables de comercialización de sintaxis de producto. Esto permite la recopilación de información como una &quot;cantidad de descuento&quot; por producto o información sobre la &quot;ubicación en la página&quot; del producto en los resultados de búsqueda del cliente.

Estos son los campos XDM para acceder a las variables de comercialización en el conjunto de datos de Analytics:

### eVars

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Donde `[#]` es un índice de matriz y `evar#` es la variable eVar específica.

### Eventos personalizados

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

Donde `[#]` es un índice de matriz y `event#` es la variable de evento personalizada específica.

### consultas de muestra

Esta es una consulta de muestra que devuelve una eVar de comercialización y un evento para el primer producto encontrado en la `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

La siguiente consulta &#39;explota&#39; la `productListItems` y devuelve cada eVar de comercialización y cada evento por producto. El `_id` campo se incluye para mostrar la relación con la visita original. El `_id` valor es una clave principal única en el conjunto de datos de ExperienceEvent.

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### Error común al implementar las consultas de muestra

Se encuentra el error &quot;No existe dicho campo de estructura&quot; cuando intenta recuperar un campo que no existe en el conjunto de datos actual. Evalúe el motivo devuelto en el mensaje de error para identificar un campo disponible y, a continuación, actualice la consulta y vuelva a ejecutarlo.

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Variables de comercialización (sintaxis de conversión)

Otro tipo de variable de comercialización que se encuentra en Adobe Analytics es la sintaxis de conversión. Con Sintaxis del producto, el valor se recopila al mismo tiempo que el producto, pero esto requiere que los datos estén presentes en la misma página. Existen escenarios en los que los datos se producen en una página antes de la conversión o el evento de interés relacionado con el producto. Por ejemplo, considere el caso de uso del sistema de informes de métodos de búsqueda de productos.

1. Un usuario realiza una búsqueda interna de &quot;sombrero de invierno&quot; que establece la sintaxis de conversión habilitada para la eVar de comercialización en &quot;búsqueda interna:sombrero de invierno&quot;
2. El usuario hace clic en &quot;waffle beanie&quot; y aterriza en la página de detalles del producto.\
   a. Aterrizar acá dispara un `Product View` evento por el &quot;pimiento de gofre&quot; por $12.99.\
   b. Debido a que `Product View` está configurado como un evento de enlace, el producto &quot;waffle beanie&quot; ahora está enlazado al valor de eVar6 de &quot;internal search:winter hat&quot;. Cada vez que se recopile el producto &quot;waffle beanie&quot;, se asociará a &quot;search:winter hat&quot; hasta que (1) se alcance la configuración de caducidad o (2) se establezca un nuevo valor de eVar6 y se vuelva a producir el evento de enlace con ese producto.
3. El usuario agrega el producto al carro de compras, activando el `Cart Add` evento.
4. El usuario realiza otra búsqueda interna de &quot;camisa de verano&quot; que establece la sintaxis de conversión habilitada para la eVar de comercialización en &quot;búsqueda interna:camisa de verano&quot;
5. El usuario hace clic en &quot;camiseta deportiva&quot; y aterriza en la página de detalles del producto.\
   a. Aterrizar acá dispara un `Product View` evento por &quot;camiseta deportiva por $19.99.\
   b. El `Product View` evento sigue siendo nuestro evento de encuadernación, así que ahora el producto &quot;camiseta deportiva&quot; está enlazado al valor eVar6 de &quot;búsqueda interna:camisa de verano&quot; y el producto anterior &quot;waffle beanie&quot; está todavía enlazado a un valor eVar6 de &quot;búsqueda interna:waffle beanie&quot;.
6. El usuario agrega el producto al carro de compras, activando el `Cart Add` evento.
7. El usuario cierra la compra con ambos productos.

En sistema de informes, los pedidos, los ingresos, las vistas de productos y las adiciones al carro de compras se registrarán en la eVar6 y se alinearán con la actividad del producto vinculado.

| eVar6 (método de búsqueda de productos) | ingresos | pedidos | vistas del producto | adiciones al carro de compras |
|---|---|---|---|---|
| búsqueda interna:camisa de verano | 19.99 | 1 | 1 | 1 |
| búsqueda interna:sombrero de invierno | 12.99 | 1 | 1 | 1 |

Estos son los campos XDM para generar la sintaxis de conversión en el conjunto de datos de Analytics:

### eVars

```
_experience.analytics.customDimensions.evars.evar#
```

Dónde `evar#` está la variable eVar específica.

### Producto

```
productListItems[#].sku
```

Donde `[#]` es un índice de matriz.

### consultas de muestra

A continuación se muestra una consulta de muestra que vincula el valor al par de productos y eventos específico, en este caso el evento de vista del producto.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

A continuación se muestra una consulta de muestra que mantiene el valor enlazado a incidencias posteriores del producto correspondiente. La subconsulta más baja establece la relación de valores con el producto en el evento de enlace declarado. La siguiente subconsulta realiza la atribución de ese valor enlazado en las interacciones posteriores con el producto correspondiente. Y la selección de nivel superior agrega los resultados para producir el sistema de informes.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```
