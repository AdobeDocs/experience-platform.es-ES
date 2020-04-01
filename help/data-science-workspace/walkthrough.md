---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Recorrido de Área de trabajo de ciencias de datos
topic: Walkthrough
translation-type: tm+mt
source-git-commit: 1f756e7bc71c9ff227757aee64af29e0772c24af

---


# Recorrido de Área de trabajo de ciencias de datos

Este documento proporciona un tutorial para Adobe Experience Platform Data Science Workspace. Específicamente, analizaremos el flujo de trabajo general que un científico de datos podría llevar a cabo para resolver un problema usando el aprendizaje automático.

## Requisitos previos

- Una cuenta de Adobe ID registrada
   - La cuenta de Adobe ID debe haberse agregado a una organización con acceso a Adobe Experience Platform y a Data Science Workspace

## Motivación del científico de datos

Un minorista enfrenta muchos desafíos para seguir siendo competitivo en el mercado actual. Una de las principales preocupaciones del minorista es decidir la fijación de precios óptimos de sus productos y predecir las tendencias de venta. Con un modelo de predicción preciso, el minorista podría encontrar la relación entre la demanda y las políticas de precios y tomar decisiones de precios optimizadas para maximizar las ventas y los ingresos.

## La solución del científico de datos

La solución de un científico de datos es aprovechar la riqueza de datos históricos a los que tiene acceso un minorista, predecir tendencias futuras y optimizar las decisiones de precios. Usaremos datos de ventas anteriores para entrenar nuestro modelo de aprendizaje automático y usaremos el modelo para predecir las tendencias futuras de venta. Con esto, el minorista podrá tener perspectivas que le ayudarán a realizar cambios en los precios.

En este resumen, vamos a seguir los pasos que un científico de datos podría seguir para realizar un conjunto de datos y crear un modelo para predecir las ventas semanales. Iremos a las siguientes secciones en el bloc de notas de ventas minoristas de muestra en el espacio de trabajo de ciencia de datos de la plataforma Adobe Experience:

