---
keywords: Experience Platform;inicio;temas populares;ingestión de datos;ubicación de datos;Ubicación de datos;Gestión de datos;gestión de datos;Linaje;linaje;lote;lote;datos ingestados
solution: Experience Platform
title: Información general sobre la inserción de datos
topic: overview
description: Este documento presenta las tres principales maneras en que se ingieren los datos en la Plataforma, con vínculos a la documentación de información general correspondiente para obtener información más detallada.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 14%

---


# Información general sobre la inserción de datos

Adobe Experience Platform reúne datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingestión de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] ingesta datos de estas fuentes, así como la forma en que se mantienen esos datos dentro del lago de datos para su uso por los servicios [!DNL Platform] descendentes.

Este documento presenta las tres maneras principales en que se ingieren los datos en [!DNL Platform], con vínculos a la documentación de información general correspondiente para obtener información más detallada.

## Ingesta por lotes

La ingestión por lotes permite ingerir datos en [!DNL Experience Platform] como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros que se han introducido correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, se deben ingerir mediante este método.

Consulte la [información general de ingestión por lotes](./batch-ingestion/overview.md) para obtener más información.

## Ingesta de la transmisión

La ingestión por flujo continuo le permite enviar datos desde dispositivos del cliente y del servidor a [!DNL Experience Platform] en tiempo real. [!DNL Platform] admite el uso de entradas de datos para transmitir datos de experiencias entrantes, que se mantiene en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos se pueden configurar para autenticar automáticamente los datos que recopilan, asegurándose de que los datos procedan de una fuente de confianza.

Consulte la [descripción general de la ingestión de flujo](./streaming-ingestion/overview.md) para obtener más información.

## Fuentes

[!DNL Experience Platform] le permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en sus fuentes de datos externas, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de ingestión.

Las conexiones de origen se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]).

Consulte la [información general de las fuentes](../sources/home.md) para obtener más información.

## Próximos pasos y recursos adicionales

Este documento proporcionó una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] en [!DNL Experience Platform]. Siga leyendo la documentación general de cada método de ingestión para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede complementar su aprendizaje viendo el siguiente vídeo de información general sobre la ingestión. Para obtener información sobre cómo [!DNL Experience Platform] rastrea los metadatos de los registros ingestados, consulte la [información general del servicio de catálogos](../catalog/home.md).

>[!WARNING]
>
>El término &quot;Perfil unificado&quot; que se utiliza en el siguiente vídeo no está actualizado. Los términos [!DNL "Profile"] o [!DNL "Real-time Customer Profile"] son los términos correctos utilizados en la documentación de [!DNL Experience Platform]. Consulte la documentación para obtener las últimas funciones.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)