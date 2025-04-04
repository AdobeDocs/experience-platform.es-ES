---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;ubicación de datos;ubicación de datos;administración de datos;administración de datos;linaje;linaje;lote;lotes;datos ingeridos
solution: Experience Platform
title: Resumen de ingesta de datos
description: Este documento presenta las tres formas principales de introducir los datos en Experience Platform, con vínculos a su documentación general respectiva para obtener información más detallada.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Resumen de ingesta de datos

Adobe Experience Platform reúne datos de varias fuentes para ayudar a los especialistas en marketing a comprender mejor el comportamiento de sus clientes. La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales Experience Platform ingiere datos de estas fuentes, así como la forma en que se mantienen los datos dentro del lago de datos para que los utilicen los servicios de Experience Platform descendentes.

Este documento presenta las tres formas principales de introducir los datos en Experience Platform, con vínculos a su documentación general respectiva para obtener información más detallada.

## Ingesta por lotes

La ingesta por lotes le permite ingerir datos en [!DNL Experience Platform] como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Una vez introducidos, los lotes proporcionan metadatos que describen el número de registros introducidos correctamente, así como los registros con errores y los mensajes de error asociados.

Los archivos de datos cargados manualmente, como los archivos CSV planos (asignados a esquemas XDM) y marcos de datos de parquet, se deben introducir mediante este método.

Consulte la [descripción general de la ingesta por lotes](./batch-ingestion/overview.md) para obtener más información.

>[!TIP]
>
>Utilice JSON de una sola línea en lugar de JSON de varias líneas como entrada para la ingesta por lotes. El JSON de una sola línea ofrece un mejor rendimiento, ya que el sistema puede dividir un archivo de entrada en varios fragmentos y procesarlos en paralelo, mientras que el JSON de varias líneas no se puede dividir. Esto puede reducir significativamente los costes de procesamiento de datos y mejorar la latencia de procesamiento por lotes.

## Ingesta por streaming

La introducción por transmisión le permite enviar datos desde dispositivos del cliente y del lado del servidor a [!DNL Experience Platform] en tiempo real. Experience Platform admite el uso de entradas de datos para transmitir datos de experiencia entrantes, que persisten en conjuntos de datos habilitados para flujo continuo dentro del lago de datos. Las entradas de datos se pueden configurar para autenticar automáticamente los datos que recopilan, asegurándose de que los datos provengan de una fuente de confianza.

Consulte la [descripción general de la ingesta de transmisión](./streaming-ingestion/overview.md) para obtener más información.

## Fuentes

[!DNL Experience Platform] le permite configurar conexiones de origen a varios proveedores de datos. Estas conexiones le permiten autenticarse en las fuentes de datos externas, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de la ingesta.

Las conexiones de Source se pueden configurar para recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon] S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]).

Consulte [Resumen de orígenes](../sources/home.md) para obtener más información.

### Creación de esquemas asistidos por ML {#ml-assisted-schema-creation}

Para integrar rápidamente nuevas fuentes de datos, ahora puede utilizar algoritmos de aprendizaje automático para generar un esquema a partir de datos de ejemplo. Esta automatización simplifica la creación de esquemas precisos, reduce los errores y acelera el proceso desde la recopilación de datos hasta el análisis y las perspectivas.

Consulte la [guía de creación de esquemas asistidos por ML](../xdm/ui/ml-assisted-schema-creation.md) para obtener más información sobre este flujo de trabajo.

## Pasos siguientes y recursos adicionales

Este documento proporciona una breve introducción a los diferentes aspectos de [!DNL Data Ingestion] en [!DNL Experience Platform]. Continúe leyendo la documentación de información general de cada método de ingesta para familiarizarse con sus diferentes capacidades, casos de uso y prácticas recomendadas. También puede complementar su aprendizaje viendo el siguiente vídeo de información general sobre la ingesta. Para obtener información sobre cómo [!DNL Experience Platform] realiza el seguimiento de los metadatos de los registros ingeridos, consulte la [descripción general del servicio de catálogo](../catalog/home.md).

>[!WARNING]
>
>El término &quot;perfil unificado&quot; que se utiliza en el siguiente vídeo no está actualizado. Los términos [!DNL "Profile"] o [!DNL "Real-Time Customer Profile"] son los términos correctos utilizados en la documentación de [!DNL Experience Platform]. Consulte la documentación para obtener la funcionalidad más reciente.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
