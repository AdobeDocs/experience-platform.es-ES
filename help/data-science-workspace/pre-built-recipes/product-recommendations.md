---
keywords: Experience Platform;fórmula de recomendación de producto;espacio de trabajo de ciencia de datos;temas populares;recetas;fórmula de precompilación
solution: Experience Platform
title: Fórmula de recomendación de productos
description: La fórmula de Product Recommendations le permite ofrecer recomendaciones de productos personalizadas adaptadas a las necesidades y los intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle una perspectiva sobre qué productos pueden interesarle.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# Fórmula de recomendación de productos

La fórmula de Product Recommendations le permite ofrecer recomendaciones de productos personalizadas adaptadas a las necesidades y los intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle una perspectiva sobre qué productos pueden interesarle.

## ¿Para quién está diseñada esta receta?

En la actualidad, un minorista puede ofrecer una multitud de productos, dando a sus clientes muchas opciones que también pueden dificultar la búsqueda de sus clientes. Debido a restricciones de tiempo y esfuerzo, es posible que los clientes no encuentren el producto que desean, lo que resulta en compras con un alto nivel de disonancia cognitiva o ninguna compra en absoluto.

## ¿Qué hace esta receta?

La fórmula de Product Recommendations utiliza el aprendizaje automático para analizar las interacciones de un cliente con productos en el pasado y generar una lista personalizada de recomendaciones de productos de forma rápida y sencilla. Esto optimiza el proceso de descubrimiento de productos y elimina las búsquedas largas, improductivas e irrelevantes para sus clientes. Como resultado, la fórmula de Recommendations de productos puede mejorar la experiencia de compra general de un cliente, lo que produce una mayor participación y una lealtad de marca más sólida.

## ¿Cómo empiezo?

Puede empezar siguiendo el tutorial de Adobe Experience Platform Lab (consulte el vínculo Lab a continuación). Este tutorial muestra cómo crear la fórmula de Product Recommendations en un Jupyter Notebook siguiendo las [bloc de notas a fórmula](../jupyterlab/create-a-model.md) flujo de trabajo e implementación de la fórmula en [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratorio: predecir el futuro con Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos de laboratorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Esquema de datos

Esta fórmula utiliza la personalización [Esquemas XDM](../../xdm/schema/field-dictionary.md) para modelar los datos de entrada y salida:

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
| userId | Número entero |

## Algoritmo

La fórmula de Product Recommendations utiliza el filtrado colaborativo para generar una lista personalizada de recomendaciones de productos para sus clientes. El filtrado colaborativo, a diferencia de un enfoque basado en contenido, no requiere información sobre un producto específico, sino que utiliza las preferencias históricas de un cliente en un conjunto de productos. Esta potente técnica de recomendación utiliza dos suposiciones simples:
* Hay clientes con intereses similares y pueden agruparse comparando sus comportamientos de compra y de navegación.
* Es más probable que un cliente esté interesado en una recomendación basada en clientes similares en términos de su comportamiento de compra y navegación.

Este proceso se divide en dos pasos principales. En primer lugar, defina un subconjunto de clientes similares. A continuación, dentro de ese conjunto, identifique funciones similares entre esos clientes para devolver una recomendación para el cliente objetivo.
