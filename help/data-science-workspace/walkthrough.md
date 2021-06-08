---
keywords: Experience Platform;tutorial;Data Science Workspace;temas populares
solution: Experience Platform
title: Tutorial de Data Science Workspace
topic-legacy: Walkthrough
description: Este documento proporciona un tutorial para Adobe Experience Platform Data Science Workspace. Específicamente, el flujo de trabajo general que un científico de datos debe llevar a cabo para resolver un problema usando el aprendizaje automático.
exl-id: d814846e-52a9-46c6-831a-3399241959f2
source-git-commit: 7d98340e7949aadc744513415c4fc7469efd2403
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---

# [!DNL Data Science Workspace] tutorial

Este documento proporciona un tutorial para Adobe Experience Platform [!DNL Data Science Workspace]. Este tutorial describe un flujo de trabajo general de Data Science y cómo pueden abordar y resolver un problema mediante el aprendizaje automático.

## Requisitos previos

- Una cuenta de Adobe ID registrada
   - La cuenta de Adobe ID debe haberse agregado a una organización con acceso a Adobe Experience Platform y [!DNL Data Science Workspace].

## Caso de uso comercial

Un minorista enfrenta muchos desafíos para seguir siendo competitivo en el mercado actual. Una de las principales preocupaciones del minorista es decidir cuál es el precio óptimo de un producto y predecir las tendencias de venta. Con un modelo de predicción preciso, un minorista podría encontrar la relación entre la demanda y las políticas de precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.

## La solución del científico de datos

La solución de un científico de datos es aprovechar la gran cantidad de información histórica que proporciona un minorista, predecir tendencias futuras y optimizar las decisiones de precios. Este tutorial utiliza datos de ventas anteriores para entrenar un modelo de aprendizaje automático y utiliza el modelo para predecir tendencias de ventas futuras. Con esto, puede generar perspectivas para ayudar a realizar cambios óptimos en los precios.

