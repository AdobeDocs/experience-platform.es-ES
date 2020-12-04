---
keywords: Experience Platform;home;popular topics;data ingestion;data location;Data Location;Data management;data management;Lineage;lineage;batch;Batch;ingested data
solution: Experience Platform
title: Introducción a la ingestión de datos de Adobe Experience Platform
topic: overview
description: Este documento presenta las tres principales maneras en que se ingieren los datos en la Plataforma, con vínculos a la documentación de información general correspondiente para obtener información más detallada.
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 9%

---


# Información general sobre la inserción de datos

Adobe Experience Platform reúne los datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingestión de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] se ingieren datos de estas fuentes, así como la forma en que se mantienen esos datos dentro del lago de datos para su uso por parte de los servicios [!DNL Platform] descendentes.

Este documento presenta las tres formas principales en que se ingieren los datos [!DNL Platform], con vínculos a la documentación general correspondiente para obtener información más detallada.

## Ingesta por lotes

La ingestión por lotes permite ingerir datos en [!DNL Experience Platform] archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros que se han introducido correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, se deben ingerir mediante este método.

Consulte la información general [sobre la ingestión de](./batch-ingestion/overview.md) lotes para obtener más información.

## Transmisión por flujo continuo

La ingestión por flujo continuo le permite enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real. [!DNL Platform] admite el uso de entradas de datos para transmitir datos de experiencias entrantes, que se mantiene en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos se pueden configurar para autenticar automáticamente los datos que recopilan, asegurándose de que los datos procedan de una fuente de confianza.

Para obtener más información, consulte la descripción general [de la ingesta de](./streaming-ingestion/overview.md) flujo.

## Fuentes

[!DNL Experience Platform] le permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en sus fuentes de datos externas, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de ingestión.

Las conexiones de origen se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]).

See the [Sources overview](../sources/home.md) for more information.

## Próximos pasos y recursos adicionales

Este documento ofreció una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] la [!DNL Experience Platform]. Siga leyendo la documentación general de cada método de ingestión para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede complementar su aprendizaje viendo el siguiente vídeo de información general sobre la ingestión. Para obtener información sobre cómo [!DNL Experience Platform] realizar un seguimiento de los metadatos de los registros ingestados, consulte la descripción general [del servicio de](../catalog/home.md)catálogos.

>[!WARNING]
>
>El término &quot;Perfil unificado&quot; que se utiliza en el siguiente vídeo no está actualizado. Los términos [!DNL "Profile"] o [!DNL "Real-time Customer Profile"] son los términos correctos utilizados en la [!DNL Experience Platform] documentación. Consulte la documentación para obtener las últimas funciones.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)