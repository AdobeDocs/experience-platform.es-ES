---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;consultas de muestra;consulta de muestra;adobe analytics;
solution: Experience Platform
title: Consultas de muestra
topic: queries
description: Los datos de los grupos de informes de Adobe Analytics seleccionados se transforman en eventos de experiencia XDM y se ingeryen en Adobe Experience Platform como conjuntos de datos para usted. Este documento describe una serie de casos de uso en los que el Servicio de Consulta de Adobe Experience Platform utiliza estos datos, y las consultas de muestra incluidas deberían funcionar con sus conjuntos de datos de Adobe Analytics.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---


# Consultas de muestra para datos de Adobe Analytics

Los datos de los grupos de informes de Adobe Analytics seleccionados se transforman en datos que se ajustan a la clase [!DNL XDM ExperienceEvent] y se ingieren en Adobe Experience Platform como conjuntos de datos.

Este documento describe una serie de casos de uso en los que Adobe Experience Platform [!DNL Query Service] hace uso de estos datos, incluyendo consultas de muestra que deberían funcionar con sus datasets de Adobe Analytics. Consulte la documentación sobre [Asignación de campos de Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) para obtener más información sobre la asignación a [!DNL Experience Events].

## Primeros pasos

Los ejemplos SQL de este documento requieren que edite el SQL y rellene los parámetros esperados para sus consultas en función del conjunto de datos, el eVar, el evento o el intervalo de tiempo que le interese evaluar. Proporcione parámetros donde vea `{ }` en los ejemplos de SQL siguientes.

## Ejemplos SQL que se utilizan habitualmente

Los siguientes ejemplos muestran consultas SQL de uso común para analizar los datos de Adobe Analytics.

### Recuento de visitantes por hora para un día determinado

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Las 10 páginas más visitadas de un día determinado

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Los 10 usuarios más activos

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Principales 10 ciudades por actividad del usuario

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
        FROM   {TARGET_TABLE} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Recuentos de eventos por día

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## Variables de comercialización (sintaxis del producto)


### Sintaxis del producto

En Adobe Analytics, los datos de nivel de producto personalizados se pueden recopilar a través de variables configuradas especialmente llamadas variables de comercialización. Se basan en un eVar o en eventos personalizados. La diferencia entre estas variables y su uso estándar es que representan un valor por separado para cada producto encontrado en la visita, en lugar de representar un solo valor para la visita.

Estas variables se denominan variables de comercialización de sintaxis de producto. Esto permite la recopilación de información, como una &quot;cantidad de descuento&quot; por producto o información sobre la &quot;ubicación en la página&quot; del producto en los resultados de búsqueda del cliente.

Para obtener más información sobre el uso de la sintaxis del producto, lea la documentación de Adobe Analytics sobre [implementación de eVars con sintaxis de producto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Las secciones siguientes describen los campos XDM necesarios para acceder a las variables de comercialización en el conjunto de datos [!DNL Analytics]:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:: Índice de la matriz a la que está accediendo.
- `evar#`:: Variable de eVar específica a la que está accediendo.

#### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:: Índice de la matriz a la que está accediendo.
- `event#`:: Variable de evento personalizada específica a la que accede.

#### Consultas de muestra

Esta es una consulta de muestra que devuelve un eVar de comercialización y un evento para el primer producto encontrado en `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Esta siguiente consulta explota la matriz `productListItems` y devuelve cada eVar de comercialización y evento por producto. El campo `_id` se incluye para mostrar la relación con la visita original. El valor `_id` es una clave principal única para el conjunto de datos.

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
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> Si intenta recuperar un campo que no existe en el conjunto de datos actual, se producirá el error &quot;No existe dicho campo de estructura&quot;. Evalúe el motivo devuelto en el mensaje de error para identificar un campo disponible, luego actualice la consulta y vuelva a ejecutarlo.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintaxis de conversión

Otro tipo de variable de comercialización que se encuentra en Adobe Analytics es la sintaxis de conversión. Con la sintaxis del producto, el valor se recopila al mismo tiempo que el producto, pero esto requiere que los datos estén presentes en la misma página. Existen escenarios en los que los datos se producen en una página antes de la conversión o el evento de interés relacionado con el producto. Por ejemplo, considere el caso de uso del método de búsqueda de productos.

1. Un usuario realiza una búsqueda interna de &quot;sombrero de invierno&quot; que establece la sintaxis de conversión habilitada para el eVar de comercialización 6 en &quot;búsqueda interna:sombrero de invierno&quot;
2. El usuario hace clic en &quot;waffle beanie&quot; y aterriza en la página de detalles del producto.\
   a. Aterrizar aquí dispara un `Product View` evento por el &quot;waffle beanie&quot; por $12.99.\
   b. Debido a que `Product View` está configurado como un evento de enlace, el producto &quot;waffle beanie&quot; está ahora enlazado al valor de eVar6 de &quot;internal search:winter hat&quot;. Cada vez que se recopile el producto &quot;waffle beanie&quot;, se asociará a &quot;search:winter hat&quot; hasta que (1) se alcance la configuración de caducidad o (2) se establezca un nuevo valor eVar6 y se vuelva a producir el evento de enlace con ese producto.
3. El usuario agrega el producto al carro de compras, activando el evento `Cart Add`.
4. El usuario realiza otra búsqueda interna de &quot;camisa de verano&quot; que establece la Sintaxis de conversión habilitada eVar de comercialización 6 en &quot;búsqueda interna:camisa de verano&quot;
5. El usuario hace clic en &quot;camiseta deportiva&quot; y aterriza en la página de detalles del producto.\
   a. Aterrizar aquí dispara un evento de &quot;camiseta deportiva por $19.99.`Product View`\
   b. El evento `Product View` sigue siendo nuestro evento de encuadernación, por lo que ahora el producto &quot;camiseta deportiva&quot; está enlazado al valor eVar6 de &quot;búsqueda interna:camisa de verano&quot; y el producto anterior &quot;waffle beanie&quot; está todavía enlazado a un valor eVar6 de &quot;búsqueda interna:waffle beanie&quot;.
6. El usuario agrega el producto al carro de compras, activando el evento `Cart Add`.
7. El usuario cierra la compra con ambos productos.

En sistema de informes, los pedidos, los ingresos, las vistas de productos y las adiciones al carro de compras se registrarán con eVar6 y se alinearán con la actividad del producto vinculado.

| eVar6 (método de búsqueda de productos) | ingresos | pedidos | vistas del producto | adiciones al carro de compras |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| búsqueda interna:camisa de verano | 19,99 | 1 | 3 | 1 |
| búsqueda interna:sombrero de invierno | 12,99 | 1 | 1 | 1 |

Para obtener más información sobre el uso de la sintaxis de conversión, lea la documentación de Adobe Analytics sobre [implementación de eVars con sintaxis de conversión](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Estos son los campos XDM para generar la sintaxis de conversión en el conjunto de datos [!DNL Analytics]:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:: Variable de eVar específica a la que está accediendo.

#### Producto

```console
productListItems[#].sku
```

- `#`:: Índice de la matriz a la que está accediendo.

#### Consultas de muestra

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
