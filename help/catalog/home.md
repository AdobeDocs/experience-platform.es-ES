---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;catálogo;servicio de catálogo;ubicación de datos;ubicación de datos;gestión de datos;administración de datos;linaje;catálogo;habilitar conjunto de datos
solution: Experience Platform
title: Descripción general del servicio de catálogo
description: El servicio de catálogo es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. Aunque todos los datos que se incorporan en el Experience Platform se almacenan en el lago de datos como archivos y directorios, Catálogo guarda los metadatos y la descripción de esos archivos y directorios con fines de búsqueda y supervisión.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# Información general del [!DNL Catalog Service]

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Aunque todos los datos que se incorporan en [!DNL Experience Platform] se almacena en la variable [!DNL Data Lake] como archivos y directorios, [!DNL Catalog] contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

En pocas palabras, [!DNL Catalog] actúa como almacén de metadatos o &quot;catálogo&quot;, donde puede encontrar información sobre sus datos dentro de [!DNL Experience Platform]. Puede usar [!DNL Catalog] para responder a las siguientes preguntas:

* ¿Dónde se encuentran mis datos?
* ¿En qué fase de procesamiento se encuentran estos datos?
* ¿Qué sistemas o procesos han actuado sobre mis datos?
* ¿Cuántos datos se procesaron correctamente?
* ¿Qué errores se han producido durante el procesamiento?

[!DNL Catalog] proporciona una API de RESTful que le permite administrar mediante programación [!DNL Platform] metadatos utilizando operaciones básicas de CRUD. Consulte la [Guía para desarrolladores del catálogo](api/getting-started.md) para obtener más información.

## [!DNL Catalog] y [!DNL Experience Platform] servicios

Los recursos que [!DNL Catalog Service] las pistas las usan varios [!DNL Experience Platform] servicios. Para sacar el máximo partido a [!DNL Catalog's] , se recomienda que se familiarice con estos servicios y con cómo interactúan con ellos [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] El sistema (XDM) es el marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente. [!DNL Experience Platform] aprovecha los esquemas XDM para describir la estructura de los datos de una manera consistente y reutilizable.

Cuando los datos se introducen en [!DNL Platform], la estructura de esos datos se asigna a un esquema XDM y se almacena dentro de la variable [!DNL Data Lake] como parte de un conjunto de datos. El seguimiento de los metadatos de cada conjunto de datos se realiza mediante [!DNL Catalog Service], que incluye una referencia al esquema XDM al que se ajusta el conjunto de datos.

Para obtener información más general sobre el sistema XDM, consulte la [Información general del sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] Ingesta datos de varias fuentes y mantiene registros como conjuntos de datos dentro de la variable [!DNL Data Lake]. [!DNL Catalog] rastrea los metadatos de estos conjuntos de datos, independientemente de su origen o método de ingesta.

Al utilizar el método de ingesta por lotes, [!DNL Catalog] también realiza el seguimiento de metadatos adicionales para archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. [!DNL Catalog] rastrea los metadatos de estos archivos por lotes, así como los conjuntos de datos en los que se conservan tras la ingesta. Los metadatos del lote incluyen información sobre el número de registros introducidos correctamente, así como los registros fallidos y los mensajes de error asociados.

Consulte la [información general sobre la ingesta de datos](../ingestion/home.md) para obtener más información.

## [!DNL Catalog] objetos

Como se describe en la sección anterior, [!DNL Catalog] rastrea metadatos para varios tipos de recursos y operaciones que otros utilizan [!DNL Platform] servicios. [!DNL Catalog] mantiene su propio almacén de &quot;objetos&quot; que encapsula estos metadatos. [!DNL Catalog] los objetos son representaciones consultables de [!DNL Platform] datos que le permiten buscar, supervisar y etiquetar sus datos sin necesidad de acceder a los datos en sí.

La tabla siguiente resume los distintos tipos de objetos admitidos por [!DNL Catalog]:

| Objeto | Punto de conexión de API | Definición |
|---|---|---|
| Cuenta | `/accounts` | Al crear conexiones de origen, se deben proporcionar credenciales de autenticación. Una cuenta representa una colección de credenciales de autenticación que se utilizaron para crear una conexión de un tipo específico. Cada conexión tiene un conjunto de parámetros únicos que son persistentes por [!DNL Catalog] y garantizadas en un [!DNL Azure Key Vault]. |
| Lote | `/batches` | Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Un objeto de lote en [!DNL Catalog] describe las métricas de ingesta del lote (como el número de registros procesados o el tamaño del disco) y también puede incluir vínculos a conjuntos de datos, vistas y otros recursos que se vieron afectados por la operación por lotes. |
| Conexión | `/connections` | Una conexión es una instancia única de un conector de origen, único para su organización y configurado con las credenciales de autenticación adecuadas para el tipo de conector. |
| Conector  | `/connectors` | Los conectores definen el modo en que las conexiones de origen recopilan datos de otras aplicaciones de Adobe (como Adobe Analytics y Adobe Audience Manager), fuentes de almacenamiento en la nube de terceros (como [!DNL Azure Blob], [!DNL Amazon S3], servidores FTP y servidores SFTP) y sistemas CRM de terceros (como [!DNL Microsoft Dynamics] y [!DNL Salesforce]). |
| Conjunto de datos | `/dataSets` | Un conjunto de datos es una construcción de almacenamiento y administración que se utiliza para la recopilación de datos (normalmente una tabla) que contiene un esquema (columnas) y campos (filas). Consulte la [información general sobre conjuntos de datos](./datasets/overview.md) para obtener más información. |
| Archivo de conjunto de datos | `/datasetFiles` | Los archivos de conjunto de datos representan bloques de datos que se han guardado en [!DNL Platform]. Como registros de archivos literales, aquí es donde puede encontrar el tamaño del archivo, el número de registros que contiene y una referencia al lote que ingerió el archivo. |

## Pasos siguientes

Este documento contenía una introducción a [!DNL Catalog Service] y su funcionamiento dentro del bueno ámbito de aplicación [!DNL Experience Platform]. Consulte la [[!DNL Catalog] guía para desarrolladores](api/getting-started.md) para ver los pasos sobre la interacción con los diferentes extremos de aquello [!DNL Catalog] API. Se recomienda consultar también la guía de [filtrado de datos del catálogo](api/filter-data.md) para seguir las prácticas recomendadas y limitar los datos devueltos en las respuestas de API.
