---
keywords: Experience Platform;JupyterLab;blocs de notas;Área de trabajo de ciencia de datos;temas populares;analizar blocs de notas de datos
solution: Experience Platform
title: Analizar los datos con portátiles
topic: tutorial
type: Tutorial
description: Este tutorial se centra en cómo utilizar los equipos portátiles Jupyter, creados en el espacio de trabajo de ciencias de datos, para acceder, explorar y visualizar sus datos.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---


# Analizar los datos con portátiles

Este tutorial se centra en cómo utilizar los equipos portátiles Jupyter, creados en el espacio de trabajo de ciencias de datos, para acceder, explorar y visualizar sus datos. Al final de este tutorial, debe conocer algunas de las funciones de la oferta de los equipos portátiles Jupyter para comprender mejor sus datos.

Se introducen los siguientes conceptos:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) es la interfaz basada en web de próxima generación para Project Jupyter, y está estrechamente integrada en  [!DNL Adobe Experience Platform].
- **Lotes:** Los conjuntos de datos se componen de lotes. Un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. Se crean nuevos lotes cuando se agregan datos a un conjunto de datos.
- **SDK de acceso a datos (obsoleto):** El SDK de acceso a datos ya no se utiliza. Utilice la guía [[!DNL Platform SDK]](../authoring/platform-sdk.md).

## Explorar blocs de notas en el área de trabajo de ciencias de datos

En esta sección, se exploran los datos que anteriormente se ingirieron en el esquema de ventas minoristas.

Data Science Workspace permite a los usuarios crear [!DNL Jupyter Notebooks] mediante la plataforma [!DNL JupyterLab], donde pueden crear y editar flujos de trabajo de aprendizaje automático. [!DNL JupyterLab] es una herramienta de colaboración servidor-cliente que permite a los usuarios editar documentos de portátiles a través de un navegador web. Estos blocs de notas pueden contener tanto código ejecutable como elementos de texto enriquecido. Para nuestros propósitos, usaremos Markdown para la descripción de análisis y el código ejecutable [!DNL Python] para realizar la exploración y análisis de datos.

### Elija el espacio de trabajo

Al lanzar [!DNL JupyterLab], se nos presenta una interfaz basada en Web para equipos portátiles Jupyter. Dependiendo del tipo de portátil que seleccionemos, se iniciará un núcleo correspondiente.

Al comparar qué entorno utilizar debemos tener en cuenta las limitaciones de cada servicio. Por ejemplo, si utilizamos la biblioteca [pandas](https://pandas.pydata.org/) con [!DNL Python] como usuario normal, el límite de RAM es de 2 GB. Incluso como usuario de energía, estaríamos limitados a 20 GB de RAM. Si se trata de cálculos más grandes, tendría sentido utilizar [!DNL Spark], que oferta 1,5 TB que se comparte con todas las instancias de portátiles.

De forma predeterminada, la fórmula Tensorflow funciona en un clúster de GPU y Python se ejecuta en un clúster de CPU.

### Crear un bloc de notas nuevo

En la interfaz de usuario [!DNL Adobe Experience Platform], haga clic en la ficha Ciencias de datos del menú superior para ir al Área de trabajo de ciencias de datos. Desde esta página, haga clic en la ficha [!DNL JupyterLab] que abrirá el iniciador [!DNL JupyterLab]. Debería ver una página similar a esta.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher.png)

