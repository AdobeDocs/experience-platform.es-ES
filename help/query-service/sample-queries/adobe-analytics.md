---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consultas de ejemplo;consulta de ejemplo;adobe analytics;
solution: Experience Platform
title: Consultas de ejemplo para datos de Adobe Analytics
description: Los datos de los grupos de informes de Adobe Analytics seleccionados se transforman en XDM ExperienceEvents e se incorporan en Adobe Experience Platform como conjuntos de datos. Este documento describe una serie de casos de uso en los que Query Service utiliza estos datos e incluye consultas de ejemplo diseñadas para trabajar con sus conjuntos de datos de Adobe Analytics.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Consultas de ejemplo para datos de Adobe Analytics

Los datos de los grupos de informes de Adobe Analytics seleccionados se transforman en datos que se ajustan al [!DNL XDM ExperienceEvent] e ingerida en Adobe Experience Platform como conjuntos de datos.

Este documento describe una serie de casos de uso en los que Adobe Experience Platform [!DNL Query Service] utiliza estos datos. Consulte la documentación sobre [Asignación de campos de Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) para obtener más información sobre la asignación a [!DNL Experience Events].

Consulte la [documentación de casos de uso de analytics](../use-cases/analytics-insights.md) para aprender a utilizar el servicio de consulta para crear perspectivas procesables a partir de datos de Adobe Analytics ingestados.

## Anulación de duplicación

[!DNL Query Service] admite la deduplicación de datos. Consulte la [Deduplicación de datos en [!DNL Query Service] documentación](../best-practices/deduplication.md) para obtener información sobre cómo generar nuevos valores en el momento de la consulta [!DNL Experience Event] conjuntos de datos.

## Variables de comercialización (sintaxis del producto)

Las secciones siguientes proporcionan campos XDM y consultas de ejemplo que puede utilizar para acceder a las variables de comercialización de su [!DNL Analytics] conjunto de datos.

### Sintaxis del producto

En Adobe Analytics, los datos personalizados de nivel de producto se pueden recopilar mediante variables configuradas especialmente llamadas variables de comercialización. Se basan en un eVar o en eventos personalizados. La diferencia entre estas variables y su uso habitual es que representan un valor independiente para cada producto encontrado en la visita, en lugar de representar un solo valor para la visita.

Estas variables se denominan variables de comercialización de sintaxis de producto. Esto permite la recopilación de información, como una &quot;cantidad de descuento&quot; por producto o información sobre la &quot;ubicación en la página&quot; del producto en los resultados de búsqueda del cliente.

Para obtener más información sobre el uso de la sintaxis del producto, consulte la documentación de Adobe Analytics sobre [implementación de eVars con sintaxis de producto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Las secciones siguientes describen los campos XDM necesarios para acceder a las variables de comercialización de su [!DNL Analytics] conjunto de datos:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: Índice de la matriz a la que está accediendo.
- `evar#`: La variable de eVar específica a la que accede.

#### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: Índice de la matriz a la que está accediendo.
- `event#`: La variable de evento personalizada específica a la que accede.

#### Consultas de ejemplo

Esta es una consulta de ejemplo que devuelve un eVar y un evento de comercialización para el primer producto que se encuentra en la variable `productListItems`.

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

Esta siguiente consulta explota el `productListItems` y devuelve cada eVar y evento de comercialización por producto. La variable `_id` se incluye para mostrar la relación con la visita original. La variable `_id` es una clave principal única para el conjunto de datos.

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
> Si intenta recuperar un campo que no existe en el conjunto de datos actual, se producirá el error &quot;No se encuentra dicho campo de estructura&quot;. Evalúe el motivo devuelto en el mensaje de error para identificar un campo disponible, luego actualice la consulta y vuelva a ejecutar.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintaxis de conversión

Otro tipo de variable de comercialización que se encuentra en Adobe Analytics es la sintaxis de conversión. Con la sintaxis del producto, el valor se recopila al mismo tiempo que el producto, pero esto requiere que los datos estén presentes en la misma página. Hay escenarios en los que los datos se producen en una página antes de la conversión o el evento de interés relacionado con el producto. Por ejemplo, considere el caso de uso del método de búsqueda de productos.

1. Un usuario realiza una búsqueda interna de &quot;sombrero de invierno&quot; que establece Sintaxis de conversión habilitada eVar de comercialización 6 como &quot;búsqueda interna:sombrero de invierno&quot;
2. El usuario hace clic en &quot;waffle beanie&quot; y aterriza en la página de detalles del producto.\
   a. Aquí el aterrizaje se dispara `Product View` para el evento &quot;waffle beanie&quot; por $12.99.\
   b. Since `Product View` está configurado como un evento de enlace, el producto &quot;waffle beanie&quot; está ahora enlazado al valor eVar6 de &quot;internal search:winter hat&quot;. Cada vez que se recopile el producto &quot;waffle beanie&quot;, se asociará a &quot;internal search:winter hat&quot; hasta que (1) se alcance la configuración de caducidad o (2) se establezca un nuevo valor de eVar6 y se produzca de nuevo el evento de enlace con ese producto.
3. El usuario agrega el producto al carro de compras y activa la variable `Cart Add` evento.
4. El usuario realiza otra búsqueda interna de &quot;camisa de verano&quot; que establece la Sintaxis de conversión habilitada eVar de comercialización 6 en &quot;búsqueda interna:camisa de verano&quot;
5. El usuario hace clic en &quot;camiseta deportiva&quot; y llega a la página de detalles del producto.\
   a. Aquí el aterrizaje se dispara `Product View` evento para &quot;camiseta deportiva por 19,99 $.\
   b. La variable `Product View` el evento sigue siendo nuestro evento de enlace, por lo que ahora el producto &quot;camiseta deportiva&quot; está ahora enlazado al valor eVar6 de &quot;búsqueda interna:camisa de verano&quot; y el producto anterior &quot;waffle beanie&quot; está todavía enlazado a un valor eVar6 de &quot;búsqueda interna:waffle beanie&quot;.
6. El usuario agrega el producto al carro de compras y activa la variable `Cart Add` evento.
7. El usuario cierra la compra con ambos productos.

En los informes, los pedidos, los ingresos, las vistas de productos y los adiciones al carro de compras se podrán registrar en relación con el eVar 6 y se alinearán con la actividad del producto enlazado.

| eVar6 (método de búsqueda de productos) | ingresos | pedidos | vistas del producto | adiciones al carro de compras |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| búsqueda interna:camisa de verano | 19,99 | 1 | 1 | 1 |
| búsqueda interna:sombrero de invierno | 12.99 | 1 | 1 | 1 |

Para obtener más información sobre el uso de la sintaxis de conversión, consulte la documentación de Adobe Analytics sobre [implementación de eVars con sintaxis de conversión](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Estos son los campos XDM para generar la sintaxis de conversión en la [!DNL Analytics] conjunto de datos:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: La variable de eVar específica a la que accede.

#### Producto

```console
productListItems[#].sku
```

- `#`: Índice de la matriz a la que está accediendo.

#### Consultas de ejemplo

Esta es una consulta de ejemplo que vincula el valor al producto específico y al par de eventos, en este caso el evento de vista del producto.

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

A continuación, se muestra una consulta de ejemplo que persiste el valor enlazado a incidencias posteriores del producto correspondiente. La subconsulta más baja establece la relación de valores con el producto en el evento de enlace declarado. La siguiente subconsulta realiza la atribución de ese valor enlazado en las interacciones posteriores con el producto correspondiente. Y la selección de nivel superior agrega los resultados para generar el informe.

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
