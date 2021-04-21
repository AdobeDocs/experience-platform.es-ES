---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;ubicación de datos;ubicación de datos;gestión de datos;gestión de datos;linaje;lote;lote;datos ingestados
solution: Experience Platform
title: Información general sobre la incorporación de datos
topic-legacy: overview
description: Este documento presenta las tres maneras principales en que se introducen los datos en Platform, con vínculos a su respectiva documentación general para obtener información más detallada.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 14%

---

# Información general sobre la ingesta de datos

Adobe Experience Platform reúne datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] ingesta datos de estas fuentes, así como el modo en que se mantienen esos datos dentro del lago de datos para su uso por parte de los servicios [!DNL Platform] descendentes.

Este documento presenta las tres maneras principales en que se introducen los datos en [!DNL Platform], con vínculos a su respectiva documentación general para obtener información más detallada.

## Ingesta por lotes

La ingesta por lotes permite introducir datos en [!DNL Experience Platform] como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros que se han introducido correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, deben ingerirse mediante este método.

Consulte la [información general sobre la ingesta por lotes](./batch-ingestion/overview.md) para obtener más información.

## Ingesta de la transmisión

La introducción por transmisión le permite enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real. [!DNL Platform] admite el uso de entradas de datos para transmitir datos de experiencias entrantes, que se mantiene en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos pueden configurarse para autenticar automáticamente los datos que recopilan, asegurándose de que los datos provengan de una fuente de confianza.

Consulte la [descripción general de la ingesta de flujo](./streaming-ingestion/overview.md) para obtener más información.

## Fuentes

[!DNL Experience Platform] permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en sus fuentes de datos externas, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta.

Las conexiones de origen se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]).

Consulte la [Información general sobre fuentes](../sources/home.md) para obtener más información.

## Pasos siguientes y recursos adicionales

Este documento ofrece una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] en [!DNL Experience Platform]. Siga leyendo la documentación general de cada método de ingesta para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede complementar su aprendizaje viendo el siguiente vídeo de información general sobre la ingesta. Para obtener información sobre cómo [!DNL Experience Platform] rastrea los metadatos de los registros ingestados, consulte la [Información general del Servicio de catálogo](../catalog/home.md).

>[!WARNING]
>
>El término &quot;Perfil unificado&quot; que se utiliza en el siguiente vídeo está desactualizado. Los términos [!DNL "Profile"] o [!DNL "Real-time Customer Profile"] son los términos correctos utilizados en la documentación de [!DNL Experience Platform]. Consulte la documentación para conocer las últimas funciones.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
