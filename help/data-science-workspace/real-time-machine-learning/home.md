---
keywords: Experience Platform;guía para desarrolladores;Área de trabajo de ciencia de datos;temas populares;Aprendizaje automático en tiempo real;
solution: Experience Platform
title: Información general sobre aprendizaje automático en tiempo real
topic: Overview
description: El aprendizaje automático en tiempo real puede aumentar considerablemente la relevancia del contenido de su experiencia digital para los usuarios finales. Esto es posible gracias a la inferenciación en tiempo real y al aprendizaje continuo en Experience Edge.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---


# Información general sobre aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

El aprendizaje automático en tiempo real puede aumentar considerablemente la relevancia del contenido de su experiencia digital para los usuarios finales. Esto es posible gracias a la inferenciación en tiempo real y al aprendizaje continuo en [!DNL Experience Edge].

Una combinación de computación optimizada tanto en el concentrador como en el [!DNL Edge] reduce drásticamente la latencia que tradicionalmente está involucrada en la generación de experiencias hiperpersonalizadas que son relevantes y responden. Por lo tanto, el aprendizaje automático en tiempo real proporciona inferencias con una latencia increíblemente baja para la toma de decisiones sincrónica. Algunos ejemplos son el procesamiento de contenido personalizado de una página web o la aparición de una oferta o descuento para reducir la generación y aumentar las conversiones en una tienda web.

## Arquitectura de aprendizaje automático en tiempo real {#architecture}

Los siguientes diagramas proporcionan información general sobre la arquitectura de aprendizaje automático en tiempo real. Actualmente, alpha tiene una versión más simplificada.

![arco alfa](../images/rtml/alpha-arch.png)

![Visión general simplificada](../images/rtml/end-to-end-arch.png)

## Flujo de trabajo de aprendizaje automático en tiempo real

El flujo de trabajo siguiente describe los pasos y resultados típicos que conlleva la creación y utilización de un modelo de aprendizaje automático en tiempo real.

### Introducción y preparación de datos

Los datos se ingieren y transforman con el [!DNL Experience Data Model] (XDM) en Adobe Experience Platform. Estos datos se utilizan para la formación de modelos. Para obtener más información sobre XDM, visite la [información general de XDM](../../xdm/home.md).

### Creación

Cree un modelo de aprendizaje automático en tiempo real creándolo desde cero o incorporándolo como un modelo ONNX serializado previamente capacitado en equipos portátiles Adobe Experience Platform Jupyter.

### Implementación

Implemente el modelo en [!DNL Experience Edge] para crear un servicio de aprendizaje automático en tiempo real en la [!UICONTROL Galería de servicios] mediante el extremo de la API de predicción.

### Inferencia

Utilice el punto final de la API de REST de predicción para generar perspectivas de aprendizaje automático en tiempo real.

### Envío

Los especialistas en marketing pueden definir segmentos y reglas que asignen puntuaciones de aprendizaje automático en tiempo real a experiencias mediante Adobe Target. Esto permite que visitantes del sitio web de su marca se muestren en tiempo real como una experiencia hiperpersonalizada de la misma página o de la página siguiente.

## Funcionalidad actual

El aprendizaje automático en tiempo real se encuentra actualmente en alfa. La funcionalidad que se describe a continuación está sujeta a cambios a medida que más funciones y nodos están disponibles.

>[!NOTE]
>
> Limitaciones alfa:
> - Actualmente, solo se admiten modelos basados en ONNX.
> - Las funciones utilizadas en los nodos no se pueden serializar. Por ejemplo, una función lambda utilizada en un nodo Pandas.
> - Hay una suspensión de 20 segundos después de que la implementación [!DNL Edge] se realice manualmente.
> - Para el aprendizaje profundo, los datos deben enviarse de manera tal que cuando se llama `df.values` devuelve un arreglo de discos aceptable para su modelo DL. Esto se debe a que el nodo de puntuación del modelo ONNX utiliza `df.values` y envía la salida para realizar una puntuación con respecto al modelo.



### Funcionalidades:

|  | Alfa (mayo) |
| --- | --- |
| **Funcionalidades** | - Mediante la plantilla de bloc de notas RTML, cree, pruebe e implemente un modelo de aprendizaje automático personalizado. <br> - Soporte para importar modelos de aprendizaje automático preentrenados. <br> - SDK de aprendizaje automático en tiempo real. <br> - Conjunto inicial de nodos de creación. <br> - Implementado en Adobe Experience Platform Hub. |
| **Disponibilidad** | América del Norte |
| **Creación de nodos** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Tiempos de ejecución de puntuación** | ONNX |

## Pasos siguientes

Puede empezar por seguir la guía [introducción](./getting-started.md). Esta guía lo acompaña durante la configuración de todos los requisitos previos necesarios para crear un modelo de aprendizaje automático en tiempo real.

