---
title: Devolución y uso de variables de comercialización a partir de datos de análisis
description: Obtenga información sobre cómo proporcionar campos XDM y consultas de ejemplo para acceder a las variables de comercialización en sus conjuntos de datos de Analytics.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# Devolución y uso de variables de comercialización a partir de datos de Analytics

Utilice el servicio de consulta para administrar los datos ingeridos de Adobe Analytics en Adobe Experience Platform como conjuntos de datos. Las secciones siguientes proporcionan consultas de ejemplo que puede utilizar para acceder a las variables de comercialización de sus conjuntos de datos de Analytics. Consulte la documentación para obtener más información sobre [ingesta y asignación de datos de Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=es) a través del origen de Analytics

## Variables de comercialización {#merchandising-variables}

Las variables de comercialización pueden seguir una de dos sintaxis:

* **Sintaxis del producto**: Asocia el valor de eVar a un producto. 
* **Sintaxis de la variable de conversión**: Asocia el eVar con un producto solo si se produce un evento de enlace. Puede seleccionar los eventos que actúan como eventos de enlace.

## Sintaxis del producto {#product-syntax}

En Adobe Analytics, los datos personalizados de nivel de producto se pueden recopilar mediante variables configuradas especialmente llamadas variables de comercialización. Se basan en un eVar o en eventos personalizados. La diferencia entre estas variables y su uso habitual es que representan un valor independiente para cada producto encontrado en la visita, en lugar de representar un solo valor para la visita.

Estas variables se denominan variables de comercialización de sintaxis de producto. Esto permite la recopilación de información, como una &quot;cantidad de descuento&quot; por producto o información sobre la &quot;ubicación en la página&quot; del producto en los resultados de búsqueda del cliente.

