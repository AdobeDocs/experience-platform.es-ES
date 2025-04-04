---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;catálogo;servicio de catálogo;ubicación de datos;ubicación de datos;administración de datos;administración de datos;linaje;linaje;catálogo;habilitar conjunto de datos
solution: Experience Platform
title: Resumen del servicio de catálogo
description: El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 8%

---

# Información general de [!DNL Catalog Service]

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan en [!DNL Experience Platform] se almacenan en [!DNL Data Lake] como archivos y directorios, [!DNL Catalog] contiene los metadatos y la descripción de esos archivos y directorios con fines de búsqueda y supervisión.

En pocas palabras, [!DNL Catalog] actúa como un almacén de metadatos o &quot;catálogo&quot; en el que puede encontrar información acerca de sus datos dentro de [!DNL Experience Platform]. Puede usar [!DNL Catalog] para responder a las siguientes preguntas:

* ¿Dónde se encuentran mis datos?
* ¿En qué fase del procesamiento se encuentran estos datos?
* ¿Qué sistemas o procesos han actuado en mis datos?
* ¿Cuántos datos se procesaron correctamente?
* ¿Qué errores se han producido durante el procesamiento?

[!DNL Catalog] proporciona una API RESTful que le permite administrar mediante programación los metadatos de [!DNL Experience Platform] mediante operaciones básicas de CRUD. Consulte la [Guía para desarrolladores de catálogos](api/getting-started.md) para obtener más información.

## [!DNL Catalog] y [!DNL Experience Platform] servicios

Varios servicios de [!DNL Experience Platform] utilizan los recursos que [!DNL Catalog Service] rastrea. Para aprovechar al máximo las capacidades de [!DNL Catalog's], se recomienda que se familiarice con estos servicios y cómo interactúan con [!DNL Catalog].

### Sistema [!DNL Experience Data Model] (XDM)

El sistema [!DNL Experience Data Model] (XDM) es el marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente. [!DNL Experience Platform] aprovecha los esquemas XDM para describir la estructura de los datos de una manera uniforme y reutilizable.

Cuando se incorporan datos en [!DNL Experience Platform], la estructura de esos datos se asigna a un esquema XDM y se almacena dentro de [!DNL Data Lake] como parte de un conjunto de datos. [!DNL Catalog Service] realiza el seguimiento de los metadatos de cada conjunto de datos, lo que incluye una referencia al esquema XDM al que se ajusta el conjunto de datos.

Para obtener más información general sobre el sistema XDM, consulte la [descripción general del sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] ingiere datos de varios orígenes y conserva registros como conjuntos de datos dentro de [!DNL Data Lake]. [!DNL Catalog] realiza el seguimiento de los metadatos de estos conjuntos de datos, independientemente de su origen o método de ingesta.

Al utilizar el método de ingesta por lotes, [!DNL Catalog] también realiza un seguimiento de los metadatos adicionales de los archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. [!DNL Catalog] realiza el seguimiento de los metadatos de estos archivos por lotes, así como de los conjuntos de datos en los que se mantienen después de la ingesta. Los metadatos por lotes incluyen información sobre el número de registros ingeridos correctamente, así como sobre los registros con errores y los mensajes de error asociados.

Consulte la [descripción general de la ingesta de datos](../ingestion/home.md) para obtener más información.

## [!DNL Catalog] objetos

Como se describe en la sección anterior, [!DNL Catalog] realiza un seguimiento de los metadatos de varios tipos de recursos y operaciones que utilizan otros servicios de [!DNL Experience Platform]. [!DNL Catalog] mantiene su propio almacén de &quot;objetos&quot; que encapsulan estos metadatos. Los objetos [!DNL Catalog] son representaciones consultables de datos [!DNL Experience Platform] que le permiten buscar, supervisar y etiquetar sus datos sin necesidad de tener acceso a los propios datos.

En la tabla siguiente se describen los diferentes tipos de objetos admitidos por [!DNL Catalog]:

| Objeto | Extremo de API | Definición |
|---|---|---|
| Lote | `/batches` | Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Un objeto batch de [!DNL Catalog] describe las métricas de ingesta del lote (como el número de registros procesados o el tamaño en el disco) y también puede incluir vínculos a conjuntos de datos, vistas y otros recursos afectados por la operación por lotes. |
| Conjunto de datos | `/dataSets` | Un conjunto de datos es una construcción de almacenamiento y administración que se utiliza para recopilar datos (normalmente una tabla) que contiene un esquema (columnas) y campos (filas). Consulte la [descripción general de conjuntos de datos](./datasets/overview.md) para obtener más información. |
| Archivo de conjunto de datos | `/datasetFiles` | Los archivos de conjuntos de datos representan bloques de datos que se guardaron en [!DNL Experience Platform]. Como registros de archivos literales, aquí es donde puede encontrar el tamaño del archivo, el número de registros que contiene y una referencia al lote que ingerió el archivo. |

## Pasos siguientes

Este documento proporciona una introducción a [!DNL Catalog Service] y cómo funciona dentro del ámbito mayor de [!DNL Experience Platform]. Consulte la [[!DNL Catalog] guía para desarrolladores](api/getting-started.md) para ver los pasos que debe seguir para interactuar con los diferentes extremos de esa API de [!DNL Catalog]. Se recomienda que también consulte la guía sobre [filtrado de datos de catálogo](api/filter-data.md) para seguir las prácticas recomendadas y limitar los datos devueltos en las respuestas de API.