Esta descripción general refleja los pasos que un científico de datos debe seguir para realizar un conjunto de datos y crear un modelo para predecir ventas semanales. Este tutorial cubre las siguientes secciones en el bloc de notas de ventas minoristas de muestra de Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configuración](#setup)
- [Exploración de datos](#exploring-data)
- [Ingeniería de funciones](#feature-engineering)
- [Capacitación y verificación](#training-and-verification)

### Portátiles en [!DNL Data Science Workspace]

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Notebooks]** desde la pestaña **[!UICONTROL Data Science]** para que se muestre en la página de información general [!UICONTROL Notebooks]. En esta página, seleccione la pestaña [!DNL JupyterLab] para iniciar el entorno [!DNL JupyterLab]. La página de aterrizaje predeterminada para [!DNL JupyterLab] es **[!UICONTROL Launcher]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Este tutorial utiliza [!DNL Python] 3 en [!DNL JupyterLab Notebooks] para mostrar cómo acceder a los datos y explorarlos. En la página Lanzador se proporcionan muestras de blocs de notas. El bloc de notas de muestra **[!UICONTROL Retail Sales]** se utiliza en los ejemplos que se proporcionan a continuación.

### Configuración {#setup}

Con el bloc de notas Ventas minoristas abierto, lo primero que debe hacer es cargar las bibliotecas necesarias para el flujo de trabajo. La siguiente lista ofrece una breve descripción de cada una de las bibliotecas utilizadas en los ejemplos en pasos posteriores.

- **numpy**: Biblioteca informática científica que añade compatibilidad con matrices y matrices multidimensionales y grandes
- **pandas**: Biblioteca que ofrece estructuras de datos y operaciones utilizadas para la manipulación y el análisis de datos
- **matplotlib.pyplot**: Biblioteca de gráficos que proporciona una experiencia similar a MATLAB al trazar
- **mar** : Biblioteca de visualización de datos de interfaz de alto nivel basada en matplotlib
- **sklearn**: Biblioteca de aprendizaje automático que incluye algoritmos de clasificación, regresión, vector de compatibilidad y clúster
- **advertencias**: Biblioteca que controla los mensajes de advertencia

### Explorar datos {#exploring-data}

#### Carga de datos

Una vez cargadas las bibliotecas, puede empezar a consultar los datos. El siguiente código [!DNL Python] utiliza la estructura de datos `DataFrame` de pandas y la función [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para leer el CSV alojado en [!DNL Github] en el DataFrame de pandas:

![](./images/walkthrough/read_csv.png)

La estructura de datos DataFrame de Pandas es una estructura de datos etiquetada bidimensional. Para ver rápidamente las dimensiones de los datos, puede utilizar `df.shape`. Esto devuelve un tuple que representa la dimensión del DataFrame:

![](./images/walkthrough/df_shape.png)

Por último, puede obtener una vista previa del aspecto que tendrán los datos. Puede utilizar `df.head(n)` para ver las primeras `n` filas del DataFrame:

![](./images/walkthrough/df_head.png)

#### Resumen estadístico

Podemos aprovechar la biblioteca de paneles [!DNL Python's] para obtener el tipo de datos de cada atributo. El resultado de la siguiente llamada nos proporcionará información sobre el número de entradas y el tipo de datos de cada una de las columnas:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Esta información es útil, ya que conocer el tipo de datos de cada columna nos permitirá saber cómo tratar los datos.

Ahora veamos el resumen estadístico. Solo se mostrarán los tipos de datos numéricos, por lo que no se producirán `date`, `storeType` y `isHoliday`:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Con esto, puede ver que hay 6435 instancias para cada característica. Además, se proporciona información estadística como media, desviación estándar (std), min, max e intercuarartiles. Esto nos proporciona información sobre la desviación de los datos. En la siguiente sección, pasará a la visualización que funciona junto con esta información para darnos una comprensión completa de sus datos.

Si observa los valores mínimo y máximo de `store`, puede ver que hay 45 almacenes únicos que representan los datos. También hay `storeTypes` que diferencian lo que es una tienda. puede ver la distribución de `storeTypes` haciendo lo siguiente:

![](./images/walkthrough/df_groupby.png)

Esto significa que 22 tiendas son de `storeType A` , 17 son `storeType B` y 6 son `storeType C`.

#### Visualizar datos

Ahora que conoce los valores de los marcos de datos, desea complementar esto con visualizaciones para que las cosas sean más claras y fáciles de identificar patrones. Estos gráficos también son útiles para transmitir resultados a una audiencia.

#### Univar gráficos

Los gráficos uniformes son gráficos de una variable individual. Un gráfico univariado común que se utiliza para visualizar los datos son gráficos de cajas y whiskies.

Utilizando su conjunto de datos minoristas de antes, puede generar el diagrama de cajas y whiskys para cada una de las 45 tiendas y sus ventas semanales. El diagrama se genera mediante la función `seaborn.boxplot`.

![](./images/walkthrough/box_whisker.png)

Para mostrar la distribución de datos se utiliza un diagrama de cajas y de whiskies. Las líneas exteriores de la trama muestran los cuartiles superior e inferior, mientras que la casilla abarca el intervalo intercuartil. La línea del cuadro marca la mediana. Cualquier punto de datos que supere 1,5 veces el cuartil superior o inferior se marcará como un círculo. Estos puntos se consideran periféricos.

A continuación, puede trazar las ventas semanales con el tiempo. Solo se mostrará el resultado del primer almacén. El código del bloc de notas genera 6 gráficos correspondientes a 6 de las 45 tiendas de nuestro conjunto de datos.

![](./images/walkthrough/weekly_sales.png)

Con este diagrama, puede comparar las ventas semanales durante un periodo de 2 años. Es fácil ver los picos de venta y los patrones a través del tiempo.

#### Gráficos multivariados

Los gráficos multivariados se utilizan para ver la interacción entre variables. Con la visualización, los científicos de datos pueden ver si hay correlaciones o patrones entre las variables. Un gráfico multivariable común es una matriz de correlación. Con una matriz de correlación, las dependencias entre varias variables se cuantifican con el coeficiente de correlación.

Con el mismo conjunto de datos comercial, puede generar la matriz de correlación.

![](./images/walkthrough/correlation_1.png)

Fíjese en la diagonal de las que están en el centro. Esto muestra que cuando se compara una variable con sí misma, tiene una correlación positiva completa. Una correlación positiva fuerte tendrá una magnitud más cercana a 1, mientras que las correlaciones débiles estarán más cerca de 0. La correlación negativa se muestra con un coeficiente negativo que muestra una tendencia inversa.

### Ingeniería de características {#feature-engineering}

En esta sección, la ingeniería de características se utiliza para realizar modificaciones en el conjunto de datos comercial realizando las siguientes operaciones:

- Agregar columnas de semana y año
- Convertir storeType en una variable de indicador
- Convertir isHoliday en una variable numérica
- Predecir ventas semanales de la semana siguiente

#### Agregar columnas de semana y año

El formato actual para la fecha (`2010-02-05`) puede dificultar la diferenciación de que los datos son para cada semana. Por este motivo, debe convertir la fecha para que contenga semana y año.

![](./images/walkthrough/date_to_week_year.png)

Ahora, la semana y la fecha son las siguientes:

![](./images/walkthrough/date_week_year.png)

#### Convertir storeType en variable de indicador

A continuación, desea convertir la columna storeType en columnas que representen cada `storeType`. Existen tres tipos de almacenamiento (`A`, `B`, `C`), desde los cuales se crean 3 nuevas columnas. El valor establecido en cada es un valor booleano donde se establece un &quot;1&quot; en función de `storeType` y `0` en las otras 2 columnas.

![](./images/walkthrough/storeType.png)

La columna `storeType` actual se abandona.

#### Convertir isHoliday a tipo numérico

La siguiente modificación es cambiar el booleano `isHoliday` a una representación numérica.

![](./images/walkthrough/isHoliday.png)

#### Predecir ventas semanales de la semana siguiente

Ahora, desea agregar ventas semanales anteriores y futuras a cada uno de sus conjuntos de datos. Puede hacerlo compensando su `weeklySales`. Además, se calcula la diferencia `weeklySales`. Esto se hace restando `weeklySales` con el `weeklySales` de la semana anterior.

![](./images/walkthrough/weekly_past_future.png)

Como está compensando los `weeklySales` datos 45 conjuntos de datos hacia adelante y 45 conjuntos de datos hacia atrás para crear nuevas columnas, los 45 primeros y últimos puntos de datos tienen valores NaN. Puede eliminar estos puntos del conjunto de datos utilizando la función `df.dropna()` que elimina todas las filas que tienen valores NaN.

![](./images/walkthrough/dropna.png)

A continuación se muestra un resumen del conjunto de datos después de sus modificaciones:

![](./images/walkthrough/df_info_new.png)

### Capacitación y verificación {#training-and-verification}

Ahora, es el momento de crear algunos modelos de los datos y seleccionar qué modelo es el mejor para predecir ventas futuras. Evaluará los 5 algoritmos siguientes:

- Regresión lineal
- Árbol de decisiones
- Bosque aleatorio
- Aumento de degradado
- K Vecinos

#### Dividir conjunto de datos en subconjuntos de prueba y capacitación

Necesita una forma de saber la precisión con la que su modelo podrá predecir valores. Esta evaluación se puede realizar asignando parte del conjunto de datos para utilizarla como validación y el resto como datos de capacitación. Dado que `weeklySalesAhead` es el valor futuro real de `weeklySales`, puede utilizarlo para evaluar la precisión del modelo en la predicción del valor. La división se realiza a continuación:

![](./images/walkthrough/split_data.png)

Ahora tiene `X_train` y `y_train` para preparar los modelos y `X_test` y `y_test` para su evaluación posterior.

#### Algoritmos de comprobación al azar

En esta sección, declara todos los algoritmos en una matriz denominada `model`. A continuación, se repite a través de esta matriz y para cada algoritmo, introduzca los datos de capacitación con `model.fit()` que crea un modelo `mdl`. Con este modelo, puede predecir `weeklySalesAhead` con sus datos `X_test`.

![](./images/walkthrough/training_scoring.png)

Para la puntuación, está tomando la diferencia porcentual media entre el `weeklySalesAhead` predicho y los valores reales en los datos `y_test`. Dado que desea minimizar la diferencia entre la predicción y el resultado real, el Regresor de aumento de degradado es el modelo de mejor rendimiento.

#### Visualizar predicciones

Por último, puede visualizar el modelo de predicción con los valores de ventas semanales reales. La línea azul representa los números reales, mientras que el verde representa la predicción mediante el aumento de degradado. El siguiente código genera 6 gráficos que representan 6 de los 45 almacenes en el conjunto de datos. Aquí solo se muestra `Store 1`:

![](./images/walkthrough/visualize_prediction.png)

## Pasos siguientes

Este documento abarcaba un flujo de trabajo general de científicos de datos para resolver un problema de ventas minoristas. Para resumir:

- Cargue las bibliotecas necesarias para el flujo de trabajo.
- Una vez cargadas las bibliotecas, puede empezar a ver los datos mediante resúmenes estadísticos, visualizaciones y gráficos.
- A continuación, se usa ingeniería de características para realizar modificaciones en el conjunto de datos comercial.
- Por último, cree modelos de los datos y seleccione qué modelo es el de mejor rendimiento para predecir ventas futuras.

Una vez que esté listo, comience leyendo la [guía del usuario de JupyterLab](./jupyterlab/overview.md) para obtener una descripción general rápida de los blocs de notas en Adobe Experience Platform Data Science Workspace. Además, si le interesa conocer los modelos y las fórmulas, comience leyendo el tutorial [retail sales schema and dataset](./models-recipes/create-retails-sales-dataset.md) .
