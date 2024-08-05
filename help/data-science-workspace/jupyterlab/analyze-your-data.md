---
keywords: Experience Platform; JupyterLab; Cuadernos; Data Science Espacio de trabajo; temas populares; Análisis de blocs de notas de datos
solution: Experience Platform
title: Analizar los datos con blocs de notas
type: Tutorial
description: Este tutorial se centra en cómo usar Jupyter Notebooks, integrados dentro de Data Science Espacio de trabajo, para acceder, explorar y visualizar sus datos.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1729'
ht-degree: 0%

---

# Analice sus datos con blocs de notas

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Este tutorial se centra en cómo utilizar Jupyter Notebooks, creados dentro de Data Science Workspace, para acceder, explorar y visualizar sus datos. Al final de este tutorial, debería tener una comprensión de algunas de las funciones que Jupyter Notebooks ofrece para comprender mejor sus datos.

Se introducen los siguientes conceptos:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) es la interfaz basada en web de próxima generación para Project Jupyter, y está estrechamente integrada en [!DNL Adobe Experience Platform].
- **Lotes:** Los conjuntos de datos están formados por lotes. Un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. Los lotes nuevos se crean cuando se agregan datos a un conjunto de datos.
- **SDK de acceso a datos (obsoleto):** El SDK de acceso a datos está en desuso. Utilice el [[!DNL Platform SDK]](../authoring/platform-sdk.md) guía.

## Explore los blocs de notas en Data Science Espacio de trabajo

En esta sección, se exploran datos que anteriormente se ingirieron en el esquema de ventas minoristas.

Data Science Workspace permite a los usuarios crear [!DNL Jupyter Notebooks] a través de la plataforma [!DNL JupyterLab], donde pueden crear y editar flujos de trabajo de aprendizaje automático. [!DNL JupyterLab] es una herramienta de colaboración cliente-servidor que permite a los usuarios editar documentos de bloc de notas a través de un explorador web. Estos blocs de notas pueden contener tanto elementos de código ejecutable como de texto enriquecido. Para nuestros fines, utilizaremos Markdown para la descripción del análisis y el código ejecutable [!DNL Python] para la exploración y el análisis de datos.

### Elija su espacio de trabajo

Al iniciar [!DNL JupyterLab], se nos presenta una interfaz basada en web para Jupyter Notebooks. Dependiendo del tipo de cuaderno que escojamos, se iniciará un núcleo correspondiente.

