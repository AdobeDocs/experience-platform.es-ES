---
keywords: Experience Platform;fórmula de ventas minoristas;Data Science Workspace;temas populares;fórmulas;fórmula de generación previa
solution: Experience Platform
title: Fórmula de ventas minoristas
description: La fórmula Venta minorista permite predecir la previsión de ventas de todas las tiendas creadas durante un período determinado. Con un modelo de predicción preciso, el minorista podría encontrar la relación entre la demanda y las políticas de precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---

# Receta de ventas minoristas

La fórmula Venta minorista permite predecir la previsión de ventas de todas las tiendas creadas durante un período determinado. Con un modelo de predicción preciso, el minorista podría encontrar la relación entre la demanda y las políticas de precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.

El siguiente documento responderá preguntas como:
* ¿Para quién se ha creado esta receta?
* ¿Qué hace esta receta?
* ¿Cómo empiezo?

## ¿Para quién se ha creado esta receta?

Un minorista enfrenta muchos desafíos para seguir siendo competitivo en el mercado actual. Su marca busca aumentar las ventas anuales de su marca minorista, pero hay muchas decisiones que tomar para minimizar sus costos operativos. Demasiada oferta aumenta los costos de inventario, mientras que la oferta insuficiente aumenta el riesgo de perder clientes a otras marcas. ¿Necesita pedir más suministro para los próximos meses? ¿Cómo puede decidir cuál es el precio óptimo de sus productos para mantener los objetivos de ventas semanales?

## ¿Qué hace esta receta?

La fórmula de previsión de ventas minoristas utiliza el aprendizaje automático para predecir las tendencias de venta. Para ello, la fórmula aprovecha la riqueza de datos comerciales históricos y el algoritmo de aprendizaje automático o retroceso que aumenta el degradado personalizado para predecir las ventas con una semana de antelación. El modelo utiliza el historial de compras anterior y establece de forma predeterminada parámetros de configuración predeterminados determinados por nuestros científicos de datos para mejorar la precisión predictiva.

## ¿Cómo empiezo?

Para empezar, siga esta [tutorial](../jupyterlab/create-a-model.md).

Este tutorial explicará la creación de la fórmula de ventas minoristas en un bloc de notas de Jupyter y el uso del bloc de notas en el flujo de trabajo de fórmula para crear la fórmula en Adobe Experience Platform.

## Esquema de datos

Esta fórmula utiliza [Esquemas XDM](../../xdm/schema/field-dictionary.md) para modelar los datos. El esquema utilizado para esta fórmula se muestra a continuación:

| Nombre del campo | Tipo |
| --- | --- |
| date | Cadena |
| almacenar | Número entero |
| storeType | Cadena |
| weeklySales | Número |
| storeSize | Número entero |
| temperatura | Número |
| regionalFuelPrice | Número |
| markdown | Número |
| cpi | Número |
| desempleo | Número |
| isHoliday | Booleano |


## Algoritmo

En primer lugar, el conjunto de datos de formación en la variable *DSWRetailSales* se ha cargado el esquema. Desde aquí, el modelo se entrena usando un [algoritmo de regresión de aumento de degradado](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). La mejora de degradado utiliza la idea de que los estudiantes débiles (uno que sea al menos ligeramente mejor que una oportunidad aleatoria) pueden formar una sucesión de estudiantes centrados en mejorar las debilidades del alumno anterior. Juntos, se pueden usar para crear un poderoso modelo predictivo.

El proceso consta de tres elementos: una función de pérdida, un aprendiz débil y un modelo aditivo.

La función de pérdida se refiere a una medida de lo bien que hace un modelo de predicción en términos de poder predecir el resultado esperado: en esta receta se utiliza la regresión con menos cuadrados.

En la mejora de degradado, se utiliza un árbol de decisiones como el alumno débil. Normalmente, los árboles con un número limitado de capas, nodos y divisiones se utilizan para garantizar que el alumno siga siendo débil.

Por último, se utiliza un modelo aditivo. Después de calcular la pérdida con la función de pérdida, se elige y se pondera el árbol que reduce la pérdida para mejorar la modelización de las observaciones más difíciles. A continuación, la salida del árbol ponderado se agrega a la secuencia existente de árboles para mejorar la producción final del modelo - cantidad de ventas futuras .
