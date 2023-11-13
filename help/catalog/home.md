---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;catálogo;servicio de catálogo;ubicación de datos;ubicación de datos;administración de datos;administración de datos;linaje;linaje;catálogo;habilitar conjunto de datos
solution: Experience Platform
title: Resumen del servicio de catálogo
description: El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 0ebe9eadb1bce6252b43a50af009ce1b0f6e5d6e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 13%

---

# Información general del [!DNL Catalog Service]

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan en [!DNL Experience Platform] se almacena en [!DNL Data Lake] como archivos y directorios, [!DNL Catalog] contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y supervisión.

En pocas palabras, [!DNL Catalog] actúa como un almacén de metadatos o catálogo en el que puede encontrar información sobre sus datos dentro de [!DNL Experience Platform]. Puede utilizar [!DNL Catalog] para responder a las siguientes preguntas:

* ¿Dónde se encuentran mis datos?
* ¿En qué fase del procesamiento se encuentran estos datos?
* ¿Qué sistemas o procesos han actuado en mis datos?
* ¿Cuántos datos se procesaron correctamente?
* ¿Qué errores se han producido durante el procesamiento?

[!DNL Catalog] proporciona una API RESTful que le permite administrar mediante programación [!DNL Platform] metadatos que utilizan operaciones básicas de CRUD. Consulte la [Guía para desarrolladores de catálogos](api/getting-started.md) para obtener más información.

## [!DNL Catalog] y [!DNL Experience Platform] servicios

Los recursos que [!DNL Catalog Service] varias pistas las utilizan [!DNL Experience Platform] servicios. Para sacar el máximo partido a [!DNL Catalog's] funciones, se recomienda que se familiarice con estos servicios y con cómo interactúan con [!DNL Catalog].

### [!DNL Experience Data Model] Sistema (XDM)

[!DNL Experience Data Model] (XDM) El sistema es el marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente. [!DNL Experience Platform] aprovecha los esquemas XDM para describir la estructura de los datos de una manera uniforme y reutilizable.

Cuando se incorporan datos en [!DNL Platform], la estructura de esos datos se asigna a un esquema XDM y se almacena en el [!DNL Data Lake] como parte de un conjunto de datos. Los metadatos de cada conjunto de datos se rastrean mediante [!DNL Catalog Service], que incluye una referencia al esquema XDM al que se ajusta el conjunto de datos.

Para obtener información más general sobre el sistema XDM, consulte la [Información general del sistema XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] ingiere datos de varias fuentes y conserva registros como conjuntos de datos dentro de la variable [!DNL Data Lake]. [!DNL Catalog] rastrea los metadatos de estos conjuntos de datos, independientemente de su origen o método de ingesta.

Al utilizar el método de ingesta por lotes, [!DNL Catalog] también realiza un seguimiento de metadatos adicionales para archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. [!DNL Catalog] rastrea los metadatos de estos archivos por lotes, así como los conjuntos de datos en los que se mantienen después de la ingesta. Los metadatos por lotes incluyen información sobre el número de registros ingeridos correctamente, así como sobre los registros con errores y los mensajes de error asociados.

Consulte la [información general sobre ingesta de datos](../ingestion/home.md) para obtener más información.

## [!DNL Catalog] objetos

Como se indica en la sección anterior, [!DNL Catalog] realiza un seguimiento de los metadatos de varios tipos de recursos y operaciones utilizados por otros [!DNL Platform] servicios. [!DNL Catalog] mantiene su propio almacén de &quot;objetos&quot; que encapsulan estos metadatos. [!DNL Catalog] Los objetos son representaciones consultables de [!DNL Platform] datos que le permiten buscar, monitorizar y etiquetar sus datos sin necesidad de acceder a los propios datos.

En la tabla siguiente se describen los distintos tipos de objetos admitidos por [!DNL Catalog]:

| Objeto | Extremo de API | Definición |
|---|---|---|
| Lote | `/batches` | Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Un objeto por lotes en [!DNL Catalog] describe las métricas de ingesta del lote (como el número de registros procesados o el tamaño en disco) y también puede incluir vínculos a conjuntos de datos, vistas y otros recursos afectados por la operación por lotes. |
| Conjunto de datos | `/dataSets` | Un conjunto de datos es una construcción de almacenamiento y administración que se utiliza para recopilar datos (normalmente una tabla) que contiene un esquema (columnas) y campos (filas). Consulte la [información general sobre conjuntos de datos](./datasets/overview.md) para obtener más información. |
| Archivo de conjunto de datos | `/datasetFiles` | Los archivos de conjuntos de datos representan bloques de datos que se han guardado en [!DNL Platform]. Como registros de archivos literales, aquí es donde puede encontrar el tamaño del archivo, el número de registros que contiene y una referencia al lote que ingerió el archivo. |

## Pasos siguientes

Este documento proporciona una introducción a [!DNL Catalog Service] y cómo funciona dentro del ámbito más amplio de [!DNL Experience Platform]. Consulte la [[!DNL Catalog] guía para desarrolladores](api/getting-started.md) para ver los pasos necesarios para interactuar con los diferentes extremos de [!DNL Catalog] API. Se recomienda consultar también la guía sobre [filtrado de datos de catálogo](api/filter-data.md) para seguir las prácticas recomendadas y limitar los datos devueltos en las respuestas de API.
