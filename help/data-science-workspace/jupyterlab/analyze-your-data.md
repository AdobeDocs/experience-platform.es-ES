---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;analizar blocs de notas de datos
solution: Experience Platform
title: Analizar los datos con Notebooks
type: Tutorial
description: Este tutorial se centra en cómo utilizar Jupyter Notebooks, creados dentro del espacio de trabajo de ciencia de datos, para acceder, explorar y visualizar sus datos.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---

# Analizar los datos con blocs de notas

Este tutorial se centra en cómo utilizar Jupyter Notebooks, creados dentro del espacio de trabajo de ciencia de datos, para acceder, explorar y visualizar sus datos. Al final de este tutorial, debería tener una comprensión de algunas de las funciones que Jupyter Notebooks ofrece para comprender mejor sus datos.

Se introducen los siguientes conceptos:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) es la interfaz basada en web de próxima generación para Project Jupyter y está totalmente integrada en [!DNL Adobe Experience Platform].
- **Lotes:** Los conjuntos de datos están formados por lotes. Un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. Los lotes nuevos se crean cuando se agregan datos a un conjunto de datos.
- **SDK de acceso a datos (obsoleto):** El SDK de acceso a datos ya no se utiliza. Utilice el [[!DNL Platform SDK]](../authoring/platform-sdk.md) guía.

## Explorar blocs de notas en Data Science Workspace

En esta sección, se exploran los datos que se han introducido anteriormente en el esquema de ventas minoristas.

Data Science Workspace permite a los usuarios crear [!DNL Jupyter Notebooks] a través de [!DNL JupyterLab] plataforma donde pueden crear y editar flujos de trabajo de aprendizaje automático. [!DNL JupyterLab] es una herramienta de colaboración servidor-cliente que permite a los usuarios editar documentos del bloc de notas a través de un explorador web. Estos blocs de notas pueden contener tanto elementos de código ejecutable como de texto enriquecido. Para nuestros fines, utilizaremos Markdown para la descripción del análisis y el ejecutable [!DNL Python] código para realizar análisis y exploración de datos.

### Elija su espacio de trabajo

Al iniciar [!DNL JupyterLab], se nos presenta una interfaz basada en web para Jupyter Notebooks. Dependiendo del tipo de cuaderno que escojamos, se iniciará un núcleo correspondiente.

