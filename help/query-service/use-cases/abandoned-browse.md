---
keywords: Experience Platform;servicio de consultas;servicio de consultas;consulta
title: Ejemplo de caso de uso para el servicio de consultas de Adobe Experience Platform
description: Un ejemplo completo para demostrar la versatilidad y las ventajas del servicio de consultas de Adobe Experience Platform.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Ejemplo de caso de uso para Adobe Experience Platform [!DNL Query Service]

Este documento y el vídeo que lo acompaña proporcionan un flujo de trabajo completo de alto nivel que muestra cómo Adobe Experience Platform [!DNL Query Service] beneficia las perspectivas empresariales estratégicas de su organización. Utilizando un caso de uso de abandono del explorador como ejemplo, esta guía ilustra los siguientes conceptos clave:

* La importancia clave del procesamiento de datos para maximizar el potencial de Adobe Experience Platform.
* Formas de generar la consulta en función de la arquitectura de datos existente.
* Garantice una calidad de datos que satisfaga sus necesidades y métodos para mitigar cualquier déficit.
* Proceso para programar una consulta de modo que se ejecute con una frecuencia determinada para su uso descendente en la segmentación y en los destinos de personalización.
* La facilidad con la que los especialistas en marketing pueden incluir atributos derivados en sus segmentos a través del poder de [!DNL Query Service].

## Objetivos {#objectives}

Esta demostración del flujo de trabajo se basa en varios servicios de Adobe Experience Platform. Si desea realizar el seguimiento, se recomienda tener una buena comprensión de las siguientes funciones y servicios:

* El [Conceptos básicos de la composición de esquemas del Modelo de datos de experiencia (XDM)](../../xdm/schema/composition.md)
* Cómo: [creación de conjuntos de datos e ingesta de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es)
* Cómo: [ingesta de datos mediante el conector de origen de Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=es)
* [Segmentación](../../segmentation/home.md)
* [Destinos](../../destinations/home.md)

El ejemplo de abandono de exploración se centra en el uso del Adobe [!DNL Analytics] datos para crear una audiencia procesable concreta. La audiencia se refina para incluir a todos los clientes que navegaron por el sitio web en los últimos cuatro días, pero que no realizaron una compra. A continuación, cada perfil de la audiencia se segmenta con el SKU de precio más alto resultante del patrón de comportamiento del cliente.

La propia consulta es muy prescriptiva y solo incluye datos que cumplen los criterios del caso de uso para la definición del segmento. Esto mejora el rendimiento al minimizar la cantidad de [!DNL Analytics] datos en proceso. También ordena los datos por precio de mayor a menor y elige el SKU con precio más alto que el usuario estaba explorando.

La consulta utilizada en la presentación se puede ver a continuación:

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] ejemplo de abandono de exploración con adobe analytics {#video-example}

La presentación de vídeo que se muestra a continuación proporciona un caso de uso integral en el mundo real para los datos de sus Experience Platform centrados en [!DNL Query Service] y integraciones de análisis de Adobe.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Ventajas de [!DNL Query Service] {#benefits}

Las funciones que proporciona [!DNL Query Service] tiene muchos propósitos. Puede utilizarla para dar cabida a una lógica compleja para la segmentación, para calcular varios atributos personalizados para usarlos en fases posteriores o para simplificar en gran medida la forma de crear los segmentos.

[!DNL Query Service] permite incluir restricciones en las consultas para simplificar el proceso de creación de segmentos. Esto mejora la calidad de los datos al garantizar que los datos adecuados cumplen los requisitos de sus segmentos y crea audiencias más precisas. Mantener la calidad de la consulta resulta en una audiencia precisa y ayuda con la fiabilidad de los datos. También puede guardar la audiencia creando esquemas y tablas personalizadas basadas en atributos derivados de la consulta. Se puede habilitar una tabla personalizada para el perfil y puede utilizar estos puntos de datos para la segmentación y personalización. Esta función ayuda a los especialistas en marketing que desean crear una audiencia nítida de personas.

Además, al incluir en la consulta lógica que cumpla cualquier condición recurrente o estática, [!DNL Query Service] extrae la carga de una segmentación detallada.

Adobe Experience Platform proporciona un repositorio de datos y las herramientas necesarias para activar los datos de una manera eficiente y fiable. Al mantener los datos dentro de Platform, le permite derivar atributos mientras ejecuta otros procesos y elimina la necesidad de exportar datos a herramientas de terceros para su manipulación y procesamiento. Estos gastos generales de procesamiento pueden afectar en gran medida a la cronología de un proyecto al tratar con cientos de atributos o campañas. Esto proporciona a los especialistas en marketing una ubicación única para acceder a sus datos y crear campañas, así como un medio muy dinámico de segmentar y personalizar sus mensajes.

## Pasos siguientes

Al leer este documento, debería saber cómo [!DNL Query Service] afecta no solo a la calidad de los datos y a la facilidad de segmentación, sino también a su importancia dentro de la arquitectura de datos para todo el flujo de trabajo de extremo a extremo. Para ver ejemplos de SQL más aplicables que utilicen Adobe Analytics con [!DNL Query Service], consulte la [Caso de uso de variables de comercialización Adobe Analytics](./merchandising-variables.md).

Otros documentos que demuestran los beneficios de [!DNL Query Service] para conocer las perspectivas empresariales estratégicas de su organización, consulte [caso de uso de filtrado de bots](./bot-filtering.md) ejemplo.

Alternativamente, estos documentos pueden beneficiar a su comprensión de [!DNL Query Service] características:

* [Directrices para la ejecución de consultas](../best-practices/writing-queries.md)
* [Directrices para la organización de recursos de datos](../best-practices/organize-data-assets.md).