- [Configuración](#setup)
- [Exploración de datos](#exploring-data)
- [Ingeniería de funciones](#feature-engineering)
- [Formación y verificación](#training-and-verification)

### Equipos portátiles en el área de trabajo de ciencias de la información

En primer lugar, queremos crear un bloc de notas JupyterLab para abrir el bloc de notas de muestra &quot;Ventas al por menor&quot;. El seguimiento de los pasos que realiza el científico de datos en el bloc de notas nos permitirá comprender un flujo de trabajo típico.

En la interfaz de usuario de Adobe Experience Platform, haga clic en la ficha Ciencias de datos del menú superior para ir al área de trabajo de ciencias de datos. Desde esta página, haga clic en la ficha JupyterLab que abrirá el iniciador de JupyterLab. Debería ver una página similar a esta.

![](./images/walkthrough/jupyterlab_launcher.png)

En nuestro tutorial, utilizaremos Python 3 en el bloc de notas Jupyter para mostrar cómo acceder y explorar los datos. En la página del iniciador se proporcionan blocs de notas de ejemplo. Utilizaremos la muestra &quot;Ventas al detalle&quot; para Python 3.

![](./images/walkthrough/retail_sales.png)

### Configuración

Con el bloc de notas Retail Sales abierto, lo primero que hacemos es cargar las bibliotecas necesarias para nuestro flujo de trabajo. En la siguiente lista se ofrece una breve descripción de para qué se utiliza cada uno de ellos:
- **numpy** : biblioteca de computación científica que agrega compatibilidad con matrices y matrices multidimensionales y grandes
- **pandas** : biblioteca que oferta estructuras de datos y operaciones utilizadas para la manipulación y análisis de datos
- **matplotlib.pyplot** : biblioteca de trazado que proporciona una experiencia similar a MATLAB al trazar
- **mar** : biblioteca de visualización de datos de interfaz de alto nivel basada en la biblioteca de metadatos
- **sklearn** : biblioteca de aprendizaje automático que incluye algoritmos de clasificación, regresión, vector de compatibilidad y clúster
- **advertencias** : biblioteca que controla los mensajes de advertencia

### Explorar datos

#### Cargar datos

Una vez cargadas las bibliotecas, podemos ver en inicio los datos. El siguiente código Python utiliza la estructura de datos de pandas y la función `DataFrame` read_csv() [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para leer el CSV alojado en Github en el DataFrame de pandas:

![](./images/walkthrough/read_csv.png)

La estructura de datos DataFrame de Pandas es una estructura de datos bidimensional etiquetada. Para ver rápidamente las dimensiones de nuestros datos, podemos usar `df.shape`. Esto devuelve un tupla que representa la dimensionalidad del marco de datos:

![](./images/walkthrough/df_shape.png)

Finalmente, podemos echar un vistazo a cómo se ven nuestros datos. Podemos utilizar `df.head(n)` para vista de las primeras `n` filas de DataFrame:

![](./images/walkthrough/df_head.png)

#### Resumen estadístico

Podemos aprovechar la biblioteca pandas de Python para obtener el tipo de datos de cada atributo. El resultado de la siguiente llamada nos proporcionará información sobre el número de entradas y el tipo de datos de cada una de las columnas:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Esta información es útil, ya que conocer el tipo de datos de cada columna nos permitirá saber cómo tratar los datos.

Ahora veamos el resumen estadístico. Solo se mostrarán los tipos de datos numéricos `date`, `storeType`y no se `isHoliday` generarán:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Con esto podemos ver que hay 6435 instancias para cada característica. Además, se proporciona información estadística como media, desviación estándar (std), min, max e intercuartil. Esto nos proporciona información sobre la desviación de los datos. En la siguiente sección, analizaremos la visualización que trabaja junto con esta información para darnos una completa comprensión de nuestros datos.

Si miramos los valores mínimo y máximo de `store`, podemos ver que hay 45 almacenes únicos que los datos representan. También hay `storeTypes` que diferencian lo que es una tienda. Podemos ver la distribución de `storeTypes` haciendo lo siguiente:

![](./images/walkthrough/df_groupby.png)

Esto significa que 22 tiendas son de `storeType A` , 17 lo son `storeType B`, y 6 lo son `storeType C`.

#### Visualizar datos

Ahora que conocemos los valores de los marcos de datos, queremos complementar esto con visualizaciones para que las cosas sean más claras y fáciles de identificar patrones. Estos gráficos también son útiles para transmitir resultados a una audiencia.

#### Gráficos uniformes

Los gráficos uniformes son gráficos de una variable individual. Un gráfico univariado común que se utiliza para visualizar los datos son los gráficos de cajas y de murmullos.

Usando nuestro conjunto de datos de antes, podemos generar la tabla y el diagrama de whisky para cada una de las 45 tiendas y sus ventas semanales. El trazado se genera con la `seaborn.boxplot` función .

![](./images/walkthrough/box_whisker.png)

Para mostrar la distribución de datos se utiliza una casilla y un diagrama de whisky. Las líneas exteriores del trazado muestran los cuartiles superior e inferior, mientras que el cuadro abarca el rango intercuartil. La línea del cuadro marca la mediana. Cualquier punto de datos que supere 1,5 veces el cuartil superior o inferior se marcará como un círculo. Estos puntos se consideran periféricos.

Luego, podemos trazar las ventas semanales con el tiempo. Solamente mostraremos la salida de la primera tienda. El código del cuaderno genera 6 parcelas correspondientes a 6 de las 45 tiendas de nuestro conjunto de datos.

![](./images/walkthrough/weekly_sales.png)

Con este diagrama podemos comparar las ventas semanales durante un período de 2 años. Es fácil ver los picos de venta y los patrones a través del tiempo.

#### Gráficos multivariados

Los gráficos multivariados se utilizan para ver la interacción entre variables. Con la visualización, los científicos de datos pueden ver si hay correlaciones o patrones entre las variables. Un gráfico multivariado común es una matriz de correlación. Con una matriz de correlación, las dependencias entre varias variables se cuantifican con el coeficiente de correlación.

Con el mismo conjunto de datos minorista, podemos generar la matriz de correlación.

![](./images/walkthrough/correlation_1.png)

Fíjese en la diagonal de los que están en el centro. Esto muestra que cuando se compara una variable con sí misma, tiene una correlación positiva completa. Una correlación positiva fuerte tendrá una magnitud más cercana a 1, mientras que las correlaciones débiles estarán más cerca de 0. La correlación negativa se muestra con un coeficiente negativo que muestra una tendencia inversa.

### Ingeniería de funciones

En esta sección, realizaremos modificaciones en nuestro conjunto de datos comercial. Realizaremos las siguientes operaciones:

- agregar columnas de semana y año
- convertir storeType en una variable de indicador
- convertir isHoliday en una variable numérica
- predecir ventas semanalesVentas de la semana siguiente

#### Añadir columnas de semana y año

El formato actual para la fecha (`2010-02-05`) es difícil de diferenciar entre los datos de cada semana. Debido a esto, convertiremos la fecha a la semana y al año.

![](./images/walkthrough/date_to_week_year.png)

Ahora la semana y la fecha son las siguientes:

![](./images/walkthrough/date_week_year.png)

#### Convertir storeType en variable de indicador

A continuación, queremos convertir la columna storeType en columnas que representen a cada `storeType`. Hay 3 tipos de tiendas (`A`, `B`, `C`), de las cuales estamos creando 3 nuevas columnas. El valor establecido en cada una será un valor booleano donde se establecerá &#39;1&#39; en función de lo que `storeType` fue y `0` para las otras dos columnas.

![](./images/walkthrough/storeType.png)

Se eliminará la `storeType` columna actual.

#### Convertir isHoliday en tipo numérico

La siguiente modificación es cambiar el `isHoliday` booleano a una representación numérica.

![](./images/walkthrough/isHoliday.png)


#### Predecir ventas semanalesVentas de la semana siguiente

Ahora queremos agregar ventas semanales anteriores y futuras a cada uno de nuestros conjuntos de datos. Estamos haciendo esto compensando nuestra `weeklySales`. Además, calculamos la `weeklySales` diferencia. Esto se hace restando `weeklySales` a la semana anterior `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

Dado que estamos desactivando los `weeklySales` datos 45 conjuntos de datos hacia adelante y 45 conjuntos de datos hacia atrás para crear nuevas columnas, los primeros y últimos 45 puntos de datos tendrán valores NaN. Podemos eliminar estos puntos de nuestro conjunto de datos usando la `df.dropna()` función que elimina todas las filas que tienen valores NaN.

![](./images/walkthrough/dropna.png)

A continuación se muestra un resumen del conjunto de datos después de nuestras modificaciones:

![](./images/walkthrough/df_info_new.png)

### Capacitación y verificación

Ahora es el momento de crear algunos modelos de los datos y seleccionar qué modelo es el mejor para predecir las ventas futuras. Evaluaremos los 5 algoritmos siguientes:

- Regresión lineal
- Árbol de decisiones
- Bosque aleatorio
- Aumento de degradado
- K Vecinos

#### Dividir conjuntos de datos en subconjuntos de prueba y capacitación

Necesitamos una manera de saber cuán preciso será nuestro modelo para poder predecir valores. Esta evaluación se puede realizar asignando parte del conjunto de datos para utilizarlo como validación y el resto como datos de capacitación. Dado que `weeklySalesAhead` son los valores futuros reales de `weeklySales`, podemos utilizarlos para evaluar cuán preciso es el modelo para predecir el valor. La división se realiza a continuación:

![](./images/walkthrough/split_data.png)

Ahora tenemos `X_train` y `y_train` para preparar los modelos y `X_test` y `y_test` para su evaluación más adelante.

#### Algoritmos de comprobación de puntos

En esta sección, declararemos todos los algoritmos en una matriz llamada `model`. A continuación, iteramos a través de esta matriz y para cada algoritmo, ingresamos nuestros datos de capacitación con los `model.fit()` que se crea un modelo `mdl`. Usando este modelo, prediremos `weeklySalesAhead` con nuestros `X_test` datos.

![](./images/walkthrough/training_scoring.png)

Para la puntuación, estamos tomando la diferencia porcentual media entre los valores predichos `weeklySalesAhead` con los valores reales en los `y_test` datos. Ya que queremos minimizar la diferencia entre nuestra predicción y la realidad, el Regresor de aumento de degradado es el modelo de mejor rendimiento.

#### Visualizar predicciones

Finalmente, visualizaremos nuestro modelo de predicción con los valores reales de ventas semanales. La línea azul representa los números reales, mientras que el verde representa nuestra predicción usando la Ampliación de degradado. El siguiente código genera 6 gráficos que representan 6 de los 45 almacenes en nuestro conjunto de datos. Aquí solo `Store 1` se muestra:

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## Conclusión. 

Con esta visión general, analizamos el flujo de trabajo que un científico de datos podría llevar a cabo para resolver un problema de ventas minoristas. Específicamente, dimos los siguientes pasos para llegar a una solución que prediga futuras ventas semanales.

- [Configuración](#setup)
- [Exploración de datos](#exploring-data)
- [Ingeniería de funciones](#feature-engineering)
- [Formación y verificación](#training-and-verification)