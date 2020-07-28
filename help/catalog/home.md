---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general del servicio de catálogo
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 6%

---


# [!DNL Catalog Service]sobre validación

[!DNL Catalog Service] es el sistema de registro para la ubicación y linaje de datos dentro del Adobe Experience Platform. Aunque todos los datos que se ingestan [!DNL Experience Platform] se almacenan en el [!DNL Data Lake] como archivos y directorios, [!DNL Catalog] guarda los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y supervisión.

En pocas palabras, [!DNL Catalog] actúa como un almacén de metadatos o un &quot;[!UICONTROL catálogo]&quot; donde puede encontrar información sobre sus datos dentro de [!DNL Experience Platform]. Puede usar [!DNL Catalog] para responder a las siguientes preguntas:

* ¿Dónde se encuentran mis datos?
* ¿En qué fase de procesamiento se encuentran estos datos?
* ¿Qué sistemas o procesos han actuado en mis datos?
* ¿Cuántos datos se procesaron correctamente?
* ¿Qué errores se produjeron durante el procesamiento?

[!DNL Catalog] proporciona una API RESTful que le permite administrar mediante programación [!DNL Platform] metadatos mediante operaciones CRUD básicas. Consulte la guía para desarrolladores de [catálogos](api/getting-started.md) para obtener más información.

## [!DNL Catalog] y [!DNL Experience Platform] servicios

Los recursos que [!DNL Catalog Service] rastrea son utilizados por varios [!DNL Experience Platform] servicios. Para aprovechar al máximo [!DNL Catalog's] las capacidades, se recomienda familiarizarse con estos servicios y con cómo interactúan con ellos [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) Sistema es el marco estandarizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente. [!DNL Experience Platform] aprovecha los esquemas XDM para describir la estructura de los datos de una manera consistente y reutilizable.

Cuando los datos se ingieren en [!DNL Platform], la estructura de esos datos se asigna a un esquema XDM y se almacena en el [!DNL Data Lake] como parte de un **conjunto de datos**. Los metadatos de cada conjunto de datos son rastreados por [!DNL Catalog Service], lo que incluye una referencia al esquema XDM al que se ajusta el conjunto de datos.

Para obtener información más general sobre el sistema XDM, consulte la descripción general [del sistema](../xdm/home.md)XDM.

### [!DNL Data Ingestion]

[!DNL Experience Platform] ingiere datos de varias fuentes y mantiene los registros como conjuntos de datos dentro del [!DNL Data Lake]. [!DNL Catalog] rastrea los metadatos de estos conjuntos de datos, independientemente de su origen o método de ingestión.

Cuando se utiliza el método de ingestión por lotes, [!DNL Catalog] también se rastrean metadatos adicionales para los archivos por **lotes** . Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. [!DNL Catalog] realiza un seguimiento de los metadatos de estos archivos por lotes, así como de los conjuntos de datos en los que se conservan tras la ingestión. Los metadatos del lote incluyen información sobre el número de registros que se han ingestado correctamente, así como sobre los registros fallidos y los mensajes de error asociados.

Consulte la descripción general [de la ingestión de](../ingestion/home.md) datos para obtener más información.

## [!DNL Catalog] objetos

Como se describe en la sección anterior, [!DNL Catalog] rastrea los metadatos de varios tipos de recursos y operaciones que utilizan otros [!DNL Platform] servicios. [!DNL Catalog] mantiene su propio almacén de &quot;objetos&quot; que encapsula estos metadatos. [!DNL Catalog] los objetos son representaciones consultables de los [!DNL Platform] datos que le permiten buscar, supervisar y etiquetar los datos sin necesidad de acceder a los mismos.

La siguiente tabla describe los distintos tipos de objetos admitidos por [!DNL Catalog]:

| Objeto | Extremo API | Definición |
|---|---|---|
| Cuenta | `/accounts` | Al crear conexiones de origen, se deben proporcionar credenciales de autenticación. Una cuenta representa una colección de credenciales de autenticación que se utilizaron para crear una conexión de un tipo específico. Cada conexión tiene un conjunto de parámetros únicos que se mantienen [!DNL Catalog] y aseguran en un [!DNL Azure Key Vault]. |
| Lote | `/batches` | Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Un objeto de lote [!DNL Catalog] describe las métricas de ingestión del lote (como el número de registros procesados o el tamaño del disco) y también puede incluir vínculos a conjuntos de datos, vistas y otros recursos que se vieron afectados por la operación por lotes. |
| Conexión | `/connections` | Una conexión es una única instancia de un conector de origen, exclusivo de su organización y configurado con las credenciales de autenticación correspondientes para el tipo de conector. |
| Conector | `/connectors` | Los conectores definen la forma en que las conexiones de origen deben recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob]los servidores FTP [!DNL Amazon S3], FTP y SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]). |
| Conjunto de datos | `/dataSets` | Un conjunto de datos es un almacenamiento y una estructura de administración que se utiliza para recopilar datos (generalmente una tabla) que contiene un esquema (columnas) y campos (filas). Consulte la información general [de los](./datasets/overview.md) conjuntos de datos para obtener más información. |
| Archivo de conjunto de datos | `/datasetFiles` | Los archivos de conjunto de datos representan bloques de datos que se han guardado en [!DNL Platform]. Como registros de archivos literales, es allí donde puede encontrar el tamaño del archivo, el número de registros que contiene y una referencia al lote que ingesta el archivo. |

## Pasos siguientes

Este documento proporcionó una introducción [!DNL Catalog Service] y la manera en que funciona dentro del bueno ámbito de [!DNL Experience Platform]. Consulte la guía [para desarrolladores de](api/getting-started.md) catálogos para ver los pasos para interactuar con los distintos extremos de esa [!DNL Catalog] API. También se recomienda consultar la guía sobre el [filtrado de datos](api/filter-data.md) del catálogo para seguir las prácticas recomendadas para limitar los datos devueltos en las respuestas de la API.