---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre la introducción de datos de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Información general sobre la inserción de datos

Adobe Experience Platform aúna los datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingestión de datos de la plataforma de experiencia de Adobe representa los múltiples métodos mediante los cuales la plataforma ingesta datos de estas fuentes, así como la forma en que se mantienen los datos dentro del lago de datos para su uso por los servicios de plataforma descendente.

Este documento presenta las tres principales maneras en que se ingieren los datos en la Plataforma, con vínculos a la documentación de información general correspondiente para obtener información más detallada.

## Ingesta por lotes

La ingestión por lotes permite ingerir datos en la plataforma de experiencias como archivos por lotes. Los lotes son unidades de datos que consisten en uno o más archivos que se van a ingerir como una sola unidad. Una vez ingeridos, los lotes proporcionan metadatos que describen el número de registros que se han ingestado correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, se deben ingerir mediante este método.

Consulte la información general [sobre la ingestión de](./batch-ingestion/overview.md) lotes para obtener más información.

## Transmisión por flujo continuo

La ingestión de flujo continuo le permite enviar datos desde dispositivos del lado del cliente y del servidor a la plataforma de experiencias en tiempo real. La plataforma admite el uso de entradas de datos para transmitir los datos de experiencia entrantes, que se mantienen en conjuntos de datos con transmisión habilitada dentro del lago de datos. Las entradas de datos se pueden configurar para autenticar automáticamente los datos que recopilan, asegurándose de que los datos procedan de una fuente de confianza.

Para obtener más información, consulte la descripción general [de la ingesta de](./streaming-ingestion/overview.md) flujo.

## Fuentes

La plataforma de experiencia le permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en sus fuentes de datos externas, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de ingestión.

Las conexiones de origen se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audiencia Manager), fuentes de almacenamiento en la nube de terceros (como Azure Blob, Amazon S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como Microsoft Dynamics y Salesforce).

Consulte la descripción general [de](../source-connectors/home.md) Fuentes para obtener más información.

## Pasos siguientes

Este documento proporcionó una breve introducción a los diferentes aspectos de la ingestión de datos en la plataforma de experiencia. Siga leyendo la documentación general de cada método de ingestión para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. Para obtener información sobre cómo rastrea la plataforma de experiencias los metadatos de los registros ingestados, consulte la descripción general [del servicio de](../catalog/home.md)catálogos.