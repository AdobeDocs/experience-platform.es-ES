---
keywords: Experience Platform;guía para desarrolladores;Área de trabajo de ciencia de datos;temas populares;Aprendizaje automático en tiempo real;
solution: Experience Platform
title: Introducción al aprendizaje automático en tiempo real
topic: Getting started
description: El siguiente documento describe los pasos necesarios para crear un modelo de aprendizaje automático en tiempo real en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Introducción al aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

Para utilizar el aprendizaje automático en tiempo real, debe tener acceso a una organización aprovisionada con Adobe Experience Platform y [!DNL Data Science Workspace]. Además, necesita disponer de un conjunto de datos completo para su uso en la formación y la puntuación.

Las guías para aprendizaje automático en tiempo real requieren una comprensión práctica de Python 3, [Equipos portátiles Jupyter](../jupyterlab/overview.md), ciencia de datos y aprendizaje automático.

**Términos clave:**

- **DSL:Idioma específico** del dominio.
- **Edge: el servicio de puntuación de aprendizaje automático en tiempo** real se puede ejecutar en clústeres de Edge más cercanos a sus activaciones y aplicaciones.
- **Hub:** El alfa actual ejecuta el servicio de puntuación de aprendizaje automático en tiempo real en Adobe Experience Platform Hub mientras que Experience Edge Network está en desarrollo.
- **Nodo:** Un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar mediante vínculos para formar un gráfico que represente una canalización ML. La tarea que realiza un nodo representa una operación en datos de entrada, como una transformación de datos o esquemas, o una inferencia de aprendizaje automático. El nodo envía el valor transformado o inferido a los nodos siguientes.

## Conjuntos de datos en Adobe Experience Platform

Para realizar inicios mediante aprendizaje automático en tiempo real, debe tener acceso a un conjunto de datos. Tiene la opción de usar un conjunto de datos externo y cargarlo en su entorno [!DNL JupyterLab] o crear un nuevo conjunto de datos dentro de la plataforma si aún no lo ha hecho.

>[!NOTE]
>
>Si ya tiene un conjunto de datos que desea utilizar, puede saltar a [Próximos pasos](#next-steps).

### Usar un conjunto de datos externo

Para obtener más información sobre el uso de un conjunto de datos externo, como cargar datos en el entorno [!DNL JupyterLab], visite el tutorial sobre [análisis de datos mediante blocs de notas](../jupyterlab/analyze-your-data.md#external-data).

### Crear un nuevo conjunto de datos

Para crear un nuevo conjunto de datos para utilizarlo en el aprendizaje automático en tiempo real, necesita un esquema de datos para el conjunto de datos. A continuación, debe ingestar los datos con el esquema que ha creado. Utilice los siguientes tutoriales para crear y rellenar un conjunto de datos para [!DNL Platform]:

- [Creación y rellenado de un conjunto de datos en la API](../../catalog/datasets/create.md)
- [Creación y rellenado de un conjunto de datos en la interfaz de usuario](../../ingestion/tutorials/ingest-batch-data.md)

## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos para el aprendizaje automático en tiempo real, siga el inicio de la [guía del usuario del bloc de notas de aprendizaje automático en tiempo real](./rtml-authoring-notebook.md) para aprender a crear y cargar un modelo ONNX en el almacén modelo de aprendizaje automático en tiempo real.

