---
keywords: Experience Platform;solución de problemas;protecciones;directrices;
title: Protecciones para la ingesta de datos
description: Este documento proporciona instrucciones sobre protecciones para la ingesta de datos en Adobe Experience Platform
source-git-commit: 3f558c9c11945cc9af51c42f7ed872101521259f
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---

# Protecciones para la ingesta de datos

Las protecciones son umbrales que proporcionan directrices para el uso de los datos y del sistema, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform. Las protecciones pueden referirse a su uso o consumo de datos y procesamiento en relación con sus derechos de licencia.

Este documento proporciona instrucciones sobre protecciones para la ingesta de datos en Adobe Experience Platform.

## Protecciones para la ingesta de lotes

La tabla siguiente describe las barreras que se deben tener en cuenta al usar la variable [API de ingesta por lotes](./batch-ingestion/overview.md) o fuentes:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Ingesta de lago de datos mediante la API de ingesta de lotes | <ul><li>Puede ingerir hasta 20 GB de datos por hora en el lago de datos mediante la API de ingesta por lotes.</li><li>El número máximo de archivos por lote es de 1500.</li><li>El tamaño máximo del lote es de 100 GB.</li><li>El número máximo de propiedades o campos por fila es 10 000.</li><li>El número máximo de lotes por minuto, por usuario, es de 138.</li></ul> |
| Ingesta de lago de datos mediante fuentes por lotes | <ul><li>Puede ingerir hasta 200 GB de datos por hora en el lago de datos mediante fuentes de ingesta por lotes como [!DNL Azure Blob], [!DNL Amazon S3]y [!DNL SFTP].</li><li>Un tamaño de lote debe estar entre 256 MB y 100 GB.</li><li>El número máximo de archivos por lote es de 1500.</li></ul> | Consulte la [información general sobre fuentes](../sources/home.md) para un catálogo de fuentes, puede utilizar para la ingesta de datos. |
| Ingesta por lotes al perfil | <ul><li>Puede ingerir hasta 120 GB de datos por hora.</li><li>El tamaño máximo de una clase de registro es de 100 KB (suave).</li><li>El tamaño máximo de una clase ExperienceEvent es de 10 KB (suave).</li><li>El tamaño máximo de un registro único es de 1 MB.</li></ul> |

## Protecciones para la transmisión por secuencias

La tabla siguiente describe las barreras que se deben tener en cuenta al usar la variable [API de ingesta de transmisión](./streaming-ingestion/overview.md) o fuentes de flujo continuo:

| Tipo de ingesta | Directrices | Notas |
| --- | --- | --- |
| Ingesta de la transmisión | <ul><li>El tamaño máximo del registro es 1 MB, siendo el tamaño recomendado 10 KB.</li><li>Puede procesar 20 000 solicitudes por segundo en Perfil en menos de un minuto.</li><li>Puede procesar hasta 20 000 solicitudes por segundo a laca de datos en menos de 15 minutos.</li></ul> | Utilice la API de ingesta por lotes si necesita un mayor rendimiento de los datos. |
| Fuentes de transmisión | <ul><li>El tamaño máximo del registro es 1 MB, siendo el tamaño recomendado 10 KB.</li><li>Las fuentes de transmisión admiten entre 4000 y 5000 solicitudes por segundo tras la creación de una nueva conexión de origen.</li><li>Se pueden procesar entre 4000 y 5000 solicitudes por segundo en el lago de datos.</li></ul> | Fuentes de transmisión como [!DNL Kafka], [!DNL Azure Event Hubs]y [!DNL Amazon Kinesis] no use el [!DNL Data Collection Core Service] (DCCS) y puede tener diferentes límites de rendimiento. Consulte la [información general sobre fuentes](../sources/home.md) para un catálogo de fuentes, puede utilizar para la ingesta de datos. |

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre los datos y las protecciones de procesamiento en el Experience Platform:

* [Protecciones para datos de Perfil del cliente en tiempo real](../profile/guardrails.md)
* [Protecciones para los datos del servicio de identidad](../identity-service/guardrails.md)