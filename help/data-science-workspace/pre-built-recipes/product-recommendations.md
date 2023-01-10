---
keywords: Experience Platform;fórmula de recomendación de producto;Data Science Workspace;temas populares;fórmulas;fórmula de precompilación
solution: Experience Platform
title: Fórmula de recomendación de producto
description: La fórmula de Product Recommendations le permite ofrecer recomendaciones de productos personalizadas que se adaptan a las necesidades y los intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle información sobre qué productos puede interesarle.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# Fórmula de recomendación de producto

La fórmula de Product Recommendations le permite ofrecer recomendaciones de productos personalizadas que se adaptan a las necesidades y los intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle información sobre qué productos puede interesarle.

## ¿Para quién se ha creado esta receta?

En la actualidad, un minorista puede ofrecer una multitud de productos, ofreciendo a sus clientes muchas opciones que también pueden dificultar la búsqueda de sus clientes. Debido a las limitaciones de tiempo y esfuerzo, es posible que los clientes no encuentren el producto que desean, lo que resulta en compras con un alto nivel de disonancia cognitiva o en ninguna compra.

## ¿Qué hace esta receta?

La fórmula de Product Recommendations utiliza el aprendizaje automático para analizar las interacciones de un cliente con productos del pasado y generar una lista personalizada de recomendaciones de productos de forma rápida y sencilla. Esto optimiza el proceso de descubrimiento de productos y elimina las búsquedas largas, improductivas e irrelevantes para sus clientes. Como resultado, la fórmula de Product Recommendations puede mejorar la experiencia de compra general de un cliente, lo que aumenta la participación y la lealtad de marca.

## ¿Cómo empiezo?

Para empezar, siga el tutorial de Adobe Experience Platform Lab (consulte el vínculo de Lab que aparece a continuación). Este tutorial le muestra cómo crear la fórmula de Product Recommendations en un Jupyter Notebook siguiendo las [portátil a fórmula](../jupyterlab/create-a-model.md) flujo de trabajo e implementación de la fórmula en [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratorio: Predecir el futuro con Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos de laboratorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Esquema de datos

Esta fórmula utiliza [Esquemas XDM](../../xdm/schema/field-dictionary.md) para modelar los datos de entrada y salida:

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
| recommendations | Cadena |
| userId | Número entero |

## Algoritmo

La fórmula de Product Recommendations utiliza filtros de colaboración para generar una lista personalizada de recomendaciones de productos para sus clientes. El filtrado colaborativo, a diferencia de un enfoque basado en contenido, no requiere información sobre un producto específico sino que utiliza las preferencias históricas de un cliente en un conjunto de productos. Esta potente técnica de recomendación utiliza dos supuestos simples:
* Hay clientes con intereses similares y se pueden agrupar comparando sus comportamientos de compra y navegación.
* Es más probable que un cliente esté interesado en una recomendación basada en clientes similares en términos de su comportamiento de compra y exploración.

Este proceso se divide en dos pasos principales. En primer lugar, defina un subconjunto de clientes similares. Luego, dentro de ese conjunto, identifique características similares entre esos clientes para devolver una recomendación para el cliente objetivo.
