---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;catálogo;servicio de catálogo;ubicación de datos;ubicación de datos;gestión de datos;administración de datos;linaje;catálogo;habilitar conjunto de datos
solution: Experience Platform
title: Descripción general del servicio de catálogo
topic-legacy: overview
description: El servicio de catálogo es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. Aunque todos los datos que se incorporan en el Experience Platform se almacenan en el lago de datos como archivos y directorios, Catálogo guarda los metadatos y la descripción de esos archivos y directorios con fines de búsqueda y supervisión.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# Información general del [!DNL Catalog Service]

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a [!DNL Experience Platform] se almacenan en [!DNL Data Lake] como archivos y directorios, [!DNL Catalog] guarda los metadatos y la descripción de esos archivos y directorios con fines de búsqueda y monitorización.

En pocas palabras, [!DNL Catalog] actúa como un almacén de metadatos o un &quot;catálogo&quot; donde puede encontrar información sobre sus datos en [!DNL Experience Platform]. Puede utilizar [!DNL Catalog] para responder a las siguientes preguntas:

* ¿Dónde se encuentran mis datos?
* ¿En qué fase de procesamiento se encuentran estos datos?
* ¿Qué sistemas o procesos han actuado sobre mis datos?
* ¿Cuántos datos se procesaron correctamente?
* ¿Qué errores se han producido durante el procesamiento?

[!DNL Catalog] proporciona una API RESTful que le permite administrar  [!DNL Platform] metadatos mediante programación mediante operaciones CRUD básicas. Consulte la [Guía para desarrolladores de catálogo](api/getting-started.md) para obtener más información.

## [!DNL Catalog] y  [!DNL Experience Platform] servicios

Los recursos que [!DNL Catalog Service] rastrea son utilizados por varios servicios [!DNL Experience Platform]. Para aprovechar al máximo las capacidades de [!DNL Catalog's], se recomienda que se familiarice con estos servicios y con cómo interactúan con [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) El sistema es el marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente. [!DNL Experience Platform] aprovecha los esquemas XDM para describir la estructura de los datos de una manera consistente y reutilizable.

Cuando los datos se incorporan en [!DNL Platform], la estructura de esos datos se asigna a un esquema XDM y se almacena dentro de [!DNL Data Lake] como parte de un conjunto de datos. Los metadatos de cada conjunto de datos se rastrean mediante [!DNL Catalog Service], que incluye una referencia al esquema XDM con el que se ajusta el conjunto de datos.

Para obtener información más general sobre el sistema XDM, consulte la [información general del sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] Ingesta datos de varias fuentes y mantiene registros como conjuntos de datos dentro de  [!DNL Data Lake]. [!DNL Catalog] rastrea los metadatos de estos conjuntos de datos, independientemente de su origen o método de ingesta.

Al utilizar el método de ingesta por lotes, [!DNL Catalog] también realiza el seguimiento de metadatos adicionales para archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. [!DNL Catalog] rastrea los metadatos de estos archivos por lotes, así como los conjuntos de datos en los que se conservan tras la ingesta. Los metadatos del lote incluyen información sobre el número de registros introducidos correctamente, así como los registros fallidos y los mensajes de error asociados.

Consulte la [información general sobre la ingesta de datos](../ingestion/home.md) para obtener más información.

## [!DNL Catalog] objetos

Como se describe en la sección anterior, [!DNL Catalog] rastrea metadatos de varios tipos de recursos y operaciones que utilizan otros servicios [!DNL Platform]. [!DNL Catalog] mantiene su propio almacén de &quot;objetos&quot; que encapsula estos metadatos. [!DNL Catalog] Los objetos son representaciones consultables de  [!DNL Platform] datos que permiten buscar, supervisar y etiquetar los datos sin necesidad de acceder a los datos en sí.

La siguiente tabla describe los distintos tipos de objetos admitidos por [!DNL Catalog]:

| Objeto | Punto de conexión de API | Definición |
|---|---|---|
| Cuenta | `/accounts` | Al crear conexiones de origen, se deben proporcionar credenciales de autenticación. Una cuenta representa una colección de credenciales de autenticación que se utilizaron para crear una conexión de un tipo específico. Cada conexión tiene un conjunto de parámetros únicos que [!DNL Catalog] persiste y que se protegen en [!DNL Azure Key Vault]. |
| Lote | `/batches` | Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Un objeto de lote en [!DNL Catalog] describe las métricas de ingesta del lote (como el número de registros procesados o el tamaño del disco) y también puede incluir vínculos a conjuntos de datos, vistas y otros recursos que se vieron afectados por la operación por lotes. |
| Conexión | `/connections` | Una conexión es una instancia única de un conector de origen, único para su organización y configurado con las credenciales de autenticación adecuadas para el tipo de conector. |
| Conector | `/connectors` | Los conectores definen cómo se recopilan las conexiones de origen de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon S3], servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]). |
| Conjunto de datos | `/dataSets` | Un conjunto de datos es una construcción de almacenamiento y administración que se utiliza para la recopilación de datos (normalmente una tabla) que contiene un esquema (columnas) y campos (filas). Consulte la [descripción general de los conjuntos de datos](./datasets/overview.md) para obtener más información. |
| Archivo de conjunto de datos | `/datasetFiles` | Los archivos de conjunto de datos representan bloques de datos que se han guardado en [!DNL Platform]. Como registros de archivos literales, aquí es donde puede encontrar el tamaño del archivo, el número de registros que contiene y una referencia al lote que ingerió el archivo. |

## Pasos siguientes

Este documento ofrecía una introducción a [!DNL Catalog Service] y cómo funciona dentro del bueno ámbito de [!DNL Experience Platform]. Consulte la [[!DNL Catalog] guía para desarrolladores](api/getting-started.md) para ver los pasos necesarios para interactuar con los diferentes extremos de esa API [!DNL Catalog]. Se recomienda consultar la guía sobre el [filtrado de datos del catálogo](api/filter-data.md) para seguir las prácticas recomendadas para limitar los datos devueltos en las respuestas de API.
