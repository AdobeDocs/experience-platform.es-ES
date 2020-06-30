---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Fórmula de recomendación de producto
topic: overview
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 3%

---


# Fórmula de recomendación de producto

La fórmula de Recomendaciones de productos le permite ofrecer recomendaciones de productos personalizadas que se adaptan a las necesidades e intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle una visión detallada de los productos que pueden interesarle.

## ¿Para quién se construye esta receta?

En la actualidad, un minorista puede oferta una multitud de productos, dando a sus clientes muchas opciones que también pueden dificultar la búsqueda de sus clientes. Debido a las limitaciones de tiempo y esfuerzo, es posible que los clientes no encuentren el producto que desean, lo que resulta en compras con un alto nivel de disonancia cognitiva o en compras.

## ¿Qué hace esta fórmula?

La fórmula de Recomendaciones de productos utiliza el aprendizaje automático para analizar las interacciones de un cliente con los productos en el pasado y generar una lista personalizada de las recomendaciones de productos de forma rápida y sencilla. Esto optimiza el proceso de descubrimiento de productos y elimina las búsquedas largas, improductivas e irrelevantes de sus clientes. Como resultado, la fórmula de Recomendaciones de productos puede mejorar la experiencia de compra general de un cliente, lo que conlleva una mayor participación y una mayor lealtad de la marca.

## ¿Cómo empiezo?

Puede comenzar siguiendo el tutorial de Adobe Experience Platform Lab (consulte el enlace de laboratorio más abajo). Este tutorial le mostrará cómo crear la fórmula de Recomendaciones de productos en un bloc de notas de Jupyter siguiendo el flujo de trabajo del [bloc de notas para la fórmula](../jupyterlab/create-a-recipe.md) e implementando la fórmula en [!DNL Experience Platform][!DNL Data Science Workspace].

* [Laboratorio: Predecir el futuro con el área de trabajo de ciencias de datos](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos de laboratorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## esquema de datos

Esta fórmula utiliza esquemas [](../../xdm/schema/field-dictionary.md) XDM personalizados para modelar los datos de entrada y salida:

### esquema de datos de entrada

| Nombre del campo | Tipo |
--- | ---
| itemId | Cadena |
| interactiveType | Cadena |
| timestamp | Cadena |
| userId | Cadena |

### esquema de datos de salida

| Nombre del campo | Tipo |
--- | ---
| recomendaciones | Cadena |
| userId | Número entero |

## Algoritmo

La fórmula de Recomendaciones de productos utiliza filtros colaborativos para generar una lista personalizada de las recomendaciones de productos para sus clientes. El filtrado colaborativo, a diferencia de un enfoque basado en contenido, no requiere información sobre un producto específico sino que más bien utiliza las preferencias históricas de un cliente en un conjunto de productos. Esta poderosa técnica de recomendación utiliza dos simples supuestos:
* Hay clientes con intereses similares y se pueden agrupar comparando sus comportamientos de compra y exploración.
* Es más probable que un cliente esté interesado en una recomendación basada en clientes similares en términos de su comportamiento de compra y exploración.

Este proceso se divide en dos pasos principales. En primer lugar, defina un subconjunto de clientes similares. Luego, dentro de ese conjunto, identifique características similares entre esos clientes para devolver una recomendación para el cliente de destinatario.