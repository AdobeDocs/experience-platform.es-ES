---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;ubicación de datos;ubicación de datos;gestión de datos;gestión de datos;linaje;lote;lote;datos ingestados
solution: Experience Platform
title: Información general sobre la incorporación de datos
topic-legacy: overview
description: Este documento presenta las tres maneras principales en que se introducen los datos en Platform, con vínculos a su respectiva documentación general para obtener información más detallada.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 14%

---

# Información general sobre la ingesta de datos

Adobe Experience Platform reúne datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] Ingesta datos de estas fuentes, así como la forma en que se mantienen esos datos dentro del lago de datos para su uso descendente [!DNL Platform] servicios.

Este documento presenta las tres maneras principales en que se introducen los datos [!DNL Platform], con vínculos a su respectiva documentación general para obtener información más detallada.

## Ingesta por lotes

La ingesta por lotes le permite introducir datos en [!DNL Experience Platform] como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros que se han introducido correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, deben ingerirse mediante este método.

Consulte la [información general sobre la ingesta de lotes](./batch-ingestion/overview.md) para obtener más información.

## Ingesta de la transmisión

La introducción por transmisión le permite enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real. [!DNL Platform] admite el uso de entradas de datos para transmitir datos de experiencias entrantes, que se mantiene en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos pueden configurarse para autenticar automáticamente los datos que recopilan, asegurándose de que los datos provengan de una fuente de confianza.

Consulte la [información general sobre la ingesta de transmisión](./streaming-ingestion/overview.md) para obtener más información.

## Fuentes

[!DNL Experience Platform] permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en sus fuentes de datos externas, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta.

Las conexiones de origen se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]).

Consulte la [Resumen de fuentes](../sources/home.md) para obtener más información.

## Pasos siguientes y recursos adicionales

Este documento contiene una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] en [!DNL Experience Platform]. Siga leyendo la documentación general de cada método de ingesta para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede complementar su aprendizaje viendo el siguiente vídeo de información general sobre la ingesta. Para obtener información sobre cómo [!DNL Experience Platform] rastrea los metadatos de registros ingestados; consulte la [Información general del servicio de catálogo](../catalog/home.md).

>[!WARNING]
>
>El término &quot;Perfil unificado&quot; que se utiliza en el siguiente vídeo está desactualizado. Los términos [!DNL "Profile"] o [!DNL "Real-Time Customer Profile"] son los términos correctos utilizados en la variable [!DNL Experience Platform] documentación. Consulte la documentación para conocer las últimas funciones.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
