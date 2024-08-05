---
keywords: Experience Platform; recomendación fórmula del producto; Data Science Espacio de trabajo; temas populares; Recetas; Pre versión fórmula
solution: Experience Platform
title: Fórmula de recomendación de productos
description: La Recommendations fórmula productos le permite proporcionar recomendaciones de productos personalizadas que se adaptan a las necesidades e intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle conocimiento sobre qué productos pueden interesarle.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# recomendación fórmula del producto

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

La Recommendations fórmula productos le permite proporcionar recomendaciones de productos personalizadas que se adaptan a las necesidades e intereses de sus clientes. Con un modelo de predicción preciso, el historial de compras de un cliente puede proporcionarle conocimiento sobre qué productos pueden interesarle.

## ¿Para quién está diseñado este fórmula?

En la actualidad, un minorista puede oferta una multitud de productos, dando a sus clientes muchas opciones que también pueden obstaculizar a sus clientes búsqueda. Debido a las limitaciones de tiempo y esfuerzo, los clientes pueden no encontrar el producto que desean, lo que resulta en compras con un alto nivel de disonancia cognitiva o ninguna compra en absoluto.

## ¿Qué hace este fórmula?

El Recommendations fórmula de productos utiliza el aprendizaje automático para analizar las interacciones de un cliente con los productos en el pasado y generar un lista personalizado de recomendaciones de productos de forma rápida y sin esfuerzo. Esto optimiza el proceso de descubrimiento de productos y elimina las búsquedas largas, improductivas e irrelevantes para sus clientes. Como resultado, el Recommendations fórmula del producto puede mejorar el experiencia de compra general de un cliente, lo que lleva a una mayor participación y una mayor lealtad de marca.

## ¿Qué debo hacer para comenzar?

Puede comenzar siguiendo el tutorial de laboratorio de Adobe Experience Platform (consulte el vincular de laboratorio a continuación). Este tutorial le mostrará cómo crear el Recommendations fórmula de producto en un bloc de notas de Jupyter siguiendo el [bloc de notas para fórmula](../jupyterlab/create-a-model.md) flujo de trabajo e implementando el fórmula en [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Laboratorio: Predecir el futuro con la ciencia de datos Espacio de trabajo](https://expleague.azureedge.net/labs/L777/index.html)
* [Recursos de laboratorio](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## esquema de datos

Este fórmula utiliza esquemas XDM personalizados [para modelar los datos de](../../xdm/schema/field-dictionary.md) entrada y salida:

### Datos de entrada esquema

| Nombre del campo | Tipo |
| --- | --- |
| Id. de elemento | Cadena |
| Tipo de interacción | Cadena |
| timestamp | Cadena |
| Id de usuario | Cadena |

### Output datos esquema

| Nombre del campo | Tipo |
| --- | --- |
| Recomendaciones | Cadena |
| Id de usuario | Entero |

## Algoritmo

El Recommendations fórmula de productos utiliza el filtrado colaborativo para generar un lista personalizado de recomendaciones de productos para sus clientes. El filtrado colaborativo, a diferencia de un enfoque basado en contenido, no requiere información sobre un producto específico, sino que utiliza las preferencias históricas de un cliente en un conjunto de productos. Esta poderosa técnica recomendación utiliza dos simples suposiciones:
* Hay clientes con intereses similares, que se pueden agrupar comparando sus comportamientos de compra y navegación.
* Es más probable que un cliente esté interesado en un recomendación basado en clientes similares en términos de su comportamiento de compra y navegación.

Este proceso se divide en dos pasos principales. En primer lugar, defina un subconjunto de clientes similares. Luego, dentro de ese conjunto, identifique características similares entre esos clientes para devolver un recomendación para el cliente destino.
