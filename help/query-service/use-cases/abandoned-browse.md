---
keywords: Experience Platform;servicio de consulta;servicio de consulta;consulta
title: Caso de uso de ejemplo para el servicio de consulta de Adobe Experience Platform
topic-legacy: tutorial
description: Un ejemplo completo para demostrar la versatilidad y las ventajas del servicio de consulta de Adobe Experience Platform.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 6f6256b5601ce5c230ef334a9ce71325b43fda45
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Ejemplo de caso de uso para Adobe Experience Platform [!DNL Query Service]

Este documento y la presentación de vídeo adjunta proporcionan un flujo de trabajo completo que muestra cómo Adobe Experience Platform [!DNL Query Service] beneficia las perspectivas empresariales estratégicas de su organización. Con un caso de uso de abandono de exploración como ejemplo, esta guía ilustra los siguientes conceptos clave:

* La importancia clave del procesamiento de datos para maximizar el potencial de Adobe Experience Platform.
* Formas de crear la consulta en función de la arquitectura de datos existente.
* Garantizar la calidad de los datos que satisfaga sus necesidades y métodos para mitigar cualquier déficit.
* Proceso para programar una consulta para que se ejecute con una frecuencia establecida para su uso descendente en segmentación y destinos para personalización.
* La facilidad con la que los especialistas en marketing incluyen atributos derivados en sus segmentos a través del poder de [!DNL Query Service].

## Objetivos {#objectives}

Esta demostración de flujo de trabajo se basa en varios servicios de Adobe Experience Platform. Si desea continuar, se recomienda comprender bien las siguientes funciones y servicios:

* La variable [conceptos básicos de la composición de esquema del Modelo de datos de experiencia (XDM)](../../xdm/schema/composition.md)
* Cómo [crear conjuntos de datos e ingerir datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es)
* Cómo [ingesta de datos mediante el conector de origen de Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=es)
* [Segmentación](../../segmentation/home.md)
* [Destinos](../../destinations/home.md)

El ejemplo de abandono de exploración se centra en el uso del Adobe [!DNL Analytics] datos para crear una audiencia procesable concreta. La audiencia se refina para incluir a todos los clientes que han explorado el sitio web en los últimos cuatro días pero no han realizado una compra. A continuación, cada perfil de la audiencia se segmenta con el SKU de precio más alto que resulta del patrón de comportamiento del cliente.

La consulta en sí es muy prescriptiva y solo incluye datos que cumplan los criterios de caso de uso para la definición del segmento. Esto mejora el rendimiento al minimizar la cantidad de [!DNL Analytics] datos que se están procesando. También ordena los datos por precio de más alto a más bajo y elige el SKU de mayor precio que estaba explorando el usuario.

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

La presentación de vídeo que se muestra a continuación ofrece un caso de uso holístico y real para sus datos de Experience Platform centrados en [!DNL Query Service] e integraciones de análisis de Adobe.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Ventajas de [!DNL Query Service] {#benefits}

Las funciones proporcionadas por [!DNL Query Service] sirve para muchos fines. Puede utilizarlo para dar cabida a la lógica compleja de la segmentación, para calcular varios atributos personalizados para utilizarlos de forma descendente o para simplificar en gran medida la forma en que genera sus segmentos.

[!DNL Query Service] le permite incluir restricciones en sus consultas para simplificar el proceso de creación de segmentos. Esto mejora la calidad de los datos al garantizar que los datos adecuados se califiquen para los segmentos y crea audiencias más precisas. Mantener la calidad de la consulta resulta en una audiencia precisa y ayuda con la fiabilidad de los datos. También puede guardar la audiencia creando esquemas y tablas personalizadas basadas en atributos derivados de la consulta. Se puede habilitar una tabla personalizada para Perfil y se pueden usar estos puntos de datos para la segmentación y personalización. Esta función ayuda a los especialistas en marketing que desean crear una audiencia clara de personas.

Además, al incluir en la consulta lógica que cumpla cualquier condición recurrente o estática, [!DNL Query Service] extrae la carga de la segmentación detallada.

Adobe Experience Platform proporciona un repositorio de datos y las herramientas necesarias para activar los datos de una manera eficiente y fiable. Al mantener los datos dentro de Platform, le permite derivar atributos mientras ejecuta otros procesos y elimina la necesidad de exportar datos a herramientas de terceros para la manipulación y el procesamiento. Estos gastos generales de procesamiento pueden afectar en gran medida a la cronología de un proyecto cuando se trata de cientos de atributos o campañas. Esto proporciona a los especialistas en marketing una sola ubicación para acceder a sus datos y crear campañas, así como un medio muy dinámico de segmentar y personalizar sus mensajes.

## Pasos siguientes

Al leer este documento, ahora debe comprender cómo [!DNL Query Service] afecta no solo a la calidad de sus datos y a la facilidad de segmentación, sino también a su importancia dentro de la arquitectura de datos para todo el flujo de trabajo de principio a fin. Para ejemplos SQL más aplicables, utilice Adobe Analytics con [!DNL Query Service], consulte la [Documentación de consultas de ejemplo de Adobe Analytics](../sample-queries/adobe-analytics.md).

Otros documentos que demuestren los beneficios de [!DNL Query Service] a la información estratégica comercial de su organización, se incluye la variable [caso de uso de filtrado de bots](./bot-filtering.md) ejemplo.

Alternativamente, estos documentos le ayudarán a comprender [!DNL Query Service] características:

* [Directrices para la ejecución de consultas](../best-practices/writing-queries.md)
* [Directrices para la organización de recursos de datos](../best-practices/organize-data-assets.md).


