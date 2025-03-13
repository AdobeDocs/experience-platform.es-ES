---
keywords: Experience Platform;solución de problemas;protecciones;directrices;
title: Protecciones para la ingesta de datos
description: Obtenga información sobre las protecciones para la ingesta de datos en Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: a862e532382472eadf29aee2568c550b1a71211a
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Protecciones para la ingesta de datos

>[!IMPORTANT]
>
>Las protecciones para la ingesta por lotes y de flujo continuo se calculan generalmente a nivel de organización y no de zona protegida. Esto significa que el uso de datos por zona protegida está enlazado al derecho de uso de licencias total que corresponde con toda la organización. Además, el uso de datos en entornos limitados de desarrollo está limitado al 10 % del total de perfiles. Para obtener más información acerca del derecho de uso de licencias, lea la [guía de prácticas recomendadas de administración de datos](../landing/license-usage-and-guardrails/data-management-best-practices.md).

Las protecciones son umbrales que proporcionan directrices para el uso de datos y sistemas, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform. Las protecciones pueden hacer referencia al uso o consumo de datos y al procesamiento en relación con los derechos de licencia.

>[!IMPORTANT]
>
>Compruebe sus derechos de licencia en su pedido de ventas y la [descripción del producto](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) correspondiente sobre los límites de uso reales, además de esta página de protecciones.

Este documento proporciona instrucciones sobre las protecciones para la ingesta de datos en Adobe Experience Platform.

## Protecciones para la ingesta por lotes

En la tabla siguiente se describen las protecciones que se deben tener en cuenta al usar la [API de ingesta por lotes](./batch-ingestion/overview.md) o las fuentes:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Ingesta del lago de datos mediante la API de ingesta por lotes | <ul><li>Puede ingerir hasta 20 GB de datos por hora en el lago de datos mediante la API de ingesta por lotes.</li><li>El número máximo de archivos por lote es de 1500.</li><li>El tamaño máximo de lote es de 100 GB.</li><li>Se 10000 el número máximo de propiedades o campos por fila.</li><li>El número máximo de lotes por minuto por usuario es de 2000.</li></ul> | |
| Ingesta del lago de datos mediante fuentes por lotes | <ul><li>Puede ingerir hasta 200 GB de datos por hora en un lago de datos mediante fuentes de ingesta por lotes como [!DNL Azure Blob], [!DNL Amazon S3] y [!DNL SFTP].</li><li>Un tamaño de lote debe estar entre 256 MB y 100 GB. Esto se aplica a los datos sin comprimir y comprimidos. Cuando los datos comprimidos no están comprimidos en el lago de datos, se aplicarán estas limitaciones.</li><li>El número máximo de archivos por lote es de 1500.</li><li>El tamaño mínimo de un archivo o carpeta es de 1 byte. No se pueden introducir archivos o carpetas con un tamaño de 0 bytes.</li></ul> | Lea la [descripción general de orígenes](../sources/home.md) para ver un catálogo de orígenes que puede usar para la ingesta de datos. |
| Ingesta por lotes en el perfil | <ul><li>El tamaño máximo de una clase de registro es 100 KB (duro).</li><li>El tamaño máximo de una clase ExperienceEvent es 10 KB (duro).</li></ul> | |
| Número de lotes de Perfil o ExperienceEvent introducidos por día | **El número máximo de lotes de Perfil o ExperienceEvent ingeridos por día es 90 por zona protegida.** Esto significa que el total combinado de lotes Profile y ExperienceEvent ingeridos cada día no puede superar los 90. La ingesta de lotes adicionales afectará al rendimiento del sistema. | Este es un límite flexible. Es posible ir más allá de un límite flexible, sin embargo, los límites flexibles proporcionan una guía recomendada para el rendimiento del sistema. Además, esta protección se establece en **por espacio aislado**, no por organización. |
| Ingesta de datos cifrados | El tamaño máximo admitido de un solo archivo cifrado es de 1 GB. Por ejemplo, aunque puede introducir datos de 2 GB o más en una sola ejecución de flujo de datos, ningún archivo individual de la ejecución de flujo de datos puede superar 1 GB. | El proceso de ingesta de datos cifrados puede llevar más tiempo que el de una ingesta de datos normal. Lea la [guía de API de ingesta de datos cifrados](../sources/tutorials/api/encrypt-data.md) para obtener más información. |
| Actualizar ingesta por lotes | La ingesta de lotes actualizados puede ser hasta 10 veces más lenta que los lotes normales; por lo tanto, debe **mantener sus lotes actualizados por debajo de los dos millones de registros** para garantizar un tiempo de ejecución eficiente y evitar que otros lotes se procesen en la zona protegida. | Aunque no cabe duda de que puede ingerir lotes que superen los dos millones de registros, el tiempo de ingesta será considerablemente mayor debido a las limitaciones de las pequeñas zonas protegidas. |

{style="table-layout:auto"}

## Protecciones para la ingesta por streaming

Lea la [descripción general de la ingesta de transmisión](./streaming-ingestion/overview.md) para obtener información sobre las protecciones para la ingesta de transmisión.

## Protecciones para fuentes de flujo continuo

La siguiente tabla describe las protecciones que se deben tener en cuenta al utilizar fuentes de flujo continuo:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Fuentes de streaming | <ul><li>El tamaño máximo de registro es 1 MB, con un tamaño recomendado de 10 KB.</li><li>Las fuentes de streaming admiten entre 4000 y 5000 solicitudes por segundo al ingerir en el lago de datos. Esto se aplica tanto a las conexiones de origen recién creadas como a las conexiones de origen existentes. **Nota**: la transmisión de datos puede tardar hasta 30 minutos en procesarse completamente en el lago de datos.</li><li>Las fuentes de streaming admiten un máximo de 1500 solicitudes por segundo al ingerir datos en un perfil o una segmentación de streaming.</li></ul> | Los orígenes de transmisión por secuencias como [!DNL Kafka], [!DNL Azure Event Hubs] y [!DNL Amazon Kinesis] no utilizan la ruta [!DNL Data Collection Core Service] (DCCS) y pueden tener límites de rendimiento diferentes. Consulte la [descripción general de orígenes](../sources/home.md) para ver un catálogo de orígenes que puede usar para la ingesta de datos. |

{style="table-layout:auto"}

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
