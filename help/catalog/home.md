---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general del servicio de catálogo
topic: overview
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Información general del servicio de catálogo

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de los datos en Adobe Experience Platform. Aunque todos los datos que se ingestan en la plataforma de experiencia se almacenan en el lago de datos como archivos y directorios, Catálogo guarda los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y supervisión.

En pocas palabras, Catálogo actúa como un almacén de metadatos o un &quot;catálogo&quot; en el que puede encontrar información sobre los datos en la plataforma de experiencias. Puede utilizar el catálogo para responder a las siguientes preguntas:

* ¿Dónde se encuentran mis datos?
* ¿En qué fase de procesamiento se encuentran estos datos?
* ¿Qué sistemas o procesos han actuado en mis datos?
* ¿Cuántos datos se procesaron correctamente?
* ¿Qué errores se produjeron durante el procesamiento?

Catalog proporciona una API RESTful que le permite administrar mediante programación metadatos de plataforma mediante operaciones CRUD básicas. Consulte la guía para desarrolladores de [catálogos](api/getting-started.md) para obtener más información.

## Servicios de catálogos y plataformas de experiencias

Los recursos que el servicio de catálogo rastrea son utilizados por varios servicios de la plataforma de experiencia. Para aprovechar al máximo las funciones del catálogo, se recomienda familiarizarse con estos servicios y con la forma en que interactúan con el catálogo.

### Sistema de modelo de datos de experiencia (XDM)

El sistema de modelo de datos de experiencia (XDM) es el marco estandarizado mediante el cual la plataforma organiza los datos de experiencia del cliente. La plataforma de experiencia aprovecha los esquemas XDM para describir la estructura de los datos de una manera consistente y reutilizable.

Cuando los datos se ingieren en la plataforma, la estructura de esos datos se asigna a un esquema XDM y se almacena dentro del lago de datos como parte de un **conjunto de datos**. El servicio de catálogos realiza un seguimiento de los metadatos de cada conjunto de datos, que incluye una referencia al esquema XDM al que se ajusta el conjunto de datos.

Para obtener información más general sobre el sistema XDM, consulte la descripción general [del sistema](../xdm/home.md)XDM.

### Ingesta de datos

La plataforma de experiencia ingesta datos de varias fuentes y mantiene registros como conjuntos de datos dentro del lago de datos. El catálogo rastrea los metadatos de estos conjuntos de datos, independientemente de su origen o método de ingesta.

Al utilizar el método de ingesta por lotes, Catalog también realiza un seguimiento de metadatos adicionales para los archivos de **lotes** . Los lotes son unidades de datos que consisten en uno o más archivos que se van a ingerir como una sola unidad. El catálogo realiza un seguimiento de los metadatos de estos archivos por lotes, así como de los conjuntos de datos en los que se conservan tras la ingestión. Los metadatos del lote incluyen información sobre el número de registros que se han ingestado correctamente, así como sobre los registros fallidos y los mensajes de error asociados.

Consulte la descripción general [de la ingestión de](../ingestion/home.md) datos para obtener más información.

## Objetos del catálogo

Como se describe en la sección anterior, Catálogo realiza un seguimiento de los metadatos de varios tipos de recursos y operaciones que utilizan otros servicios de plataforma. Catalog mantiene su propia tienda de &quot;objetos&quot; que encapsula estos metadatos. Los objetos de catálogo son representaciones cuestionables de los datos de la plataforma que le permiten buscar, supervisar y etiquetar sus datos sin necesidad de acceder a los mismos.

La siguiente tabla describe los distintos tipos de objetos admitidos por Catalog:

| Objeto | Extremo API | Definición |
|---|---|---|
| Cuenta | `/accounts` | Al crear conexiones de origen, se deben proporcionar credenciales de autenticación. Una cuenta representa una colección de credenciales de autenticación que se utilizaron para crear una conexión de un tipo específico. Cada conexión tiene un conjunto de parámetros únicos que el catálogo persiste y que se protegen en un Almacén de claves de Azure. |
| Lote | `/batches` | Los lotes son unidades de datos que consisten en uno o más archivos que se van a ingerir como una sola unidad. Un objeto de lote en Catálogo describe las métricas de ingestión del lote (como el número de registros procesados o el tamaño del disco) y también puede incluir vínculos a conjuntos de datos, vistas y otros recursos que se vieron afectados por la operación por lotes. |
| Conexión | `/connections` | Una conexión es una única instancia de un conector de origen, exclusivo de su organización y configurado con las credenciales de autenticación correspondientes para el tipo de conector. |
| Conector | `/connectors` | Los conectores definen el modo en que las conexiones de origen deben recopilar datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audiencia Manager), fuentes de almacenamiento en la nube de terceros (como Azure Blob, Amazon S3, servidores FTP y servidores SFTP) y sistemas CRM de terceros (como Microsoft Dynamics y Salesforce). |
| Conjunto de datos | `/dataSets` | Un conjunto de datos es un almacenamiento y una estructura de administración que se utiliza para recopilar datos (generalmente una tabla) que contiene un esquema (columnas) y campos (filas). |
| Archivo de conjunto de datos | `/datasetFiles` | Los archivos de conjunto de datos representan bloques de datos que se han guardado en la plataforma. Como registros de archivos literales, es allí donde puede encontrar el tamaño del archivo, el número de registros que contiene y una referencia al lote que ingesta el archivo. |

## Pasos siguientes

Este documento proporcionó una introducción al servicio de catálogos y a cómo funciona dentro del bueno ámbito de la plataforma de experiencias. Consulte la guía [para desarrolladores de](api/getting-started.md) catálogos para ver los pasos para interactuar con los distintos extremos de esa API de catálogo. También se recomienda consultar la guía sobre el [filtrado de datos](api/filter-data.md) del catálogo para seguir las prácticas recomendadas para limitar los datos devueltos en las respuestas de la API.