---
keywords: Experience Platform;guía para desarrolladores;Data Science Workspace;temas populares;aprendizaje automático en tiempo real;
solution: Experience Platform
title: Información general sobre aprendizaje automático en tiempo real
topic-legacy: Overview
description: El aprendizaje automático en tiempo real puede mejorar considerablemente la relevancia del contenido de su experiencia digital para los usuarios finales. Esto es posible gracias al uso de inferencias en tiempo real y aprendizaje continuo en Experience Edge.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# Descripción general del aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real aún no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

El aprendizaje automático en tiempo real puede mejorar considerablemente la relevancia del contenido de su experiencia digital para los usuarios finales. Esto es posible aprovechando la inferenciación en tiempo real y el aprendizaje continuo en el [!DNL Experience Edge].

Una combinación de computación optimizada tanto en el Hub como en el [!DNL Edge] reduce drásticamente la latencia que tradicionalmente está involucrada en la generación de experiencias hiperpersonalizadas que son relevantes y responden. Por lo tanto, el aprendizaje automático en tiempo real proporciona inferencias con una latencia increíblemente baja para la toma de decisiones sincrónica. Algunos ejemplos son el procesamiento de contenido personalizado de una página web o el envío de una oferta o descuento para reducir la pérdida y aumentar las conversiones en una tienda web.

## Arquitectura de aprendizaje automático en tiempo real {#architecture}

Los siguientes diagramas proporcionan una visión general de la arquitectura de aprendizaje automático en tiempo real. Actualmente, alfa tiene una versión más simplificada.

![arco alfa](../images/rtml/alpha-arch.png)

![Información general simplificada](../images/rtml/end-to-end-arch.png)

## Flujo de trabajo de aprendizaje automático en tiempo real

El siguiente flujo de trabajo describe los pasos y resultados típicos involucrados en la creación y utilización de un modelo de aprendizaje automático en tiempo real.

### Ingesta de datos y preparaciones

Los datos se incorporan y transforman con [!DNL Experience Data Model] (XDM) en Adobe Experience Platform. Estos datos se utilizan para la formación de modelos. Para obtener más información sobre XDM, visite [Información general de XDM](../../xdm/home.md).

### Creación

Cree un modelo de aprendizaje automático en tiempo real creándolo desde cero o introduciéndolo como un modelo ONNX serializado previamente en Adobe Experience Platform Jupyter Notebooks.

### Implementación

Implemente el modelo en [!DNL Experience Edge] para crear un servicio de aprendizaje automático en tiempo real en [!UICONTROL Service Gallery] mediante el extremo de la API de predicción.

### Inferencia

Utilice el extremo de la API de REST de predicción para generar perspectivas de aprendizaje automático en tiempo real.

### Envío

Los especialistas en marketing pueden definir segmentos y reglas que asignen puntuaciones de aprendizaje automático en tiempo real a experiencias mediante Adobe Target. Esto permite que los visitantes del sitio web de su marca se muestren en tiempo real como una experiencia hiperpersonalizada de la misma página o de la página siguiente.

## Funcionalidad actual

El aprendizaje automático en tiempo real está actualmente en alfa. La funcionalidad descrita a continuación está sujeta a cambios a medida que hay más funciones y nodos disponibles.

>[!NOTE]
>
> Limitaciones alfa:
> - Actualmente, solo se admiten modelos basados en ONNX.
> - Las funciones utilizadas en los nodos no se pueden serializar. Por ejemplo, una función lambda utilizada en un nodo Pandas.
> - Hay una suspensión de 20 segundos después de que la implementación [!DNL Edge] se realice manualmente.
> - Para un aprendizaje profundo, los datos deben enviarse de tal manera que cuando se llama a `df.values` devuelvan un arreglo de discos que sea aceptable para su modelo DL. Esto se debe a que el nodo de puntuación del modelo ONNX utiliza `df.values` y envía la salida a la puntuación con respecto al modelo.



### Funcionalidades:

|  | Alfa (mayo) |
| --- | --- |
| **Funcionalidades** | - Uso de la plantilla de bloc de notas RTML, creación, prueba e implementación de un modelo de aprendizaje automático personalizado. <br> - Compatibilidad con la importación de modelos de aprendizaje automático preformados. <br> - SDK de aprendizaje automático en tiempo real. <br> : conjunto inicial de nodos de creación. <br> : se implementa en Adobe Experience Platform Hub. |
| **Disponibilidad** | América del Norte |
| **Creación de nodos** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Tiempos de ejecución de la puntuación** | ONNX |

## Pasos siguientes

Puede empezar por seguir la guía [introducción](./getting-started.md). Esta guía lo acompaña durante la configuración de todos los requisitos previos necesarios para crear un modelo de aprendizaje automático en tiempo real.
