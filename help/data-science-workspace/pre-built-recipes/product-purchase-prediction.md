---
keywords: Experience Platform;fórmula de compra de producto;Área de trabajo de ciencia de datos;temas populares;fórmulas;fórmula de precompilación
solution: Experience Platform
title: Fórmula de predicción de compra de productos
topic: overview
description: La fórmula Predicción de compra de productos permite predecir la probabilidad de un determinado tipo de evento de compra del cliente, por ejemplo, una compra de producto.
translation-type: tm+mt
source-git-commit: f4095a90ff70e8d054bae4f3b0f884552ffd30df
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---


# Fórmula de predicción de compra del producto

La fórmula Predicción de compra de productos permite predecir la probabilidad de un determinado tipo de evento de compra del cliente, por ejemplo, una compra de producto.

![](../images/pre-built-recipes/ppp_bigpicture.png)

El siguiente documento responderá preguntas como:
* ¿Para quién se construye esta receta?
* ¿Qué hace esta fórmula?

## ¿Para quién se construye esta receta?

Su marca busca aumentar las ventas trimestrales de su línea de productos a través de promociones efectivas y dirigidas a sus clientes. Sin embargo, no todos los clientes son iguales y usted quiere el valor de su dinero. ¿A quién destinatarios? ¿Cuál de los clientes tiene más probabilidades de responder sin que la promoción resulte invasiva? ¿Cómo personaliza las promociones para cada cliente? ¿En qué canales debe confiar y cuándo debe enviar promociones?

## ¿Qué hace esta fórmula?

La fórmula Predicción de compra de productos utiliza aprendizaje automático para predecir el comportamiento de compra de los clientes. Para ello, aplica un clasificador de bosque aleatorio personalizado y un Modelo de datos de experiencia (XDM) de dos niveles para predecir la probabilidad de un evento de compra. El modelo utiliza datos de entrada que incorporan la información de perfil del cliente y el historial de compras pasado y establece de forma predeterminada parámetros de configuración predeterminados determinados por nuestros Data Scientists para mejorar la precisión predictiva.

## Esquema de datos

Esta fórmula utiliza [esquemas XDM](../../xdm/home.md) para modelar los datos. El esquema utilizado para esta fórmula se muestra a continuación:

| Nombre del campo | Tipo |
--- | ---
| userId | Cadena |
| genderRatio | Número |
| ageY | Número |
| ageM | Número |
| optinEmail | Booleano |
| optinMobile | Booleano |
| optinAddress | Booleano |
| created | Número entero |
| totalOrders | Número |
| totalItems | Número |
| orderDate1 | Número |
| ShippingDate1 | Número |
| totalPrice1 | Número |
| tax1 | Número |
| orderDate2 | Número |
| ShippingDate2 | Número |
| totalPrice2 | Número |


## Algoritmo

En primer lugar, se carga el conjunto de datos de capacitación en el esquema *ProductPrediction*. Desde aquí, el modelo se entrena usando un [clasificador de bosque aleatorio](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). El clasificador de bosque aleatorio es un tipo de algoritmo ensamblado que hace referencia a un algoritmo que combina varios algoritmos para obtener un rendimiento predictivo mejorado. La idea detrás del algoritmo es que el clasificador forestal aleatorio construya varios árboles de decisión y los combine para crear una predicción más precisa y estable.

Este proceso tiene el inicio de crear un conjunto de árboles de decisiones que selecciona aleatoriamente subconjuntos de datos de capacitación. Después, se promedian los resultados de cada árbol de decisiones.