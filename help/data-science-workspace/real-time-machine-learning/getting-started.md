---
keywords: Experience Platform;guía para desarrolladores;espacio de trabajo de ciencia de datos;temas populares;aprendizaje automático en tiempo real;
solution: Experience Platform
title: Introducción al aprendizaje automático en tiempo real
description: En el siguiente documento se describen los pasos necesarios para crear un modelo de aprendizaje automático en tiempo real en Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Introducción al aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real aún no está disponible para todos los usuarios. Esta función está en formato alfa y aún se está probando. Este documento está sujeto a cambios.

Para utilizar el aprendizaje automático en tiempo real, debe tener acceso a una organización aprovisionada con Adobe Experience Platform y [!DNL Data Science Workspace]. Además, debe tener un conjunto de datos completo para utilizarlo en la formación y la puntuación.

Las guías para el aprendizaje automático en tiempo real requieren una comprensión práctica de Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), ciencia de datos y aprendizaje automático.

**Términos clave:**

- **DSL:** Idioma específico del dominio.
- **Edge:** El servicio de puntuación de aprendizaje automático en tiempo real se puede ejecutar en clústeres de Edge más cerca de sus activaciones y aplicaciones.
- **Concentrador:** El alfa actual está ejecutando el servicio de puntuación de aprendizaje automático en tiempo real en Adobe Experience Platform Hub mientras Experience Edge Network está en desarrollo.
- **Nodo:** Un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar mediante vínculos para formar un gráfico que represente una canalización XML. La tarea realizada por un nodo representa una operación en los datos de entrada, como una transformación de datos o esquemas o una inferencia de aprendizaje automático. El nodo genera el valor transformado o inferido en el nodo o nodos siguientes.

## Conjuntos de datos en Adobe Experience Platform

Para empezar a utilizar el aprendizaje automático en tiempo real, debe tener acceso a un conjunto de datos. Tiene la opción de utilizar un conjunto de datos externo y cargarlo en su [!DNL JupyterLab] o cree un nuevo conjunto de datos en Platform si aún no lo ha hecho.

>[!NOTE]
>
>Si ya tiene un conjunto de datos que desea utilizar, puede saltar a [Pasos siguientes](#next-steps).

### Uso de un conjunto de datos externo

Para obtener más información sobre el uso de un conjunto de datos externo, como cargar datos en la [!DNL JupyterLab] entorno, visite el tutorial en [análisis de los datos con portátiles](../jupyterlab/analyze-your-data.md#external-data).

### Crear un nuevo conjunto de datos

Para crear un nuevo conjunto de datos para utilizarlo en aprendizaje automático en tiempo real, necesita un esquema de datos para su conjunto de datos. A continuación, debe introducir los datos mediante el esquema que ha creado. Utilice los siguientes tutoriales para crear y rellenar un conjunto de datos para [!DNL Platform]:

- [Cree y rellene un conjunto de datos en la API](../../catalog/datasets/create.md)
- [Crear y rellenar un conjunto de datos en la interfaz de usuario](../../ingestion/tutorials/ingest-batch-data.md)

## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos para el aprendizaje automático en tiempo real, comience por seguir las [Guía del usuario del portátil de aprendizaje automático en tiempo real](./rtml-authoring-notebook.md) para aprender a crear y cargar un modelo ONNX en la tienda del modelo de aprendizaje automático en tiempo real.
