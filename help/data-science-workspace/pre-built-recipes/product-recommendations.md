---
keywords: Experience Platform;fórmula de recomendación de producto;Data Science Workspace;temas populares;fórmulas;fórmula de precompilación
solution: Experience Platform
title: Fórmula de recomendación de productos
description: La fórmula de recomendaciones de productos le permite proporcionar recomendaciones de productos personalizadas que se adaptan a las necesidades y los intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle insight sobre qué productos pueden interesarle.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# Fórmula de recomendación de productos

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

La fórmula de recomendaciones de productos le permite proporcionar recomendaciones de productos personalizadas que se adaptan a las necesidades y los intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle insight sobre qué productos pueden interesarle.

## ¿Para quién está diseñada esta receta?

En la actualidad, una retailer puede ofrecer una multitud de productos, ofreciendo a sus clientes muchas opciones que también pueden dificultar la búsqueda. Debido a restricciones de tiempo y esfuerzo, es posible que los clientes no encuentren el producto que desean, lo que resulta en compras con un alto nivel de disonancia cognitiva o ninguna compra en absoluto.

## ¿Qué hace esta receta?

La fórmula Recomendaciones de productos utiliza el aprendizaje automático para analizar las interacciones de un cliente con productos en el pasado y generar una lista personalizada de recomendaciones de productos de forma rápida y sencilla. Esto optimiza el proceso de descubrimiento de productos y elimina las búsquedas largas, improductivas e irrelevantes para sus clientes. Como resultado, la fórmula de Recomendaciones de productos puede mejorar la experiencia de compra general de un cliente, lo que produce una mayor participación y una lealtad de marca más fuerte.

## ¿Cómo empiezo?

Puede empezar siguiendo el tutorial de Adobe Experience Platform Lab (consulte el vínculo Lab a continuación). Este tutorial le mostrará cómo crear la fórmula de recomendaciones de productos en un Jupyter Notebook siguiendo el flujo de trabajo de [bloc de notas a fórmula](../jupyterlab/create-a-model.md) e implementando la fórmula en [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratorio: predecir el futuro con Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos de laboratorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Esquema de datos

Esta fórmula usa [esquemas XDM](../../xdm/schema/field-dictionary.md) personalizados para modelar los datos de entrada y salida:

### Esquema de datos de entrada

| Nombre del campo | Tipo |
| --- | --- |
| itemId | Cadena |
| interactionType | Cadena |
| timestamp | Cadena |
| userId | Cadena |

### Esquema de datos de salida

| Nombre del campo | Tipo |
| --- | --- |
| Recommendations | Cadena |
| userId | Entero |

## Algoritmo

La fórmula de Recomendaciones de productos utiliza el filtrado colaborativo para generar una lista personalizada de recomendaciones de productos para sus clientes. El filtrado colaborativo, a diferencia de un enfoque basado en contenido, no requiere información sobre un producto específico, sino que utiliza las preferencias históricas de un cliente en un conjunto de productos. Esta potente técnica de recomendación utiliza dos suposiciones simples:

* Hay clientes con intereses similares y pueden agruparse comparando sus comportamientos de compra y de navegación.
* Es más probable que un cliente esté interesado en una recomendación basada en clientes similares en términos de su comportamiento de compra y navegación.

Este proceso se divide en dos pasos principales. En primer lugar, defina un subconjunto de clientes similares. A continuación, dentro de ese conjunto, identifique funciones similares entre esos clientes para devolver una recomendación para el cliente objetivo.
