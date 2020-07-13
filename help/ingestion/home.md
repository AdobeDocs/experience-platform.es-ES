---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introducción a la ingestión de datos de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---


# Información general sobre la inserción de datos

Adobe Experience Platform reúne los datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingestión de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] se ingieren datos de estas fuentes, así como la forma en que se conservan esos datos dentro del Data Lake para que los [!DNL Platform] servicios posteriores los utilicen.

Este documento presenta las tres principales maneras en que se ingieren los datos [!DNL Platform], con vínculos a su respectiva documentación general para obtener información más detallada.

## Ingesta por lotes

La ingestión por lotes permite ingerir datos en [!DNL Experience Platform] archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros que se han introducido correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, se deben ingerir mediante este método.

Consulte la información general [sobre la ingestión de](./batch-ingestion/overview.md) lotes para obtener más información.

## Transmisión por flujo continuo

La ingestión por flujo continuo le permite enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real. [!DNL Platform] admite el uso de entradas de datos para transmitir datos de experiencias entrantes, que se mantiene en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos se pueden configurar para autenticar automáticamente los datos que recopilan, asegurándose de que los datos procedan de una fuente de confianza.

Para obtener más información, consulte la descripción general [de la ingesta de](./streaming-ingestion/overview.md) flujo.

## Fuentes

[!DNL Experience Platform] le permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en sus fuentes de datos externas, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de ingestión.

Las conexiones de origen se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como Microsoft Dynamics y Salesforce).

Consulte la descripción general [de](../sources/home.md) Fuentes para obtener más información.

## Próximos pasos y recursos adicionales

Este documento ofreció una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] la [!DNL Experience Platform]. Siga leyendo la documentación general de cada método de ingestión para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede proporcionar su aprendizaje mediante el siguiente vídeo de información general sobre la ingestión. Para obtener información sobre cómo [!DNL Experience Platform] realizar un seguimiento de los metadatos de los registros ingestados, consulte la descripción general [del servicio de](../catalog/home.md)catálogos.

>[!WARNING]
>
> El término &quot;Perfil unificado&quot; que se utiliza en el siguiente vídeo no está actualizado. Los términos [!DNL "Profile"] o [!DNL "Real-time Customer Profile"] son los términos correctos utilizados en la [!DNL Experience Platform] documentación. Consulte la documentación para obtener las últimas funciones.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)