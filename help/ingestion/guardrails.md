---
keywords: Experience Platform;solución de problemas;protecciones;directrices;
title: Protecciones para la ingesta de datos
description: Obtenga información sobre las protecciones para la ingesta de datos en Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: cdc5bb01ef6de8134c6ad4ef6601a748571bf86f
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Protecciones para la ingesta de datos

>[!IMPORTANT]
>
>Las protecciones para la ingesta por lotes y de flujo continuo se calculan en el nivel de organización y no en el de zona protegida. Esto significa que el uso de datos por zona protegida está enlazado al derecho de uso de licencias total que corresponde con toda la organización. Además, el uso de datos en entornos limitados de desarrollo está limitado al 10 % del total de perfiles. Para obtener más información sobre el derecho de uso de licencias, lea la [guía de prácticas recomendadas de administración de datos](../landing/license-usage-and-guardrails/data-management-best-practices.md).

Las protecciones son umbrales que proporcionan directrices para el uso de datos y sistemas, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform. Las protecciones pueden hacer referencia al uso o consumo de datos y al procesamiento en relación con los derechos de licencia.

Este documento proporciona instrucciones sobre las protecciones para la ingesta de datos en Adobe Experience Platform.

## Protecciones para la ingesta por lotes

En la tabla siguiente se describen las protecciones que deben tenerse en cuenta al utilizar [API de ingesta por lotes](./batch-ingestion/overview.md) o fuentes:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Ingesta del lago de datos mediante la API de ingesta por lotes | <ul><li>Puede ingerir hasta 20 GB de datos por hora en el lago de datos mediante la API de ingesta por lotes.</li><li>El número máximo de archivos por lote es de 1500.</li><li>El tamaño máximo de lote es de 100 GB.</li><li>Se 10000 el número máximo de propiedades o campos por fila.</li><li>El número máximo de lotes por minuto por usuario es de 138.</li></ul> | |
| Ingesta del lago de datos mediante fuentes por lotes | <ul><li>Puede ingerir hasta 200 GB de datos por hora en un lago de datos mediante fuentes de ingesta por lotes como [!DNL Azure Blob], [!DNL Amazon S3], y [!DNL SFTP].</li><li>Un tamaño de lote debe estar entre 256 MB y 100 GB. Esto se aplica a los datos sin comprimir y comprimidos. Cuando los datos comprimidos no están comprimidos en el lago de datos, se aplicarán estas limitaciones.</li><li>El número máximo de archivos por lote es de 1500.</li><li>El tamaño mínimo de un archivo o carpeta es de 1 byte. No se pueden introducir archivos o carpetas con un tamaño de 0 bytes.</li></ul> | Lea el [información general de orígenes](../sources/home.md) para un catálogo de fuentes que puede utilizar para la ingesta de datos. |
| Ingesta por lotes en el perfil | <ul><li>El tamaño máximo de una clase de registro es 100 KB (duro).</li><li>El tamaño máximo de una clase ExperienceEvent es 10 KB (duro).</li></ul> | |
| Número de lotes de Perfil o ExperienceEvent introducidos por día | **El número máximo de lotes de Perfil o ExperienceEvent ingeridos por día es de 90.** Esto significa que el total combinado de lotes Profile y ExperienceEvent introducidos cada día no puede superar los 90. La ingesta de lotes adicionales afectará al rendimiento del sistema. | Este es un límite flexible. Es posible ir más allá de un límite flexible, sin embargo, los límites flexibles proporcionan una guía recomendada para el rendimiento del sistema. |

## Protecciones para la ingesta por streaming

Lea el [información general sobre ingesta de streaming](./streaming-ingestion/overview.md) para obtener información sobre las protecciones para la ingesta de transmisión.

## Protecciones para fuentes de flujo continuo

La siguiente tabla describe las protecciones que se deben tener en cuenta al utilizar fuentes de flujo continuo:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Fuentes de streaming | <ul><li>El tamaño máximo de registro es 1 MB, con un tamaño recomendado de 10 KB.</li><li>Las fuentes de streaming admiten entre 4000 y 5000 solicitudes por segundo al ingerir en el lago de datos. Esto se aplica tanto a las conexiones de origen recién creadas como a las conexiones de origen existentes. **Nota**: Puede tardar hasta 30 minutos en que los datos de flujo se procesen completamente en el lago de datos.</li><li>Las fuentes de streaming admiten un máximo de 1500 solicitudes por segundo al ingerir datos en un perfil o una segmentación de streaming.</li></ul> | Fuentes de streaming como [!DNL Kafka], [!DNL Azure Event Hubs], y [!DNL Amazon Kinesis] no utilice el [!DNL Data Collection Core Service] (DCCS) y pueden tener límites de rendimiento diferentes. Consulte la [información general de orígenes](../sources/home.md) para un catálogo de fuentes que puede utilizar para la ingesta de datos. |

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-time Customer Data Platform (edición B2C - paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P: paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (Paquetes B2B Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
