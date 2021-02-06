---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;servicio de catálogo;servicio de catálogo;ubicación de datos;Ubicación de datos;Gestión de datos;gestión de datos;Linaje;linaje;Catálogo;habilitar conjunto de datos
solution: Experience Platform
title: Información general del servicio de catálogo
topic: overview
description: Catalog Service es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. Aunque todos los datos que se ingestan en el Experience Platform se almacenan en el Data Lake como archivos y directorios, Catalog guarda los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y supervisión.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---


# Información general del [!DNL Catalog Service]

[!DNL Catalog Service] es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se ingestan en [!DNL Experience Platform] se almacenan en [!DNL Data Lake] como archivos y directorios, [!DNL Catalog] guarda los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitoreo.

En pocas palabras, [!DNL Catalog] actúa como un almacén de metadatos o &quot;catálogo&quot; donde puede encontrar información sobre sus datos dentro de [!DNL Experience Platform]. Puede utilizar [!DNL Catalog] para responder a las siguientes preguntas:

* ¿Dónde se encuentran mis datos?
* ¿En qué fase de procesamiento se encuentran estos datos?
* ¿Qué sistemas o procesos han actuado en mis datos?
* ¿Cuántos datos se procesaron correctamente?
* ¿Qué errores se produjeron durante el procesamiento?

[!DNL Catalog] proporciona una API RESTful que le permite administrar  [!DNL Platform] metadatos mediante programación mediante operaciones CRUD básicas. Consulte la [guía para desarrolladores de catálogos](api/getting-started.md) para obtener más información.

## [!DNL Catalog] y  [!DNL Experience Platform] servicios

Los recursos que [!DNL Catalog Service] rastrea son utilizados por varios servicios [!DNL Experience Platform]. Para aprovechar al máximo las [!DNL Catalog's] capacidades, se recomienda familiarizarse con estos servicios y con cómo interactúan con [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) Sistema es el marco estandarizado por el cual  [!DNL Platform] organiza los datos de experiencia del cliente. [!DNL Experience Platform] aprovecha los esquemas XDM para describir la estructura de los datos de una manera consistente y reutilizable.

Cuando los datos se ingieren en [!DNL Platform], la estructura de esos datos se asigna a un esquema XDM y se almacena dentro de [!DNL Data Lake] como parte de un conjunto de datos. Los metadatos de cada conjunto de datos son rastreados por [!DNL Catalog Service], que incluye una referencia al esquema XDM al que se ajusta el conjunto de datos.

Para obtener información más general sobre el sistema XDM, consulte la [información general del sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] ingiere datos de varias fuentes y mantiene los registros como conjuntos de datos dentro del  [!DNL Data Lake]. [!DNL Catalog] rastrea los metadatos de estos conjuntos de datos, independientemente de su origen o método de ingestión.

Al utilizar el método de ingestión por lotes, [!DNL Catalog] también rastrea metadatos adicionales para los archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. [!DNL Catalog] realiza un seguimiento de los metadatos de estos archivos por lotes, así como de los conjuntos de datos en los que se conservan tras la ingestión. Los metadatos del lote incluyen información sobre el número de registros que se han ingestado correctamente, así como sobre los registros fallidos y los mensajes de error asociados.

Consulte la [información general sobre la ingestión de datos](../ingestion/home.md) para obtener más información.

## [!DNL Catalog] objetos

Como se describe en la sección anterior, [!DNL Catalog] rastrea metadatos para varios tipos de recursos y operaciones que utilizan otros [!DNL Platform] servicios. [!DNL Catalog] mantiene su propio almacén de &quot;objetos&quot; que encapsula estos metadatos. [!DNL Catalog] los objetos son representaciones consultables de  [!DNL Platform] datos que le permiten buscar, supervisar y etiquetar sus datos sin necesidad de acceder a los mismos.

La siguiente tabla describe los diferentes tipos de objetos admitidos por [!DNL Catalog]:

| Objeto | Extremo API | Definición |
|---|---|---|
| Cuenta | `/accounts` | Al crear conexiones de origen, se deben proporcionar credenciales de autenticación. Una cuenta representa una colección de credenciales de autenticación que se utilizaron para crear una conexión de un tipo específico. Cada conexión tiene un conjunto de parámetros únicos que [!DNL Catalog] mantienen y aseguran en [!DNL Azure Key Vault]. |
| Lote | `/batches` | Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Un objeto de lote en [!DNL Catalog] describe las métricas de ingestión del lote (como el número de registros procesados o el tamaño del disco) y también puede incluir vínculos a conjuntos de datos, vistas y otros recursos que se vieron afectados por la operación por lotes. |
| Conexión | `/connections` | Una conexión es una única instancia de un conector de origen, exclusivo de su organización y configurado con las credenciales de autenticación correspondientes para el tipo de conector. |
| Conector | `/connectors` | Los conectores definen la manera en que las conexiones de origen deben recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon S3], servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]). |
| Conjunto de datos | `/dataSets` | Un conjunto de datos es un almacenamiento y una estructura de administración que se utiliza para recopilar datos (generalmente una tabla) que contiene un esquema (columnas) y campos (filas). Consulte la [información general de datasets](./datasets/overview.md) para obtener más información. |
| Archivo de conjunto de datos | `/datasetFiles` | Los archivos de conjunto de datos representan bloques de datos que se han guardado en [!DNL Platform]. Como registros de archivos literales, es allí donde puede encontrar el tamaño del archivo, el número de registros que contiene y una referencia al lote que ingesta el archivo. |

## Pasos siguientes

Este documento proporcionó una introducción a [!DNL Catalog Service] y a cómo funciona dentro del bueno ámbito de [!DNL Experience Platform]. Consulte la [[!DNL Catalog] guía para desarrolladores](api/getting-started.md) para ver los pasos para interactuar con los diferentes extremos de esa [!DNL Catalog] API. También se recomienda consultar la guía sobre [filtrado de datos del catálogo](api/filter-data.md) para seguir las optimizaciones para limitar los datos devueltos en las respuestas de la API.