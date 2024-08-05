---
keywords: Experience Platform; guía de desarrolladores; Data Science Espacio de trabajo; temas populares; Aprendizaje automático en tiempo real;
solution: Experience Platform
title: Introducción con el aprendizaje automático en tiempo real
description: En el siguiente documento se describen los pasos necesarios para crear un modelo de aprendizaje automático en tiempo real en Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Introducción al aprendizaje automático en tiempo real (Alpha)

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta característica está en alfa y aún se está probando. Este documento está sujeto a cambios.

Para utilizar el aprendizaje automático en tiempo real, debe tener acceso a una organización aprovisionada con Adobe Experience Platform y [!DNL Data Science Workspace]. Además, debe tener un conjunto de datos completo para usar en aprendizaje y puntuación.

Las guías para el aprendizaje automático en tiempo real requieren una comprensión práctica de Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), ciencia de datos y aprendizaje automático.

**Términos clave:**

- **DSL:** Idioma específico del dominio.
- **Edge:** El servicio de puntuación de aprendizaje automático en tiempo real se puede ejecutar en clústeres de Edge más cercanos a sus activaciones y aplicaciones.
- **Hub:** el alfa actual ejecuta el servicio de puntuación de aprendizaje automático en tiempo real en el Adobe Experience Platform Hub mientras Edge Network está en desarrollo.
- **Nodo:** Un nodo es la unidad fundamental de los gráficos que se forman. Cada nodo realiza una tarea específica y se puede encadenar mediante vínculos para formar un gráfico que represente una canalización XML. El tarea realizado por un nodo representa una operación en datos de entrada, como un transformación de datos o esquema, o una inferencia de aprendizaje automático. El nodo genera el valor transformado o inferido en los nodo siguientes.

## Conjuntos de datos en Adobe Experience Platform

Para inicio con el aprendizaje automático en tiempo real, debe tener acceso a un conjunto de datos. Tiene la opción de utilizar un conjunto de datos externo y cargar a su [!DNL JupyterLab] entorno o crear un nuevo conjunto de datos dentro de Platform si aún no lo ha hecho.

>[!NOTE]
>
>Si ya tiene un conjunto de datos desea utilizar, puede omitir Siguiente [pasos](#next-steps).

### Utilizar un conjunto de datos externo

Para obtener más información sobre el uso de un conjunto de datos externo, como cargar datos en su [!DNL JupyterLab] entorno, visita la tutorial sobre [el análisis de sus datos con blocs de notas](../jupyterlab/analyze-your-data.md#external-data).

### Crear una nueva conjunto de datos

Para crear un nuevo conjunto de datos para su uso en Aprendizaje automático en tiempo real, necesita un esquema de datos para su conjunto de datos. A continuación, debe introducir los datos mediante el esquema que ha creado. Utilice los siguientes tutoriales para crear y rellenar un conjunto de datos para [!DNL Platform]:

- [Cree y rellene un conjunto de datos en la API](../../catalog/datasets/create.md)
- [Crear y rellenar un conjunto de datos en el IU](../../ingestion/tutorials/ingest-batch-data.md)

## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos para el aprendizaje automático en tiempo real, inicio siguiendo el bloc de notas de [aprendizaje automático en tiempo real usuario guía](./rtml-authoring-notebook.md) aprender a crear y cargar un modelo ONNX al modelo de aprendizaje automático en tiempo real tienda.