Al comparar qué entorno utilizar, debemos tener en cuenta las limitaciones de cada servicio. Por ejemplo, si utilizamos la variable [pandas](https://pandas.pydata.org/) biblioteca con [!DNL Python], como usuario normal, el límite de RAM es de 2 GB. Incluso como usuario avanzado, estaríamos limitados a 20 GB de RAM. Si se trata de cálculos más grandes, tendría sentido utilizar [!DNL Spark] que ofrece 1,5 TB que se comparten con todas las instancias de portátiles.

De forma predeterminada, la fórmula Tensorflow funciona en un clúster de GPU y Python se ejecuta dentro de un clúster de CPU.

### Crear nuevo bloc de notas

En el [!DNL Adobe Experience Platform] IU, seleccione [!UICONTROL Ciencia de datos] en el menú superior para llevarle al espacio de trabajo de ciencia de datos. En esta página, seleccione [!DNL JupyterLab] para abrir [!DNL JupyterLab] lanzador. Debería ver una página similar a esta.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

En nuestro tutorial, utilizaremos [!DNL Python] 3 en Jupyter Notebook para mostrar cómo acceder y explorar los datos. En la página del lanzador, hay blocs de notas de ejemplo proporcionados. Se utilizará la fórmula de ventas minoristas para [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

La fórmula de ventas minoristas es un ejemplo independiente que utiliza el mismo conjunto de datos de ventas minoristas para mostrar cómo se pueden explorar y visualizar los datos en Jupyter Notebook. Además, el portátil profundiza en la formación y la verificación. Encontrará más información sobre este bloc de notas específico en este [introducción](../walkthrough.md).

### Acceso a datos

>[!NOTE]
>
>El `data_access_sdk_python` está obsoleto y ya no se recomienda. Consulte la [convertir el SDK de acceso a datos a Platform SDK](../authoring/platform-sdk.md) tutorial para convertir el código. Los mismos pasos que se describen a continuación siguen siendo aplicables a este tutorial.

Pasaremos a acceder a los datos internamente desde [!DNL Adobe Experience Platform] y los datos de forma externa. Se va a utilizar el `data_access_sdk_python` para acceder a datos internos, como conjuntos de datos y esquemas XDM. Para datos externos, usaremos los pandas [!DNL Python] biblioteca.

#### Datos externos

Con el bloc de notas Ventas minoristas abierto, busque el encabezado &quot;Cargar datos&quot;. Lo siguiente [!DNL Python] el código usa &quot;pandas&quot; `DataFrame` la estructura de datos y el [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para leer el CSV alojado en [!DNL Github] en el DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

La estructura de datos DataFrame de Pandas es una estructura de datos etiquetada bidimensional. Para ver rápidamente las dimensiones de nuestros datos, podemos usar la variable `df.shape`. Devuelve una tupla que representa la dimensionalidad del DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Por último, podemos echar un vistazo a la apariencia de nuestros datos. Podemos usar `df.head(n)` para ver la primera `n` filas del DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] data

Ahora, pasaremos a acceder a [!DNL Experience Platform] datos.

##### Por ID de conjunto de datos

Para esta sección, utilizamos el conjunto de datos de ventas minoristas, que es el mismo conjunto de datos utilizado en el bloc de notas de muestra de ventas minoristas.

En Jupyter Notebook, puede acceder a sus datos desde el **Datos** pestaña ![pestaña de datos](../images/jupyterlab/analyze-data/dataset-tab.png) a la izquierda. Al seleccionar la pestaña, se proporcionan dos carpetas. Seleccione el **[!UICONTROL Conjuntos de datos]** carpeta.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Ahora, en el directorio Conjuntos de datos, puede ver todos los conjuntos de datos ingeridos. Tenga en cuenta que puede tardar un minuto en cargar todas las entradas si el directorio está muy lleno de conjuntos de datos.

Dado que el conjunto de datos es el mismo, queremos reemplazar los datos de carga de la sección anterior, que utiliza datos externos. Seleccione el bloque de código en **Cargar datos** y pulse el botón **&#39;d&#39;** en el teclado dos veces. Asegúrese de que el enfoque esté en el bloque y no en el texto. Puede pulsar **&#39;esc&#39;** para escapar del enfoque del texto antes de pulsar **&#39;d&#39;** dos veces.

Ahora, podemos hacer clic derecho en el `Retail-Training-<your-alias>` y seleccione la opción &quot;Explorar datos en Notebook&quot; en el menú desplegable. Aparecerá una entrada de código ejecutable en el bloc de notas.

>[!TIP]
>
>Consulte la [[!DNL Platform SDK]](../authoring/platform-sdk.md) para convertir el código.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Si está trabajando en otros núcleos distintos de [!DNL Python], consulte [esta página](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) para acceder a los datos de [!DNL Adobe Experience Platform].

Si selecciona la celda ejecutable y pulsa el botón de reproducción en la barra de herramientas, se ejecutará el código ejecutable. La salida de `head()` será una tabla con las claves del conjunto de datos como columnas y las primeras n filas del conjunto de datos. `head()` acepta un argumento entero para especificar cuántas líneas se van a generar. El valor predeterminado es 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Si reinicia el núcleo y vuelve a ejecutar todas las celdas, debería obtener las mismas salidas que antes.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Exploración de los datos

Ahora que podemos acceder a sus datos, vamos a centrarnos en los datos en sí mediante el uso de estadísticas y visualización. El conjunto de datos que estamos utilizando es un conjunto de datos de minoristas que proporciona información variada sobre 45 tiendas diferentes en un día determinado. Algunas características de un determinado `date` y `store` incluir lo siguiente:
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

Podemos aprovechar [!DNL Python's] biblioteca pandas para obtener el tipo de datos de cada atributo. El resultado de la siguiente llamada nos dará información sobre el número de entradas y el tipo de datos para cada una de las columnas:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Esta información es útil, ya que conocer el tipo de datos de cada columna nos permitirá saber cómo tratar los datos.

Ahora veamos el resumen estadístico. Solo se muestran los tipos de datos numéricos, por lo que `date`, `storeType`, y `isHoliday` no se colocará:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Con esto, podemos ver que hay 6435 instancias para cada característica. Además, se proporciona información estadística como la media, la desviación estándar (std), el mínimo, el máximo y los intercuartiles. Esto nos proporciona información sobre la desviación de los datos. En la siguiente sección, analizaremos la visualización que funciona junto con esta información para darnos una buena comprensión de nuestros datos.

Consulta de los valores mínimo y máximo de `store`, podemos ver que hay 45 almacenes únicos que representan los datos. También hay `storeTypes` que diferencian lo que es una tienda. Podemos ver la distribución de `storeTypes` haciendo lo siguiente:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Esto significa que 22 tiendas son de `storeType` `A`, 17 son `storeType` `B`, y 6 son `storeType` `C`.

#### Visualización de datos

Ahora que conocemos los valores de nuestros marcos de datos, queremos complementarlos con visualizaciones para que las cosas sean más claras y fáciles de identificar. Los gráficos también son útiles para transmitir los resultados a una audiencia. Algunos [!DNL Python] las bibliotecas que son útiles para la visualización incluyen:
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [embarcado](https://seaborn.pydata.org/)
- [diagrama de gg](https://ggplot2.tidyverse.org/)

En esta sección, analizaremos rápidamente algunas ventajas de utilizar cada biblioteca.

[Matplotlib](https://matplotlib.org/) es el más antiguo [!DNL Python] paquete de visualización. Su objetivo es hacer &quot;las cosas fáciles y las cosas difíciles posibles&quot;. Esto suele ser cierto, ya que el paquete es extremadamente potente, pero también viene con complejidad. No siempre es fácil obtener un gráfico de aspecto razonable sin tomar una cantidad considerable de tiempo y esfuerzo.

[Pandas](https://pandas.pydata.org/) se utiliza principalmente para su objeto DataFrame, que permite la manipulación de datos con indexación integrada. Sin embargo, pandas también incluye una funcionalidad de trazado integrada que se basa en matplotlib.

[embarcado](https://seaborn.pydata.org/) es un paquete creado sobre matplotlib. Su objetivo principal es hacer que los gráficos predeterminados sean más atractivos visualmente y simplificar la creación de gráficos complicados.

[diagrama de gg](https://ggplot2.tidyverse.org/) es un paquete también creado sobre matplotlib. Sin embargo, la principal diferencia es que la herramienta es un puerto de gglot2 para R. Similar a seaborn, el objetivo es mejorar sobre matplotlib. Los usuarios que estén familiarizados con gplot2 para R deben considerar esta biblioteca.


##### Gráficos univariables

Los gráficos univariables son gráficos de una variable individual. Un gráfico univariado común se utiliza para visualizar sus datos es el gráfico de cajas y bigotes.

Utilizando nuestro conjunto de datos de comercio minorista de antes, podemos generar la trama de cajas y bigotes para cada una de las 45 tiendas y sus ventas semanales. El gráfico se genera mediante la variable `seaborn.boxplot` función.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Se utiliza un gráfico de cajas y bigotes para mostrar la distribución de los datos. Las líneas exteriores del gráfico muestran los cuartiles superior e inferior, mientras que el cuadro abarca el intervalo intercuartil. La línea de la caja marca la mediana. Los puntos de datos que superen 1,5 veces el cuartil superior o inferior se marcan como un círculo. Estos puntos se consideran periféricos.

##### Gráficos multivariable

Se utilizan gráficos multivariados para ver la interacción entre variables. Con la visualización, los científicos de datos pueden ver si hay correlaciones o patrones entre las variables. Un gráfico multivariado común es una matriz de correlación. Con una matriz de correlación, las dependencias entre múltiples variables se cuantifican con el coeficiente de correlación.

Utilizando el mismo conjunto de datos de venta minorista, podemos generar la matriz de correlación.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Observe la diagonal de 1 en el centro. Esto muestra que, al comparar una variable consigo misma, tiene una correlación positiva completa. La correlación positiva fuerte tendrá una magnitud más cercana a 1 mientras que las correlaciones débiles estarán más cerca de 0. La correlación negativa se muestra con un coeficiente negativo que muestra una tendencia inversa.


## Pasos siguientes

Este tutorial explica cómo crear un nuevo Jupyter Notebook en el espacio de trabajo de ciencia de datos y cómo acceder a los datos de forma externa y desde [!DNL Adobe Experience Platform]. Específicamente, hemos seguido los siguientes pasos:
- Crear nuevo Jupyter Notebook
- Acceso a conjuntos de datos y esquemas
- Explorar conjuntos de datos

Ahora está listo para continuar con la [sección siguiente](../models-recipes/package-source-files-recipe.md) para empaquetar una fórmula y para importarla en Data Science Workspace.
