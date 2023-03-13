---
keywords: Experience Platform;fórmula de compra de producto;espacio de trabajo de ciencia de datos;temas populares;recetas;receta previa a la compilación
solution: Experience Platform
title: Fórmula de predicción de compra de productos
description: 'La fórmula de predicción de compra de productos le permite predecir la probabilidad de un determinado tipo de evento de compra de cliente: una compra de producto, por ejemplo.'
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 7%

---

# Fórmula de predicción de compra de productos

La fórmula de predicción de compra de productos le permite predecir la probabilidad de un determinado tipo de evento de compra de cliente: una compra de producto, por ejemplo.

![](../images/pre-built-recipes/ppp_bigpicture.png)

El siguiente documento responderá preguntas como las siguientes:
* ¿Para quién está diseñada esta receta?
* ¿Qué hace esta receta?

## ¿Para quién está diseñada esta receta?

Su marca busca impulsar las ventas trimestrales para su línea de productos a través de promociones efectivas y dirigidas a sus clientes. Sin embargo, no todos los clientes son iguales y usted quiere el valor de su dinero. ¿A quién se dirige? ¿Cuáles de sus clientes tienen más probabilidades de responder sin que su promoción resulte intrusiva? ¿Cómo personalizas tus promociones para cada cliente? ¿En qué canales debería confiar y cuándo debería enviar promociones?

## ¿Qué hace esta receta?

La fórmula de predicción de compra de productos utiliza el aprendizaje automático para predecir el comportamiento de compra de los clientes. Para ello, aplica un clasificador de bosque aleatorio personalizado y un modelo de datos de experiencia (XDM) de dos niveles para predecir la probabilidad de un evento de compra. El modelo utiliza datos de entrada que incorporan información de perfil del cliente e historial de compras anterior y toma por defecto parámetros de configuración predeterminados determinados por nuestros científicos de datos para mejorar la precisión predictiva.

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

En primer lugar, el conjunto de datos de aprendizaje en *ProductPrediction* se ha cargado el esquema. A partir de aquí, el modelo se entrena con una [clasificador de bosque aleatorio](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). El clasificador de bosque aleatorio es un tipo de algoritmo ensamblado que hace referencia a un algoritmo que combina varios algoritmos para obtener un rendimiento predictivo mejorado. La idea detrás del algoritmo es que el clasificador de bosque aleatorio construye múltiples árboles de decisión y los combina para crear una predicción más precisa y estable.

Este proceso comienza con la creación de un conjunto de árboles de decisión que selecciona aleatoriamente subconjuntos de datos de formación. Después, se promedia el resultado de cada árbol de decisión.
