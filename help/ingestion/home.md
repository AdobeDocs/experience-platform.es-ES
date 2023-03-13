---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;ubicación de datos;ubicación de datos;administración de datos;administración de datos;linaje;linaje;lote;lote;datos ingeridos
solution: Experience Platform
title: Información general sobre la ingesta de datos
description: Este documento presenta las tres formas principales de introducir los datos en Platform, con vínculos a su documentación general respectiva para obtener información más detallada.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---

# Resumen de ingesta de datos

Adobe Experience Platform reúne datos de varios orígenes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] ingiere datos de estas fuentes, así como la forma en que se mantienen los datos dentro del lago de datos para que los utilice el flujo descendente [!DNL Platform] servicios.

Este documento presenta las tres formas principales en que se incorporan los datos a [!DNL Platform], con vínculos a su documentación de información general correspondiente para obtener información más detallada.

## Ingesta por lotes

La ingesta por lotes le permite introducir datos en [!DNL Experience Platform] como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros que se han introducido correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como los archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, se deben introducir mediante este método.

Consulte la [introducción a la ingesta por lotes](./batch-ingestion/overview.md) para obtener más información.

## Ingesta de streaming

La introducción por transmisión le permite enviar datos de dispositivos del cliente y del lado del servidor a [!DNL Experience Platform] en tiempo real. [!DNL Platform] admite el uso de entradas de datos para transmitir datos de experiencia entrantes, que se conservan en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos se pueden configurar para autenticar automáticamente los datos que recopilan, asegurándose de que los datos provengan de una fuente de confianza.

Consulte la [información general sobre ingesta de streaming](./streaming-ingestion/overview.md) para obtener más información.

## Fuentes

[!DNL Experience Platform] permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en las fuentes de datos externas, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de la ingesta.

Las conexiones de fuente se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager) y fuentes de almacenamiento de nube de terceros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]).

Consulte la [Resumen de orígenes](../sources/home.md) para obtener más información.

## Pasos siguientes y recursos adicionales

Este documento proporciona una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] in [!DNL Experience Platform]. Continúe leyendo la documentación de información general de cada método de ingesta para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede complementar su aprendizaje viendo el siguiente vídeo de información general sobre la ingesta. Para obtener información sobre cómo [!DNL Experience Platform] realiza un seguimiento de los metadatos de los registros ingeridos; consulte la [Resumen del servicio de catálogo](../catalog/home.md).

>[!WARNING]
>
>El término &quot;perfil unificado&quot; que se utiliza en el siguiente vídeo no está actualizado. Los términos [!DNL "Profile"] o [!DNL "Real-Time Customer Profile"] son los términos correctos utilizados en [!DNL Experience Platform] documentación. Consulte la documentación para obtener la funcionalidad más reciente.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
