---
keywords: Experience Platform; fórmula de compra de productos; Data Science Espacio de trabajo; temas populares; Recetas; Pre versión fórmula
solution: Experience Platform
title: Fórmula de predicción de compra de productos
description: El fórmula de predicción de compra de productos le permite predecir la probabilidad de un determinado tipo de Evento de compra de cliente, es decir, la compra de un producto, por instancia.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 5%

---

# Predicción de compra de productos fórmula

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

La fórmula de predicción de compra de productos le permite predecir la probabilidad de un determinado tipo de evento de compra de cliente: una compra de producto, por ejemplo.

![](../images/pre-built-recipes/ppp_bigpicture.png)

El siguiente documento responderá preguntas como las siguientes:
* ¿Para quién está diseñada esta receta?
* ¿Qué hace esta receta?

## ¿Para quién está diseñado este fórmula?

Su marca busca aumentar las ventas trimestrales de su línea de productos a través de promociones efectivas y dirigidas a sus clientes. Sin embargo, no todos los clientes son iguales y usted quiere el valor de su dinero. ¿A quién destino? ¿Cuál de sus clientes tiene más probabilidades de responder sin encontrar su promoción intrusivo? ¿Cómo personalizas tus promociones para cada cliente? ¿En qué canales debe confiar y cuándo debe enviar promociones?

## ¿Qué hace esta receta?

La fórmula de predicción de compra de productos utiliza el aprendizaje automático para predecir el comportamiento de compra de los clientes. Para ello, aplica un clasificador de bosque aleatorio personalizado y un modelo de datos de experiencia (XDM) de dos niveles para predecir la probabilidad de un evento de compra. El modelo utiliza datos de entrada que incorporan información de perfil del cliente e historial de compras anterior y toma por defecto parámetros de configuración predeterminados determinados por nuestros científicos de datos para mejorar la precisión predictiva.

## Esquema de datos

Esta fórmula usa [esquemas XDM](../../xdm/home.md) para modelar los datos. El esquema utilizado para esta fórmula se muestra a continuación:

| Nombre del campo | Tipo |
| --- | --- |
| Id de usuario | Cadena |
| Proporción de género | Número |
| ageY | Número |
| ageM | Número |
| optinEmail | Booleano |
| optinMobile | Booleano |
| optinAddress | Booleano |
| created | Entero |
| totalOrders | Número |
| totalItems | Número |
| orderDate1 | Número |
| Fecha de envío1 | Número |
| totalPrice1 | Número |
| impuesto1 | Número |
| orderDate2 | Número |
| Fecha de envío2 | Número |
| totalPrice2 | Número |


## Algoritmo

Primero, se carga el conjunto de datos de aprendizaje en el esquema *ProductPrediction*. Desde aquí, el modelo se entrena con un [clasificador de bosque aleatorio](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). El clasificador de bosque aleatorio es un tipo de algoritmo ensamblado que hace referencia a un algoritmo que combina varios algoritmos para obtener un rendimiento predictivo mejorado. La idea detrás del algoritmo es que el clasificador de bosque aleatorio construye múltiples árboles de decisión y los combina para crear una predicción más precisa y estable.

Este proceso comienza con la creación de un conjunto de árboles de decisión que selecciona aleatoriamente subconjuntos de datos de capacitación. Después, se promedian los resultados de cada árbol de decisión.
