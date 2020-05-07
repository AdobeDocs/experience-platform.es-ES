---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Introducción al aprendizaje automático en tiempo real
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Introducción al aprendizaje automático en tiempo real

>[!IMPORTANT]
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

Para utilizar el aprendizaje automático en tiempo real, debe tener acceso a una organización aprovisionada con Adobe Experience Platform y Data Science Workspace. Además, necesita tener un conjunto de datos en Plataforma.

Las guías para aprendizaje automático en tiempo real requieren un conocimiento práctico de los portátiles Python 3, [Jupyter](../jupyterlab/overview.md), la ciencia de datos y el aprendizaje automático.

## Conjuntos de datos en Adobe Experience Platform

Para realizar inicios mediante aprendizaje automático en tiempo real, debe disponer de un conjunto de datos rellenado en la plataforma de experiencia. Tiene la opción de usar un conjunto de datos externo y cargarlo en su entorno de JupyterLab o crear un nuevo conjunto de datos dentro de la plataforma si aún no lo ha hecho.

>[!NOTE]
>Si ya tiene un conjunto de datos que desea utilizar, puede omitir los dos pasos siguientes.

### Usar un conjunto de datos externo

Para obtener más información sobre el uso de un conjunto de datos externo, como cargar datos en el entorno de JupyterLab, visite el tutorial sobre el [análisis de datos con portátiles](../jupyterlab/analyze-your-data.md#external-data).

### Crear un nuevo conjunto de datos

Para crear un nuevo conjunto de datos para utilizarlo en el aprendizaje automático en tiempo real, necesita un esquema de datos para el conjunto de datos. A continuación, debe ingestar los datos con el esquema que ha creado. Utilice los siguientes tutoriales para crear y rellenar un conjunto de datos para la plataforma:

- [Creación y rellenado de un conjunto de datos en la API](../../catalog/datasets/create.md)
- [Creación y rellenado de un conjunto de datos en la interfaz de usuario](../../ingestion/tutorials/ingest-batch-data.md)

## Git y Docker

Si planea formar un modelo mediante el flujo de trabajo de fórmula de Data Science Workplace, se requieren Git y Docker.

>[!NOTE]
>No necesita descargar Git y Docker si planea entrenar un modelo con un portátil Python o si está utilizando su propio modelo ONNX.

- [Guía de instalación de Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Guía de instalación del acoplador](https://docs.docker.com/get-docker/)

## Pasos siguientes

Una vez que haya preparado los datos para el aprendizaje automático en tiempo real, siga el inicio del tutorial sobre la [formación de un modelo](./training-ml-model.md) para aprender a crear y cargar un modelo ONNX en la tienda modelo de aprendizaje automático en tiempo real.

