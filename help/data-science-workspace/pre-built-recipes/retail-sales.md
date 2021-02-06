---
keywords: Experience Platform;fórmula de ventas minoristas;Área de trabajo de ciencia de datos;temas populares;fórmulas;fórmula de precompilación
solution: Experience Platform
title: Fórmula de ventas minoristas
topic: overview
description: La fórmula Ventas al por menor le permite predecir la previsión de ventas de todas las tiendas que se hayan iniciado durante un período de tiempo determinado. Con un modelo de predicción preciso, el minorista podría encontrar la relación entre la demanda y las políticas de precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Fórmula de ventas minoristas

La fórmula Ventas al por menor le permite predecir la previsión de ventas de todas las tiendas que se hayan iniciado durante un período de tiempo determinado. Con un modelo de predicción preciso, el minorista podría encontrar la relación entre la demanda y las políticas de precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.

El siguiente documento responderá preguntas como:
* ¿Para quién se construye esta receta?
* ¿Qué hace esta fórmula?
* ¿Cómo empiezo?

## ¿Para quién se construye esta receta?

Un minorista enfrenta muchos desafíos para seguir siendo competitivo en el mercado actual. Su marca busca aumentar las ventas anuales de su marca minorista, pero hay muchas decisiones que tomar para minimizar sus costos operativos. Demasiada oferta aumenta los costos de inventario, mientras que la escasez de oferta aumenta el riesgo de perder clientes a otras marcas. ¿Necesita pedir más suministros para los próximos meses? ¿Cómo decide el precio óptimo de sus productos para mantener los objetivos de ventas semanales?

## ¿Qué hace esta fórmula?

La fórmula de previsión de ventas minoristas utiliza el aprendizaje automático para predecir las tendencias de venta. La fórmula hace esto aprovechando la abundancia de datos históricos de venta al por menor y el algoritmo de aprendizaje automático o de regresión de aumento de degradado personalizado para predecir las ventas con una semana de anticipación. El modelo utiliza el historial de compras pasado y establece de forma predeterminada parámetros de configuración predeterminados determinados por nuestros Data Scientists para mejorar la precisión predictiva.

## ¿Cómo empiezo?

Puede comenzar siguiendo este [tutorial](../jupyterlab/create-a-recipe.md).

En este tutorial se analizará la creación de la fórmula de ventas minoristas en un bloc de notas de Jupyter y el uso del bloc de notas para crear el flujo de trabajo de fórmulas para crear la fórmula en Adobe Experience Platform.

## Esquema de datos

Esta fórmula utiliza [esquemas XDM](../../xdm/schema/field-dictionary.md) para modelar los datos. El esquema utilizado para esta fórmula se muestra a continuación:

| Nombre del campo | Tipo |
--- | ---
| date | Cadena |
| store | Número entero |
| storeType | Cadena |
| weekSales | Número |
| storeSize | Número entero |
| temperatura | Número |
| regionalFuelPrice | Número |
| markdown | Número |
| cpi | Número |
| desempleo | Número |
| isHoliday | Booleano |


## Algoritmo

En primer lugar, se carga el conjunto de datos de capacitación en el esquema *DSWRetailSales*. A partir de aquí, el modelo se entrena usando un [algoritmo de regresión de aumento de degradado](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). La mejora de degradado utiliza la idea de que los alumnos débiles (uno que sea al menos ligeramente mejor que una oportunidad aleatoria) pueden formar una sucesión de alumnos centrados en mejorar las debilidades del alumno anterior. Juntos, pueden utilizarse para crear un poderoso modelo predictivo.

El proceso incluye tres elementos: una función de pérdida, un alumno débil y un modelo aditivo.

La función de pérdida se refiere a una medida de lo bien que hace un modelo de predicción en términos de poder predecir el resultado esperado: en esta fórmula se utiliza la regresión de menos cuadrados.

En el aumento de degradado, se utiliza un árbol de decisiones como alumno débil. Normalmente, los árboles con un número limitado de capas, nodos y divisiones se utilizan para garantizar que el alumno siga siendo débil.

Por último, se utiliza un modelo de aditivo. Después de calcular la pérdida con la función de pérdida, se elige y se pondera el árbol que reduce la pérdida para mejorar la modelización de las observaciones más difíciles. La producción del árbol ponderado se añade a la secuencia existente de árboles para mejorar la producción final del modelo: cantidad de ventas futuras.