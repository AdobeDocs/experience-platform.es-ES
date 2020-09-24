---
keywords: Experience Platform;home;popular topics;query service;Query service;create queries;
solution: Experience Platform
title: Creación de consultas
topic: queries
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 3%

---


# Creación de consultas

Adobe Experience Platform [!DNL Query Service] proporciona la capacidad para ejecutar consultas SQL con conjuntos de datos en el [!DNL Data Lake] interior [!DNL Experience Platform]. Al utilizar SQL para interactuar con conjuntos de datos en el lago de datos, es importante comprender que [!DNL Query Service] administra automáticamente determinados aspectos, como la creación de nombres de tabla seguros para SQL para cada conjunto de datos en el [!DNL Data Lake]. También hay consideraciones sobre cómo trabajar con datos jerárquicos en el [!DNL Data Lake]sitio, incluido el descubrimiento del esquema en el que se basa un conjunto de datos y garantizar que se selecciona el campo correcto dentro del modelo jerárquico.

La siguiente documentación le ayudará a comprender mejor los conceptos principales dentro de [!DNL Query Service]:

- [Conjuntos de datos vs. tablas y esquemas](./datasets-and-tables.md)
- [Directrices generales para la redacción de consultas](./writing-queries.md)
- [Consultas de ExperienceEvent](./experience-event-queries.md)
- [Incorporación de conjuntos de datos](./joining-datasets.md)
- [Desduplicación de datos](./deduplication.md)