Al comparar qué entorno utilizar, debemos tener en cuenta las limitaciones de cada servicio. Por ejemplo, si utilizamos la biblioteca [pandas](https://pandas.pydata.org/) con [!DNL Python], como usuario normal el límite de RAM es de 2 GB. Incluso como usuario avanzado, estaríamos limitados a 20 GB de RAM. Si se trata de cálculos más grandes, tendría sentido utilizar [!DNL Spark], que ofrece 1,5 TB compartidos con todas las instancias de bloc de notas.

De forma predeterminada, la fórmula Tensorflow funciona en un clúster de GPU y Python se ejecuta dentro de un clúster de CPU.

### Crear nuevo bloc de notas

En la interfaz de usuario [!DNL Adobe Experience Platform], seleccione [!UICONTROL Ciencia de datos] en el menú superior para llevarlo al Workspace de ciencia de datos. Desde esta página, seleccione [!DNL JupyterLab] para abrir el lanzador [!DNL JupyterLab]. Debería ver un Página similar a este.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

En nuestro tutorial, usaremos [!DNL Python] 3 en Jupyter Notebook para mostrar cómo acceder y explorar los datos. En la página del lanzador, hay blocs de notas de ejemplo proporcionados. Se utilizará la fórmula de ventas minoristas de [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

La fórmula de ventas minoristas es un ejemplo independiente que utiliza el mismo conjunto de datos de ventas minoristas para mostrar cómo se pueden explorar y visualizar los datos en Jupyter Notebook. Además, el portátil profundiza en la formación y la verificación. Encontrará más información sobre este bloc de notas específico en este [tutorial](../walkthrough.md).

### Acceso a datos

>[!NOTE]
>
>`data_access_sdk_python` está obsoleto y ya no se recomienda. Consulte el tutorial [convertir el SDK de acceso a datos al SDK de plataforma](../authoring/platform-sdk.md) para convertir su código. Los mismos pasos que se describen a continuación siguen siendo aplicables a este tutorial.

Se pasará de acceder a los datos internamente desde [!DNL Adobe Experience Platform] y a los datos externamente. Utilizaremos la biblioteca `data_access_sdk_python` para acceder a datos internos como conjuntos de datos y esquemas XDM. Para datos externos, usaremos la biblioteca [!DNL Python] de pandas.

#### Datos externos

Con el bloc de notas Ventas minoristas abierto, busque el encabezado &quot;Cargar datos&quot;. El siguiente código de [!DNL Python] utiliza la estructura de datos `DataFrame` de pandas y la función [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para leer el CSV alojado en [!DNL Github] en el DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

La estructura de datos DataFrame de Pandas es una estructura de datos etiquetada bidimensional. Para ver rápidamente las dimensiones de nuestros datos, podemos usar `df.shape`. Devuelve una tupla que representa la dimensionalidad del DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Por último, podemos echar un vistazo a la apariencia de nuestros datos. Podemos usar `df.head(n)` para ver las primeras `n` filas del DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] datos

Ahora, repasaremos el acceso a [!DNL Experience Platform] los datos.

##### Por ID de conjunto de datos

Para esta sección, utilizamos el conjunto de datos de ventas minoristas, que es el mismo conjunto de datos utilizado en el bloc de notas de muestra de ventas minoristas.

En Jupyter Notebook, puede acceder a sus datos desde la ficha **Datos** ![pestaña de datos](../images/jupyterlab/analyze-data/dataset-tab.png) a la izquierda. Al seleccionar la pestaña, se proporcionan dos carpetas. Seleccione la carpeta **[!UICONTROL Datasets]**.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Ahora, en el directorio Conjuntos de datos, puede ver todos los conjuntos de datos ingeridos. Tenga en cuenta que puede tardar un minuto en cargar todas las entradas si el directorio está muy lleno de conjuntos de datos.

Dado que el conjunto de datos es el mismo, queremos reemplazar los datos de carga de la sección anterior, que utiliza datos externos. Seleccione el bloque de código en **Cargar datos** y presione la tecla **&#39;d&#39;** del teclado dos veces. Asegúrese de que el enfoque esté en el bloque y no en el texto. Puede presionar **&#39;esc&#39;** para omitir el enfoque del texto antes de presionar **&#39;d&#39;** dos veces.

Ahora, podemos hacer clic con el botón derecho en el conjunto de datos `Retail-Training-<your-alias>` y seleccionar la opción &quot;Explorar datos en Notebook&quot; en el menú desplegable. Aparecerá una entrada de código ejecutable en el bloc de notas.

>[!TIP]
>
>Consulte la guía [[!DNL Platform SDK]](../authoring/platform-sdk.md) para convertir su código.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Si está trabajando en otros núcleos que no sean [!DNL Python], consulte [esta página](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) para acceder a los datos de [!DNL Adobe Experience Platform].

Si selecciona la celda ejecutable y pulsa el botón de reproducción en la barra de herramientas, se ejecutará el código ejecutable. El resultado de `head()` será una tabla con las claves del conjunto de datos como columnas y las primeras n filas del conjunto de datos. `head()` acepta un argumento entero para especificar cuántas líneas se van a generar. El valor predeterminado es 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Si reinicia el núcleo y vuelve a ejecutar todas las celdas, debería obtener las mismas salidas que antes.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Explorar datos

Ahora que podemos acceder a sus datos, enfocar en los datos mediante el uso de estadísticas y visualización. El conjunto de datos que estamos utilizando es un conjunto de datos minorista que brinda información diversa sobre 45 tiendas diferentes en un día determinado. Algunas características para un evento determinado `date` e `store` incluyen las siguientes:
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

Podemos impulsar [!DNL Python's] pandas biblioteca para obtener el tipo de datos de cada atributo. La salida de la siguiente llamada nos dará información sobre el número de entradas y el tipo de datos para cada una de las columnas:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Esta información es útil, ya que conocer el tipo de datos de cada columna nos permitirá saber cómo tratar los datos.

Ahora veamos el resumen estadístico. Solo se mostrarán los tipos de datos numéricos, por lo que `date`, `storeType` y `isHoliday` no se mostrarán:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Con esto, podemos ver que hay 6435 instancias para cada característica. Además, se proporciona información estadística como la media, la desviación estándar (std), el mínimo, el máximo y los intercuartiles. Esto nos proporciona información sobre la desviación de los datos. En la siguiente sección, repasaremos la visualización que funciona junto con esta información para darnos una buena comprensión de nuestros datos.

Si observamos los valores mínimos y máximos de `store`, podemos ver que hay 45 almacenes únicos que representan los datos. También existen `storeTypes` que diferencian lo que es una tienda. Podemos ver la distribución de `storeTypes` haciendo lo siguiente:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Esto significa que 22 tiendas son de `storeType` `A`, 17 son `B``storeType` y 6 son `storeType` `C`.

#### Visualización de datos

Ahora que conocemos nuestros valores de marco de datos, queremos complementar esto con visualizaciones para hacer las cosas más claras y fáciles de identificar patrones. Los gráficos también son útiles cuando se transmiten resultados a un audiencia. Algunas [!DNL Python] bibliotecas que son útiles para la visualización incluyen:
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [embarcar](https://seaborn.pydata.org/)
- [grafico](https://ggplot2.tidyverse.org/)

En esta sección, analizaremos rápidamente algunas ventajas de utilizar cada biblioteca.

[Matplotlib](https://matplotlib.org/) es el paquete de visualización [!DNL Python] más antiguo. Su objetivo es hacer &quot;las cosas fáciles y las cosas difíciles posibles&quot;. Esto suele ser cierto, ya que el paquete es extremadamente potente, pero también viene con complejidad. No siempre es fácil obtener un gráfico de aspecto razonable sin tomar una cantidad considerable de tiempo y esfuerzo.

[Pandas](https://pandas.pydata.org/) se usa principalmente por su objeto DataFrame, que permite manipular los datos mediante la indexación integrada. Sin embargo, pandas también incluye una funcionalidad de trazado integrada que se basa en matplotlib.

[seaborn](https://seaborn.pydata.org/) es un paquete compilado sobre matplotlib. Su objetivo principal es hacer que los gráficos predeterminados sean más atractivos visualmente y simplificar la creación de gráficos complicados.

[gglot](https://ggplot2.tidyverse.org/) es un paquete que también se creó sobre matplotlib. Sin embargo, la principal diferencia es que el herramienta es un puerto de ggplot2 para R. Similar a Seaborn, el objetivo es mejorar matplotlib. Los usuarios que estén familiarizados con ggplot2 para R deberían considerar este biblioteca.


##### Gráficos univariados

Los grafos univariados son diagramas de un variable individual. Un gráfico univariado común que se utiliza para visualizar sus datos es el diagrama de caja y bigotes.

Utilizando nuestros conjunto de datos minoristas de antes, podemos generar el diagrama de caja y bigotes para cada una de las 45 tiendas y sus ventas semanales. La gráfica se genera mediante la `seaborn.boxplot` función.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Se utiliza un diagrama de caja y bigotes para mostrar la distribución de los datos. Las líneas exteriores del gráfico muestran los cuartiles superior e inferior, mientras que el cuadro abarca el intervalo intercuartil. La línea de la caja marca la mediana. Los puntos de datos que superen 1,5 veces el cuartil superior o inferior se marcan como un círculo. Estos puntos se consideran periféricos.

##### Gráficos multivariable

Se utilizan gráficos multivariados para ver la interacción entre variables. Con la visualización, los científicos de datos pueden ver si hay correlaciones o patrones entre las variables. Un gráfico multivariado común es una matriz de correlación. Con una matriz de correlación, las dependencias entre múltiples variables se cuantifican con el coeficiente de correlación.

Utilizando el mismo conjunto de datos de venta minorista, podemos generar la matriz de correlación.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Observe la diagonal de 1 en el centro. Esto muestra que, al comparar una variable consigo misma, tiene una correlación positiva completa. La correlación positiva fuerte tendrá una magnitud más cercana a 1 mientras que las correlaciones débiles estarán más cerca de 0. La correlación negativa se muestra con un coeficiente negativo que muestra una tendencia inversa.


## Pasos siguientes

Este tutorial repasó cómo crear un nuevo Jupyter Notebook en el Espacio de trabajo de Ciencia de Datos y cómo acceder a los datos tanto externamente como desde [!DNL Adobe Experience Platform]. Específicamente, repasamos los siguientes pasos:
- Crear un nuevo Jupyter Notebook
- Acceso a conjuntos de datos y esquemas
- Explorar conjuntos de datos

Ahora está listo para pasar a la [siguiente sección](../models-recipes/package-source-files-recipe.md) para empaquetar una fórmula y para importarla a Data Science Workspace.
