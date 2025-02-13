---
keywords: Experience Platform;guía para desarrolladores;Data Science Workspace;temas populares;aprendizaje automático en tiempo real;
solution: Experience Platform
title: Información general sobre el aprendizaje automático en tiempo real
description: El aprendizaje automático en tiempo real puede mejorar en gran medida la relevancia del contenido de su experiencia digital para los usuarios finales. Esto es posible aprovechando la inferencia en tiempo real y el aprendizaje continuo en el Edge Network Experience Platform.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# Resumen del aprendizaje automático en tiempo real (Alpha)

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real aún no está disponible para todos los usuarios. Esta función está en formato alfa y aún se está probando. Este documento está sujeto a cambios.

El aprendizaje automático en tiempo real puede mejorar en gran medida la relevancia del contenido de su experiencia digital para los usuarios finales. Esto es posible gracias a la inferencia en tiempo real y al aprendizaje continuo en [!DNL Experience Platform Edge Network].

Una combinación de cálculo optimizado tanto en el concentrador como en [!DNL Edge] reduce considerablemente la latencia que tradicionalmente se emplea para potenciar las experiencias hiperpersonalizadas que son relevantes y adaptables. Por lo tanto, el aprendizaje automático en tiempo real proporciona deducciones con una latencia increíblemente baja para la toma de decisiones sincrónica. Algunos ejemplos son la representación de contenido de página web personalizado o la aparición de una oferta o descuento para reducir la pérdida y aumentar las conversiones en una tienda web.

## Arquitectura de aprendizaje automático en tiempo real {#architecture}

Los siguientes diagramas proporcionan una descripción general de la arquitectura de aprendizaje automático en tiempo real. Actualmente, alfa tiene una versión más simplificada.

![arco alfa](../images/rtml/alpha-arch.png)

![Información general simplificada](../images/rtml/end-to-end-arch.png)

## Flujo de trabajo de aprendizaje automático en tiempo real

En el siguiente flujo de trabajo se describen los pasos y resultados típicos que implica la creación y utilización de un modelo de aprendizaje automático en tiempo real.

### Ingesta de datos y preparativos

Los datos se incorporan y transforman con el [!DNL Experience Data Model] (XDM) en Adobe Experience Platform. Estos datos se utilizan para la formación de modelos. Para obtener más información sobre XDM, visite la [descripción general de XDM](../../xdm/home.md).

### Creación

Cree un modelo de aprendizaje automático en tiempo real creándolo desde cero o trayéndolo como un modelo ONNX serializado y preformado en Adobe Experience Platform Jupyter Notebooks.

### Implementación

Implemente su modelo en [!DNL Edge Network] para crear un servicio de aprendizaje automático en tiempo real en la [!UICONTROL Galería de servicios] mediante el extremo de la API de predicción.

### Inferencia

Utilice el extremo de la API de REST de predicción para generar perspectivas de aprendizaje automático en tiempo real.

### envío

Los especialistas en marketing pueden definir segmentos y reglas que asignen puntuaciones de aprendizaje automático en tiempo real a las experiencias mediante Adobe Target. Esto permite mostrar a los visitantes del sitio web de su marca una experiencia hiper personalizada en la misma página o en la siguiente en tiempo real.

## Funcionalidad actual

El aprendizaje automático en tiempo real se encuentra actualmente en fase alfa. La funcionalidad que se describe a continuación está sujeta a cambios a medida que hay más funciones y nodos disponibles.

>[!NOTE]
>
> Limitaciones del Alpha:
> - Actualmente, solo se admiten modelos basados en ONNX.
> - Las funciones utilizadas en los nodos no se pueden serializar. Por ejemplo, una función lambda utilizada en un nodo Pandas.
> - Hay una suspensión de 20 segundos después de que la implementación de [!DNL Edge] se realice manualmente.
> - Para el aprendizaje profundo, los datos deben enviarse de tal manera que cuando se llame a `df.values`, devuelva una matriz que sea aceptable para el modelo DL. Esto se debe a que el nodo de puntuación del modelo ONNX utiliza `df.values` y envía la salida para puntuar con respecto al modelo.


### Características:

| | Alpha (mayo) |
| --- | --- |
| **Funcionalidades** | : con la plantilla del bloc de notas RTML, cree, pruebe e implemente un modelo de aprendizaje automático personalizado. <br>: compatibilidad con la importación de modelos de aprendizaje automático formados previamente. <br> - SDK de aprendizaje automático en tiempo real. <br>: conjunto inicial de nodos de creación. <br>: implementado en Adobe Experience Platform Hub. |
| **Disponibilidad** | América del Norte |
| **Nodos de creación** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Tiempos de ejecución de puntuación** | ONNX |

## Pasos siguientes

Puede empezar por seguir la guía de [introducción](./getting-started.md). Esta guía le explica cómo configurar todos los requisitos previos necesarios para crear un modelo de aprendizaje automático en tiempo real.
