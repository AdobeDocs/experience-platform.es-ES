---
keywords: Experience Platform;receta de ventas minoristas;Data Science Workspace;temas populares;recetas;receta previa a la compilación
solution: Experience Platform
title: Fórmula de ventas minoristas
description: La fórmula de ventas minoristas permite predecir la previsión de ventas de todas las tiendas predefinidas para un período de tiempo determinado. Con un modelo de predicción preciso, el minorista podría encontrar la relación entre las políticas de demanda y precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---

# Fórmula de ventas minoristas

La fórmula de ventas minoristas permite predecir la previsión de ventas de todas las tiendas predefinidas para un período de tiempo determinado. Con un modelo de predicción preciso, el minorista podría encontrar la relación entre las políticas de demanda y precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.

El siguiente documento responderá preguntas como las siguientes:
* ¿Para quién está diseñada esta receta?
* ¿Qué hace esta receta?
* ¿Cómo empiezo?

## ¿Para quién está diseñada esta receta?

Un minorista se enfrenta a muchos desafíos para seguir siendo competitivo en el mercado actual. Su marca busca impulsar las ventas anuales de su marca minorista, pero hay muchas decisiones que tomar para minimizar sus costes operativos. Un suministro excesivo aumenta los costes de inventario, mientras que un suministro insuficiente aumenta el riesgo de perder clientes en relación con otras marcas. ¿Necesita pedir más suministros para los próximos meses? ¿Cómo decide el precio óptimo de sus productos para mantener los objetivos de ventas semanales?

## ¿Qué hace esta receta?

La fórmula de previsión de ventas minoristas utiliza el aprendizaje automático para predecir las tendencias de venta. La fórmula lo hace aprovechando la riqueza de datos históricos de venta minorista y el gradiente personalizado que potencia el algoritmo de aprendizaje automático de regresor para predecir las ventas con una semana de antelación. El modelo utiliza el historial de compras anterior y toma por defecto parámetros de configuración predeterminados determinados por nuestros científicos de datos para mejorar la precisión predictiva.

## ¿Cómo empiezo?

Puede empezar siguiendo este procedimiento [tutorial](../jupyterlab/create-a-model.md).

Este tutorial trata sobre la creación de la fórmula de ventas minoristas en un Jupyter Notebook y el uso del bloc de notas al flujo de trabajo de fórmulas para crear la fórmula en Adobe Experience Platform.

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
| regionFuelPrice | Número |
| markdown | Número |
| ppp | Número |
| desocupación | Número |
| isHoliday | Booleano |


## Algoritmo

En primer lugar, el conjunto de datos de aprendizaje en *DSWRetailSales* se ha cargado el esquema. A partir de aquí, el modelo se entrena con una [algoritmo de regresor de aumento de degradado](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). El impulso de degradado utiliza la idea de que los alumnos débiles (que es al menos ligeramente mejor que la probabilidad aleatoria) pueden formar una sucesión de alumnos centrados en mejorar las debilidades del alumno anterior. Juntos, se pueden usar para crear un poderoso modelo predictivo.

El proceso consta de tres elementos: una función de pérdida, un alumno débil y un modelo aditivo.

La función de pérdida se refiere a una medida de lo bueno que hace un modelo de predicción en términos de poder predecir el resultado esperado: en esta fórmula se utiliza la regresión de mínimos cuadrados.

En el aumento de degradado, se utiliza un árbol de decisión como alumno débil. Normalmente, se utilizan árboles con un número limitado de capas, nodos y divisiones para garantizar que el alumno siga siendo débil.

Por último, se utiliza un modelo aditivo. Después de calcular la pérdida con la función de pérdida, se elige el árbol que reduce la pérdida y se pondera para mejorar el modelado de las observaciones más difíciles. La producción del árbol ponderado se añade a la secuencia de árboles existente para mejorar la producción final del modelo - cantidad de ventas futuras .