Para obtener más información sobre el uso de la sintaxis del producto, consulte la documentación de Adobe Analytics sobre [implementación de eVars con sintaxis de producto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

Las secciones siguientes describen los campos XDM necesarios para acceder a las variables de comercialización de su [!DNL Analytics] conjunto de datos:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: Índice de la matriz a la que está accediendo.
* `evar#`: La variable de eVar específica a la que accede.

### Eventos personalizados

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: Índice de la matriz a la que está accediendo.
* `event#`: La variable de evento personalizada específica a la que accede.

## Casos de uso de sintaxis del producto {#product-use-cases}

Los siguientes casos de uso se centran en devolver un eVar de comercialización del `productListItems` matriz utilizando SQL.

### Devolver un eVar y un evento de comercialización

La siguiente consulta devuelve un eVar y un evento de comercialización para el primer producto que se encuentra en la variable `productListItems` matriz.

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

### Explore la matriz productListItems y devuelva el eVar y el evento de comercialización de cada producto.

Esta siguiente consulta explota el `productListItems` y devuelve cada eVar y evento de comercialización por producto. La variable `_id` se incluye para mostrar la relación con la visita original. La variable `_id` es una clave principal única para el conjunto de datos.

>[!NOTE]
>
>La función explode separa los elementos de una matriz en varias filas. Excluye los valores nulos.

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
> Si intenta recuperar un campo que no existe en su conjunto de datos actual, se produce el error &quot;No se produce ese campo de estructura&quot;. Evalúe el motivo devuelto en el mensaje de error para identificar un campo disponible, luego actualice la consulta y vuelva a ejecutarla.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintaxis de la variable de conversión {#conversion-variable-syntax}

Otro tipo de variable de comercialización que se encuentra en Adobe Analytics es la sintaxis de la variable de conversión. La sintaxis de la variable de conversión se utiliza cuando el valor de eVar no está disponible para configurarse en la variable products. Por lo general, esto significa que la página no dispone de contexto para el método de búsqueda o el canal de comercialización. En estos casos, debe configurar la variable de comercialización antes de que el usuario llegue a la página del producto y el valor persistirá hasta que se produzca el evento de enlace.

Por ejemplo, el escenario de búsqueda de productos que se muestra a continuación ilustra cómo los datos necesarios pueden estar presentes en una página antes de que se produzca la conversión o el evento relacionado con el producto.

1. Un usuario realiza una búsqueda interna de &quot;sombrero de invierno&quot; que establece la sintaxis de conversión habilitada para la comercialización de eVar6 en &quot;búsqueda interna:sombrero de invierno&quot;.
2. El usuario hace clic en &quot;waffle beanie&quot; y aterriza en la página de detalles del producto.\
   a. Aquí el aterrizaje se dispara `Product View` para el evento &quot;waffle beanie&quot; por $12.99.\
   b. Since `Product View` está configurado como un evento de enlace, el producto &quot;waffle beanie&quot; está ahora enlazado al valor eVar6 de &quot;internal search:winter hat&quot;. Cada vez que se recopila el producto &quot;waffle beanie&quot;, se asocia con &quot;internal search:winter hat&quot;. Esto sucede hasta que se alcanza la configuración de caducidad del eVar o hasta que se establece un nuevo valor de eVar6 y se vuelve a producir el evento de enlace con ese producto.
3. El usuario agrega el producto al carro de compras y activa la variable `Cart Add` evento.
4. El usuario realiza otra búsqueda interna de &quot;camisa de verano&quot; que establece la sintaxis de conversión habilitada para la comercialización de eVar6 en &quot;búsqueda interna:camisa de verano&quot;.
5. El usuario selecciona &quot;camiseta deportiva&quot; y aterriza en la página de detalles del producto.\
   a. Aquí el aterrizaje se dispara `Product View` evento para &quot;camiseta deportiva por 19,99 $.\
   b. Como `Product View` es el evento de enlace, el producto &quot;camiseta deportiva&quot; está ahora enlazado al valor eVar6 de &quot;búsqueda interna: camisa de verano&quot;. El producto anterior &quot;waffle beanie&quot; sigue enlazado a un valor eVar6 de &quot;internal search:waffle beanie&quot;.
6. El usuario agrega el producto al carro de compras y activa la variable `Cart Add` evento.
7. El usuario cierra la compra con ambos productos.

En los informes, los pedidos, los ingresos, las vistas de productos y los adiciones al carro de compras se pueden registrar en relación con el eVar 6 y se alinean con la actividad del producto enlazado.

| eVar6 (método de búsqueda de productos) | ingresos | pedidos | vistas del producto | adiciones al carro de compras |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| búsqueda interna:camisa de verano | 19,99 | 1 | 1 | 1 |
| búsqueda interna:sombrero de invierno | 12.99 | 1 | 1 | 1 |

Para obtener más información sobre el uso de la sintaxis de la variable de conversión, consulte la documentación de Adobe Analytics en [implementación de eVars con sintaxis de variable de conversión](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

A continuación se muestran los campos XDM para generar la sintaxis de la variable de conversión en la variable [!DNL Analytics] conjunto de datos:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: La variable de eVar específica a la que accede.

#### Producto

```console
productListItems[#].sku
```

* `#`: Índice de la matriz a la que está accediendo.

## Casos de uso de variables de conversión {#conversion-variable-use-cases}

Los casos de uso siguientes reflejan escenarios que requieren sintaxis de variable de conversión.

### Enlace el valor al producto específico y al par de eventos

La siguiente consulta vincula el valor al producto específico y al par de eventos. En este ejemplo, el valor está enlazado al evento de vista del producto.

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

### Conservar el valor enlazado en incidencias posteriores del producto correspondiente

La siguiente consulta de ejemplo mantiene el valor enlazado a incidencias posteriores del producto correspondiente. La subconsulta más baja establece la relación del valor con el producto en el evento de enlace declarado. La siguiente subconsulta realiza la atribución de ese valor enlazado en las interacciones posteriores con el producto correspondiente. El SELECT de nivel superior agrega los resultados para generar el informe.

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

## Pasos siguientes

Al leer este documento, debe comprender mejor cómo devolver un eVar de comercialización mediante la sintaxis del producto y enlazar un valor a un producto específico con la sintaxis de la variable de conversión.

Si aún no lo ha hecho, debe leer el [Documentación de perspectivas de Analytics para interacciones web y móviles](./analytics-insights.md) siguiente. Proporciona casos de uso comunes y muestra cómo utilizar el servicio de consulta para crear perspectivas procesables a partir de datos web y móviles de Adobe Analytics.
