---
keywords: Experience Platform;home;popular topics;query service;Query service;create queries;
solution: Experience Platform
title: Creación de consultas
topic: queries
type: Tutorial
description: Este documento se vincula a la documentación básica utilizada para crear y comprender consultas en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '131'
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
