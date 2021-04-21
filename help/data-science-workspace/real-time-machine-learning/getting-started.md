---
keywords: Experience Platform;guía para desarrolladores;Data Science Workspace;temas populares;aprendizaje automático en tiempo real;
solution: Experience Platform
title: Introducción al aprendizaje automático en tiempo real
topic-legacy: Getting started
description: El siguiente documento describe los pasos necesarios para crear un modelo de aprendizaje automático en tiempo real en Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Introducción al aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real aún no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

Para utilizar el aprendizaje automático en tiempo real, debe tener acceso a una organización aprovisionada con Adobe Experience Platform y [!DNL Data Science Workspace]. Además, debe tener un conjunto de datos completo para utilizarlo en la formación y la puntuación.

Las guías para aprendizaje automático en tiempo real requieren una comprensión práctica de Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), ciencia de datos y aprendizaje automático.

**Términos clave:**

- **DSL:** Idioma específico del dominio.
- **Edge:** el servicio de puntuación de aprendizaje automático en tiempo real se puede ejecutar en clústeres de Edge más cercanos a sus activaciones y aplicaciones.
- **Hub:** el alfa actual está ejecutando el servicio de puntuación de aprendizaje automático en tiempo real en Adobe Experience Platform Hub mientras Experience Edge Network está en desarrollo.
- **Nodo:** un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar utilizando vínculos para formar un gráfico que represente una canalización ML. La tarea realizada por un nodo representa una operación en los datos de entrada, como una transformación de datos o esquema, o una inferencia de aprendizaje automático. El nodo envía el valor transformado o inferido a los nodos siguientes.

## Conjuntos de datos en Adobe Experience Platform

Para empezar a utilizar el aprendizaje automático en tiempo real, debe tener acceso a un conjunto de datos. Tiene la opción de usar un conjunto de datos externo y cargarlo en su entorno [!DNL JupyterLab] o crear un nuevo conjunto de datos dentro de Platform si aún no lo ha hecho.

>[!NOTE]
>
>Si ya tiene un conjunto de datos que desea utilizar, puede pasar a [Próximos pasos](#next-steps).

### Usar un conjunto de datos externo

Para obtener más información sobre el uso de un conjunto de datos externo, como la carga de datos en el entorno [!DNL JupyterLab], visite el tutorial sobre [análisis de los datos mediante blocs de notas](../jupyterlab/analyze-your-data.md#external-data).

### Crear un nuevo conjunto de datos

Para crear un nuevo conjunto de datos para utilizarlo en el aprendizaje automático en tiempo real, necesita un esquema de datos para el conjunto de datos. A continuación, debe introducir los datos mediante el esquema creado. Utilice los siguientes tutoriales para crear y rellenar un conjunto de datos para [!DNL Platform]:

- [Crear y rellenar un conjunto de datos en la API](../../catalog/datasets/create.md)
- [Crear y rellenar un conjunto de datos en la interfaz de usuario](../../ingestion/tutorials/ingest-batch-data.md)

## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos para el aprendizaje automático en tiempo real, comience por seguir la [Guía del usuario del bloc de notas de aprendizaje automático en tiempo real](./rtml-authoring-notebook.md) para aprender a crear y cargar un modelo ONNX en el almacén modelo de aprendizaje automático en tiempo real.
