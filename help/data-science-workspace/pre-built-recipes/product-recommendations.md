---
keywords: Experience Platform;fórmula de recomendación de producto;Área de trabajo de ciencia de datos;temas populares;fórmulas;fórmula de precompilación
solution: Experience Platform
title: Fórmula de recomendación de producto
topic: overview
description: La fórmula Product Recommendations le permite ofrecer recomendaciones de productos personalizadas que se adaptan a las necesidades e intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle una visión detallada de los productos que pueden interesarle.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---


# Fórmula de recomendación de producto

La fórmula Product Recommendations le permite ofrecer recomendaciones de productos personalizadas que se adaptan a las necesidades e intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle una visión detallada de los productos que pueden interesarle.

## ¿Para quién se construye esta receta?

En la actualidad, un minorista puede oferta una multitud de productos, dando a sus clientes muchas opciones que también pueden dificultar la búsqueda de sus clientes. Debido a las limitaciones de tiempo y esfuerzo, es posible que los clientes no encuentren el producto que desean, lo que resulta en compras con un alto nivel de disonancia cognitiva o en compras.

## ¿Qué hace esta fórmula?

La fórmula Product Recommendations utiliza el aprendizaje automático para analizar las interacciones de un cliente con los productos en el pasado y generar una lista personalizada de las recomendaciones de productos de forma rápida y sencilla. Esto optimiza el proceso de descubrimiento de productos y elimina las búsquedas largas, improductivas e irrelevantes de sus clientes. Como resultado, la fórmula Product Recommendations puede mejorar la experiencia de compra general de un cliente, lo que conlleva una mayor participación y una mayor lealtad de la marca.

## ¿Cómo empiezo?

Puede comenzar siguiendo el tutorial de Adobe Experience Platform Lab (consulte el enlace de Lab más abajo). Este tutorial le mostrará cómo crear la fórmula de Product Recommendations en un bloc de notas de Jupyter siguiendo el flujo de trabajo [para fórmula](../jupyterlab/create-a-recipe.md) e implementando la fórmula en [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratorio: Predecir el futuro con el área de trabajo de ciencias de datos](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos de laboratorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Esquema de datos

Esta fórmula utiliza esquemas [XDM personalizados](../../xdm/schema/field-dictionary.md) para modelar los datos de entrada y salida:

### Esquema de datos de entrada

| Nombre del campo | Tipo |
--- | ---
| itemId | Cadena |
| interactiveType | Cadena |
| timestamp | Cadena |
| userId | Cadena |

### Esquema de datos de salida

| Nombre del campo | Tipo |
--- | ---
| recomendaciones | Cadena |
| userId | Número entero |

## Algoritmo

La fórmula Product Recommendations utiliza filtros colaborativos para generar una lista personalizada de las recomendaciones de productos para sus clientes. El filtrado colaborativo, a diferencia de un enfoque basado en contenido, no requiere información sobre un producto específico sino que más bien utiliza las preferencias históricas de un cliente en un conjunto de productos. Esta poderosa técnica de recomendación utiliza dos simples supuestos:
* Hay clientes con intereses similares y se pueden agrupar comparando sus comportamientos de compra y exploración.
* Es más probable que un cliente esté interesado en una recomendación basada en clientes similares en términos de su comportamiento de compra y exploración.

Este proceso se divide en dos pasos principales. En primer lugar, defina un subconjunto de clientes similares. Luego, dentro de ese conjunto, identifique características similares entre esos clientes para devolver una recomendación para el cliente de destinatario.