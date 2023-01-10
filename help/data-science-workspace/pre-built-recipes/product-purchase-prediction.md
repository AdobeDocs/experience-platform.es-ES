---
keywords: Experience Platform;fórmula de compra de producto;Data Science Workspace;temas populares;fórmulas;fórmula de precompilación
solution: Experience Platform
title: Fórmula de predicción de compra de producto
description: 'La fórmula de Predicción de compra de productos permite predecir la probabilidad de un determinado tipo de evento de compra de clientes: una compra de producto, por ejemplo.'
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 7%

---

# Fórmula de predicción de compra de productos

La fórmula de Predicción de compra de productos permite predecir la probabilidad de un determinado tipo de evento de compra de clientes: una compra de producto, por ejemplo.

![](../images/pre-built-recipes/ppp_bigpicture.png)

El siguiente documento responderá preguntas como:
* ¿Para quién se ha creado esta receta?
* ¿Qué hace esta receta?

## ¿Para quién se ha creado esta receta?

Su marca busca aumentar las ventas trimestrales de su línea de productos mediante promociones efectivas y específicas para sus clientes. Sin embargo, no todos los clientes son iguales y usted quiere el valor de su dinero. ¿A quién se dirige? ¿Cuál de sus clientes tiene más probabilidades de responder sin encontrar la promoción intrusiva? ¿Cómo personaliza las promociones con cada cliente? ¿En qué canales debe confiar y cuándo debe enviar promociones?

## ¿Qué hace esta receta?

La fórmula de predicción de compra de productos utiliza aprendizaje automático para predecir el comportamiento de compra de los clientes. Para ello, aplica un clasificador de bosque aleatorio personalizado y un Modelo de datos de experiencia (XDM) de dos niveles para predecir la probabilidad de un evento de compra. El modelo utiliza datos de entrada que incorporan la información de perfil del cliente y el historial de compras anterior y establece de forma predeterminada parámetros de configuración predeterminados determinados determinados por nuestros científicos de datos para mejorar la precisión predictiva.

## Esquema de datos

Esta fórmula utiliza [Esquemas XDM](../../xdm/home.md) para modelar los datos. El esquema utilizado para esta fórmula se muestra a continuación:

| Nombre del campo | Tipo |
| --- | --- |
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
| shippingDate1 | Número |
| totalPrice1 | Número |
| tax1 | Número |
| orderDate2 | Número |
| shippingDate2 | Número |
| totalPrice2 | Número |


## Algoritmo

En primer lugar, el conjunto de datos de formación en la variable *ProductPrediction* se ha cargado el esquema. Desde aquí, el modelo se entrena usando un [clasificador de bosque aleatorio](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). El clasificador de bosque aleatorio es un tipo de algoritmo ensamblado que hace referencia a un algoritmo que combina varios algoritmos para obtener un rendimiento predictivo mejorado. La idea detrás del algoritmo es que el clasificador de bosques aleatorio crea varios árboles de decisión y los combina para crear una predicción más precisa y estable.

Este proceso comienza con la creación de un conjunto de árboles de decisión que seleccionan aleatoriamente subconjuntos de datos de capacitación. Después, se calcula el promedio de los resultados de cada árbol de decisiones.
