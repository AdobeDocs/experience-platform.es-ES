---
keywords: Experience Platform;solución de problemas;protecciones;directrices;
title: Protecciones para la ingesta de datos
description: Este documento proporciona instrucciones sobre las protecciones para la ingesta de datos en Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 582f6ffdea6fa1978f6af6f0f0f92e50a12f6200
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---

# Protecciones para la ingesta de datos

Las protecciones son umbrales que proporcionan directrices para el uso de datos y sistemas, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform. Las protecciones pueden hacer referencia al uso o consumo de datos y al procesamiento en relación con los derechos de licencia.

Este documento proporciona instrucciones sobre las protecciones para la ingesta de datos en Adobe Experience Platform.

## Protecciones para la ingesta por lotes

En la tabla siguiente se describen las protecciones que deben tenerse en cuenta al utilizar [API de ingesta por lotes](./batch-ingestion/overview.md) o fuentes:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Ingesta del lago de datos mediante la API de ingesta por lotes | <ul><li>Puede ingerir hasta 20 GB de datos por hora en el lago de datos mediante la API de ingesta por lotes.</li><li>El número máximo de archivos por lote es de 1500.</li><li>El tamaño máximo de lote es de 100 GB.</li><li>Se 10000 el número máximo de propiedades o campos por fila.</li><li>El número máximo de lotes por minuto por usuario es de 138.</li></ul> |
| Ingesta del lago de datos mediante fuentes por lotes | <ul><li>Puede ingerir hasta 200 GB de datos por hora en un lago de datos mediante fuentes de ingesta por lotes como [!DNL Azure Blob], [!DNL Amazon S3], y [!DNL SFTP].</li><li>Un tamaño de lote debe estar entre 256 MB y 100 GB.</li><li>El número máximo de archivos por lote es de 1500.</li></ul> | Consulte la [información general de orígenes](../sources/home.md) para un catálogo de fuentes que puede utilizar para la ingesta de datos. |
| Ingesta por lotes en el perfil | <ul><li>El tamaño máximo de una clase de registro es 100 KB (en blanco).</li><li>El tamaño máximo de una clase ExperienceEvent es 10 KB (flexible).</li><li>El tamaño máximo de un único registro es 1 MB.</li></ul> |
| Número de lotes de Perfil o ExperienceEvent introducidos por día | **El número máximo de lotes de Perfil o ExperienceEvent ingeridos por día es de 90.** Esto significa que el total combinado de lotes Profile y ExperienceEvent introducidos cada día no puede superar los 90. La ingesta de lotes adicionales afectará al rendimiento del sistema. | Este es un límite flexible. Es posible ir más allá de un límite flexible, sin embargo, los límites flexibles proporcionan una guía recomendada para el rendimiento del sistema. |

## Protecciones para la ingesta por streaming

En la tabla siguiente se describen las protecciones que deben tenerse en cuenta al utilizar [API de ingesta de streaming](./streaming-ingestion/overview.md) o fuentes de flujo continuo:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Ingesta de streaming | <ul><li>El tamaño máximo de registro es 1 MB, con un tamaño recomendado de 10 KB.</li><li>Puede procesar hasta 2500 solicitudes por segundo en el Perfil.</li><li>Puede procesar hasta 20000 solicitudes por segundo al lago de datos en menos de 15 minutos.</li></ul> | Utilice la API de ingesta por lotes si necesita un mayor rendimiento de datos. |
| Fuentes de streaming | <ul><li>El tamaño máximo de registro es 1 MB, con un tamaño recomendado de 10 KB.</li><li>Las fuentes de streaming admiten entre 4000 y 5000 solicitudes por segundo al crear una nueva conexión de origen. **Nota**: Puede tardar hasta 30 minutos en que los datos de flujo se procesen completamente en el lago de datos.</li><li>Puede procesar entre 4000 y 5000 solicitudes por segundo al lago de datos. **Nota**: Puede tardar hasta 30 minutos en que los datos de flujo se procesen completamente en el lago de datos.</li></ul> | Fuentes de streaming como [!DNL Kafka], [!DNL Azure Event Hubs], y [!DNL Amazon Kinesis] no utilice el [!DNL Data Collection Core Service] (DCCS) y pueden tener límites de rendimiento diferentes. Consulte la [información general de orígenes](../sources/home.md) para un catálogo de fuentes que puede utilizar para la ingesta de datos. |

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre los datos y las protecciones de procesamiento en Experience Platform:

* [Protecciones para datos del perfil del cliente en tiempo real](../profile/guardrails.md)
* [Protecciones para los datos del servicio de identidad](../identity-service/guardrails.md)