En nuestro tutorial, utilizaremos [!DNL Python] 3 en el bloc de notas de Jupyter para mostrar cómo acceder y explorar los datos. En la página del iniciador, se proporcionan blocs de notas de ejemplo. Utilizaremos la fórmula Ventas al detalle para [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

La fórmula de ventas minoristas es un ejemplo independiente que utiliza el mismo conjunto de datos de ventas minoristas para mostrar cómo se pueden explorar y visualizar los datos en Jupyter Notebook. Además, el cuaderno de notas es más profundo en cuanto a capacitación y verificación. Encontrará más información sobre este bloc de notas específico en este [tutorial](../walkthrough.md).

### Acceso a los datos

>[!NOTE]
>
>El `data_access_sdk_python` está obsoleto y ya no se recomienda. Consulte el tutorial [conversión del SDK de acceso a datos al SDK de plataforma](../authoring/platform-sdk.md) para convertir el código. Los mismos pasos a continuación se aplican para este tutorial.

Pasaremos a acceder a los datos internamente desde [!DNL Adobe Experience Platform] y a los datos externamente. Utilizaremos la biblioteca `data_access_sdk_python` para acceder a datos internos como datasets y esquemas XDM. Para datos externos, usaremos la biblioteca pandas [!DNL Python].

#### Datos externos

Con el bloc de notas Ventas minoristas abierto, busque el encabezado &quot;Cargar datos&quot;. El siguiente código [!DNL Python] utiliza la estructura de datos `DataFrame` de pandas y la función [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para leer el CSV alojado en [!DNL Github] en el marco de datos:

![](../images/jupyterlab/analyze-data/read_csv.png)

La estructura de datos DataFrame de Pandas es una estructura de datos etiquetada de dos dimensiones. Para ver rápidamente las dimensiones de nuestros datos, podemos utilizar el `df.shape`. Esto devuelve un tupla que representa la dimensionalidad del marco de datos:

![](../images/jupyterlab/analyze-data/df_shape.png)

Finalmente, podemos echar un vistazo a cómo se ven nuestros datos. Podemos utilizar `df.head(n)` para la vista de las primeras `n` filas del marco de datos:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] datos

Ahora, pasaremos a acceder a [!DNL Experience Platform] datos.

##### Por ID de conjunto de datos

Para esta sección, utilizamos el conjunto de datos de ventas minoristas, que es el mismo conjunto de datos utilizado en el bloc de notas de muestra de ventas minoristas.

En nuestro bloc de notas Jupyter, podemos acceder a nuestros datos desde la ficha **Data** de la izquierda. Al hacer clic en la ficha, podrá ver una lista de conjuntos de datos.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Ahora, en el directorio Datasets, podremos ver todos los datasets ingestados. Tenga en cuenta que puede tomar un minuto cargar todas las entradas si el directorio está muy lleno con conjuntos de datos.

Dado que el conjunto de datos es el mismo, queremos reemplazar los datos de carga de la sección anterior que utiliza datos externos. Seleccione el bloque de código en **Cargar datos** y presione dos veces la tecla **&#39;d&#39;** del teclado. Asegúrese de que el enfoque está en el bloque y no en el texto. Puede pulsar **&#39;esc&#39;** para evitar el enfoque del texto antes de pulsar **&#39;d&#39;** dos veces.

Ahora, podemos hacer clic con el botón derecho en el conjunto de datos `Retail-Training-<your-alias>` y seleccionar la opción &quot;Explorar datos en el bloc de notas&quot; en la lista desplegable. Aparecerá una entrada de código ejecutable en el bloc de notas.

>[!TIP]
>
>Consulte la guía [[!DNL Platform SDK]](../authoring/platform-sdk.md) para convertir el código.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Si está trabajando en otros núcleos que no sean [!DNL Python], consulte [esta página](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) para obtener acceso a los datos de [!DNL Adobe Experience Platform].

Si selecciona la celda ejecutable y pulsa el botón de reproducción en la barra de herramientas, se ejecutará el código ejecutable. El resultado para `head()` será una tabla con las claves del conjunto de datos como columnas y las primeras n filas del conjunto de datos. `head()` acepta un argumento integer para especificar cuántas líneas desea generar. De forma predeterminada, es 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Si reinicia el núcleo y vuelve a ejecutar todas las celdas, debería obtener los mismos resultados que antes.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Explore sus datos

Ahora que podemos acceder a sus datos, centrémonos en los mismos datos mediante estadísticas y visualización. El conjunto de datos que estamos utilizando es un conjunto de datos minorista que proporciona información diversa sobre 45 almacenes diferentes en un día determinado. Algunas características para un `date` y `store` dado incluyen lo siguiente:
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### Resumen estadístico

Podemos aprovechar la biblioteca de [!DNL Python's] paneles para obtener el tipo de datos de cada atributo. El resultado de la siguiente llamada nos proporcionará información sobre el número de entradas y el tipo de datos de cada una de las columnas:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Esta información es útil, ya que conocer el tipo de datos de cada columna nos permitirá saber cómo tratar los datos.

Ahora veamos el resumen estadístico. Sólo se mostrarán los tipos de datos numéricos, por lo que no se obtendrán `date`, `storeType` y `isHoliday`:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Con esto podemos ver que hay 6435 instancias para cada característica. Además, se proporciona información estadística como media, desviación estándar (std), min, max e intercuartil. Esto nos proporciona información sobre la desviación de los datos. En la siguiente sección, analizaremos la visualización que trabaja junto con esta información para darnos una buena comprensión de nuestros datos.

Si miramos los valores mínimo y máximo de `store`, podemos ver que hay 45 almacenes únicos que los datos representan. También hay `storeTypes` que diferencian lo que es una tienda. Podemos ver la distribución de `storeTypes` haciendo lo siguiente:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Esto significa que 22 almacenes tienen `storeType` `A`, 17 son `storeType` `B` y 6 son `storeType` `C`.

#### Visualización de datos

Ahora que conocemos los valores de los marcos de datos, queremos complementar esto con visualizaciones para que las cosas sean más claras y fáciles de identificar patrones. Los gráficos también son útiles para transmitir resultados a una audiencia. Algunas bibliotecas [!DNL Python] que son útiles para la visualización incluyen:
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [gráfico](https://ggplot2.tidyverse.org/)

En esta sección, veremos rápidamente algunas ventajas de usar cada biblioteca.

[](https://matplotlib.org/) Matplotlibis es el paquete de  [!DNL Python] visualización más antiguo. Su objetivo es hacer que &quot;las cosas fáciles sean fáciles y difíciles posibles&quot;. Esto tiende a ser cierto, ya que el paquete es extremadamente poderoso pero también viene con complejidad. No siempre es fácil obtener un gráfico de aspecto razonable sin tomar una considerable cantidad de tiempo y esfuerzo.

[](https://pandas.pydata.org/) Pandasis se utiliza principalmente para su objeto DataFrame, que permite la manipulación de datos con indexación integrada. Sin embargo, pandas también incluye una funcionalidad de trazado integrada basada en matplotlib.

[](https://seaborn.pydata.org/) seabornis un paquete construido sobre matplotlib. Su objetivo principal es hacer que los gráficos predeterminados sean más atractivos visualmente y simplificar la creación de gráficos complicados.

[](https://ggplot2.tidyverse.org/) ggplotis un paquete también construido sobre matplotlib. Sin embargo, la diferencia principal es que la herramienta es un puerto de ggplot2 para R. De manera similar al mar, el objetivo es mejorar la matplotlib. Los usuarios que estén familiarizados con ggchart2 para R deben tener en cuenta esta biblioteca.


##### Gráficos uniformes

Los gráficos uniformes son gráficos de una variable individual. Para visualizar los datos se utiliza un gráfico univariado común: el cuadro y el diagrama de whisky.

Usando nuestro conjunto de datos de antes, podemos generar la tabla y el diagrama de whisky para cada una de las 45 tiendas y sus ventas semanales. El trazado se genera mediante la función `seaborn.boxplot`.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Para mostrar la distribución de datos se utiliza una casilla y un diagrama de whisky. Las líneas exteriores del trazado muestran los cuartiles superior e inferior, mientras que el cuadro abarca el rango intercuartil. La línea del cuadro marca la mediana. Los puntos de datos que superen 1,5 veces el cuartil superior o inferior se marcarán como un círculo. Estos puntos se consideran periféricos.

##### Gráficos multivariados

Los gráficos multivariados se utilizan para ver la interacción entre variables. Con la visualización, los científicos de datos pueden ver si hay correlaciones o patrones entre las variables. Un gráfico multivariado común es una matriz de correlación. Con una matriz de correlación, las dependencias entre varias variables se cuantifican con el coeficiente de correlación.

Con el mismo conjunto de datos minorista, podemos generar la matriz de correlación.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Observe la diagonal de 1&#39;s hacia abajo en el centro. Esto muestra que cuando se compara una variable con sí misma, tiene una correlación positiva completa. Una correlación positiva fuerte tendrá una magnitud más cercana a 1, mientras que las correlaciones débiles estarán más cerca de 0. La correlación negativa se muestra con un coeficiente negativo que muestra una tendencia inversa.


## Pasos siguientes

En este tutorial se explica cómo crear un nuevo bloc de notas Jupyter en el área de trabajo de ciencias de datos y cómo acceder a los datos de forma externa, así como desde [!DNL Adobe Experience Platform]. Concretamente, dimos los siguientes pasos:
- Crear un nuevo bloc de notas Jupyter
- Obtener acceso a conjuntos de datos y esquemas
- Explorar conjuntos de datos

Ahora está listo para pasar a la [siguiente sección](../models-recipes/package-source-files-recipe.md) para empaquetar una fórmula e importarla a Área de trabajo de ciencias de datos.