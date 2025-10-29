---
keywords: Experience Platform;JupyterLab;blocs de notas;Workspace de ciencia de datos;temas populares;%dataset;modo interactivo;modo por lotes;sdk de Spark;sdk de python;acceso a datos;acceso a datos de blocs de notas
solution: Experience Platform
title: Acceso a datos en Jupyterlab Notebooks
description: Esta guía se centra en cómo utilizar Jupyter Notebooks, creados dentro de Data Science Workspace para acceder a sus datos.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '3274'
ht-degree: 3%

---

# Acceso a datos en [!DNL Jupyterlab] blocs de notas

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Cada núcleo compatible proporciona funcionalidades integradas que le permiten leer datos de Experience Platform de un conjunto de datos dentro de un bloc de notas. Actualmente, JupyterLab en Adobe Experience Platform Data Science Workspace admite portátiles para [!DNL Python], R, PySpark y Scala. Sin embargo, la compatibilidad con la paginación de datos está limitada a [!DNL Python] y a los blocs de notas R. Esta guía se centra en cómo utilizar cuadernos de JupyterLab para acceder a sus datos.

## Introducción

Antes de leer esta guía, revisa la [[!DNL JupyterLab] guía del usuario](./overview.md) para ver una introducción de alto nivel a [!DNL JupyterLab] y su función en Data Science Workspace.

## Límites de datos de portátiles {#notebook-data-limits}

>[!IMPORTANT]
>
>Para los portátiles PySpark y Scala si recibe un error con el motivo &quot;Cliente RPC remoto desasociado&quot;. Esto suele significar que el controlador o un ejecutor se está quedando sin memoria. Intente cambiar al modo [&quot;por lotes&quot;](#mode) para resolver este error.

La siguiente información define la cantidad máxima de datos que se pueden leer, qué tipo de datos se utilizaron y el periodo de tiempo estimado que tarda la lectura de los datos.

Para [!DNL Python] y R, se utilizó un servidor portátil configurado con 40 GB de RAM para los puntos de referencia. Para PySpark y Scala, se utilizó un clúster de bloques de datos configurado a 64 GB de RAM, 8 núcleos, 2 DBU con un máximo de 4 trabajadores para los puntos de referencia descritos a continuación.

Los datos del esquema ExperienceEvent utilizados variaron en tamaño a partir de mil (1K) filas que van hasta mil millones (1B) de filas. Tenga en cuenta que para las métricas PySpark y [!DNL Spark], se utilizó un intervalo de fecha de 10 días para los datos XDM.

Los datos del esquema ad hoc se preprocesaron mediante [!DNL Query Service] Crear tabla como selección (CTAS). Estos datos también variaron en tamaño a partir de mil (1K) filas que van hasta mil (1B) filas.

### Cuándo usar el modo por lotes o el modo interactivo {#mode}

Al leer conjuntos de datos con portátiles PySpark y Scala, tiene la opción de utilizar el modo interactivo o el modo por lotes para leer el conjunto de datos. La interacción se realiza para obtener resultados rápidos, mientras que el modo por lotes es para conjuntos de datos grandes.

- Para los portátiles PySpark y Scala, se debe utilizar el modo por lotes cuando se lean 5 millones de filas de datos o más. Para obtener más información sobre la eficacia de cada modo, consulta las tablas de límite de datos [PySpark](#pyspark-data-limits) o [Scala](#scala-data-limits) a continuación.

### [!DNL Python] límites de datos de bloc de notas

**Esquema XDM ExperienceEvent:** Debe poder leer un máximo de 2 millones de filas (aproximadamente 6,1 GB de datos en el disco) de datos XDM en menos de 22 minutos. Añadir filas adicionales puede provocar errores.

| Número de filas | 1K | 10K | 100K | 1 M | 2 M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Tamaño en disco (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (en segundos) | 20,3 | 86,8 | 63 | 659 | 1315 |

**esquema ad hoc:** Debe poder leer un máximo de 5 millones de filas (datos de~5,6 GB en disco) de datos que no sean XDM (ad hoc) en menos de 14 minutos. Añadir filas adicionales puede provocar errores.

| Número de filas | 1K | 10K | 100K | 1 M | 2 M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Tamaño en disco (en MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (en segundos) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### Límites de datos de portátiles R

**Esquema XDM ExperienceEvent:** Debe poder leer un máximo de 1 millón de filas de datos XDM (datos de 3 GB en disco) en menos de 13 minutos.

| Número de filas | 1K | 10K | 100K | 1 M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Tamaño en disco (MB) | 18,73 | 187,5 | 308 | 3000 |
| Núcleo R (en segundos) | 14,03 | 69,6 | 86,8 | 775 |

**esquema ad hoc:** Debería poder leer un máximo de 3 millones de filas de datos ad hoc (293 MB de datos en disco) en unos 10 minutos.

| Número de filas | 1K | 10K | 100K | 1 M | 2 M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Tamaño en disco (en MB) | 0,082 | 0,612 | 9.0 | 91 | 188 | 293 |
| R SDK (en segundos) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Límites de datos de portátiles PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**Esquema XDM ExperienceEvent:** En el modo interactivo, debería poder leer un máximo de 5 millones de filas (aproximadamente 13,42 GB de datos en el disco) de datos XDM en unos 20 minutos. El modo interactivo solo admite hasta 5 millones de filas. Si desea leer conjuntos de datos más grandes, se recomienda cambiar al modo por lotes. En el modo por lotes, debería poder leer un máximo de 500 millones de filas (aproximadamente 1,31 TB de datos en disco) de datos XDM en aproximadamente 14 horas.

| Número de filas | 1K | 10K | 100K | 1 M | 2 M | 3M | 5M | 10M | 50 M | 100 M | 500 M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamaño en disco | 2,93 MB | 4,38 MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| SDK (modo interactivo) | 33s | 32,4s | 55,1s | 253,5 s | 489,2s | 729,6s | 1206,8s | - | - | - | - |
| SDK (modo por lotes) | 815,8s | 492,8s | 379,1s | 637,4s | 624,5 s | 869,2s | 1104.1s | año 1786 | 5387,2s | 10624,6s | 50547s |

**esquema ad hoc:** En el modo interactivo, debería poder leer un máximo de 5 millones de filas (datos de~5,36 GB en disco) de datos que no sean XDM en menos de 3 minutos. En el modo por lotes debería poder leer un máximo de 1000 millones de filas (datos de ~ 1,05 TB en disco) de datos que no sean XDM en unos 18 minutos.

| Número de filas | 1K | 10K | 100K | 1 M | 2 M | 3M | 5M | 10M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Tamaño en disco | 1,12 MB | 11,24 MB | 109,48 MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Modo interactivo de SDK (en segundos) | 28,2s | 18,6s | 20,8s | 20,9s | 23,8s | 21,7s | 24,7s | - | - | - | - | - |
| Modo por lotes de SDK (en segundos) | 428,8 s | 578,8s | 641,4s | 538,5 s | 630,9s | 467,3s | 411s | 675s | 702s | 719,2s | 1022.1s | 1122,3s |

### [!DNL Spark] límites de datos de cuadernos (Scala kernel): {#scala-data-limits}

**Esquema XDM ExperienceEvent:** En el modo interactivo, debería poder leer un máximo de 5 millones de filas (aproximadamente 13,42 GB de datos en el disco) de datos XDM en unos 18 minutos. El modo interactivo solo admite hasta 5 millones de filas. Si desea leer conjuntos de datos más grandes, se recomienda cambiar al modo por lotes. En el modo por lotes, debería poder leer un máximo de 500 millones de filas (aproximadamente 1,31 TB de datos en disco) de datos XDM en aproximadamente 14 horas.

| Número de filas | 1K | 10K | 100K | 1 M | 2 M | 3M | 5M | 10M | 50 M | 100 M | 500 M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamaño en disco | 2,93 MB | 4,38 MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| Modo interactivo de SDK (en segundos) | 37,9s | 22,7s | 45,6s | 231,7s | 444,7s | 660,6s | mil cien | - | - | - | - |
| Modo por lotes de SDK (en segundos) | 374,4s | 398,5s | 527s | 487,9s | 588,9s | 829s | 939,1s | 1441s | 5473,2s | 10118,8 | 49207,6 |

**esquema ad hoc:** En el modo interactivo, debería poder leer un máximo de 5 millones de filas (datos de~5,36 GB en disco) de datos que no sean XDM en menos de 3 minutos. En el modo por lotes debería poder leer un máximo de 1000 millones de filas (datos de ~ 1,05 TB en disco) de datos que no sean XDM en unos 16 minutos.

| Número de filas | 1K | 10K | 100K | 1 M | 2 M | 3M | 5M | 10M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Tamaño en disco | 1,12 MB | 11,24 MB | 109,48 MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Modo interactivo de SDK (en segundos) | 35,7s | 31s | 19,5s | 25,3s | 23s | 33,2s | 25,5 s | - | - | - | - | - |
| Modo por lotes de SDK (en segundos) | 448,8s | 459,7s | 519s | 475,8s | 599,9s | 347,6s | 407,8s | 397s | 518,8s | 487,9s | 760,2s | 975,4s |

## Notebooks de Python {#python-notebook}

[!DNL Python] blocs de notas le permiten paginar datos al acceder a conjuntos de datos. A continuación se muestra un código de muestra para leer datos con y sin paginación. Para obtener más información sobre los blocs de notas de Python de inicio disponibles, visite la sección [[!DNL JupyterLab] Launcher](./overview.md#launcher) en la guía del usuario de JupyterLab.

La siguiente documentación de Python describe los siguientes conceptos:

- [Leer de un conjunto de datos](#python-read-dataset)
- [Escribir en un conjunto de datos](#write-python)
- [Datos de consulta](#query-data-python)
- [Filtrado de datos de ExperienceEvent](#python-filter)

### Lectura de un conjunto de datos en Python {#python-read-dataset}

**Sin paginación:**

Al ejecutar el siguiente código, se leerá todo el conjunto de datos. Si la ejecución se realiza correctamente, los datos se guardarán como un marco de datos Pandas al que hace referencia la variable `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Con paginación:**

Al ejecutar el siguiente código se leerán los datos del conjunto de datos especificado. La paginación se logra limitando y desplazando los datos a través de las funciones `limit()` y `offset()` respectivamente. La limitación de datos hace referencia al número máximo de puntos de datos que se van a leer, mientras que la compensación hace referencia al número de puntos de datos que se van a omitir antes de leer los datos. Si la operación de lectura se ejecuta correctamente, los datos se guardarán como un marco de datos Pandas al que hace referencia la variable `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Escribir en un conjunto de datos en Python {#write-python}

Para escribir en un conjunto de datos de su bloc de notas de JupyterLab, seleccione la pestaña Icono de datos (resaltada a continuación) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL Schemas]**. Seleccione **[!UICONTROL Datasets]**, haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Write Data in Notebook]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.

![](../images/jupyterlab/data-access/write-dataset.png)

- Use **[!UICONTROL Write Data in Notebook]** para generar una celda de escritura con el conjunto de datos seleccionado.
- Use **[!UICONTROL Explore Data in Notebook]** para generar una celda de lectura con el conjunto de datos seleccionado.
- Use **[!UICONTROL Query Data in Notebook]** para generar una celda de consulta básica con el conjunto de datos seleccionado.

También puede copiar y pegar la siguiente celda de código. Reemplazar `{DATASET_ID}` y `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Consultar datos usando [!DNL Query Service] en [!DNL Python] {#query-data-python}

[!DNL JupyterLab] en [!DNL Experience Platform] le permite usar SQL en un bloc de notas de [!DNL Python] para tener acceso a los datos a través de [Adobe Experience Platform Query Service](https://www.adobe.com/go/query-service-home-en). El acceso a los datos a través de [!DNL Query Service] puede ser útil para tratar conjuntos de datos grandes debido a sus tiempos de ejecución superiores. Tenga en cuenta que la consulta de datos mediante [!DNL Query Service] tiene un límite de tiempo de procesamiento de diez minutos.

Antes de usar [!DNL Query Service] en [!DNL JupyterLab], asegúrese de que tiene una comprensión de la [[!DNL Query Service] sintaxis SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

La consulta de datos mediante [!DNL Query Service] requiere que proporcione el nombre del conjunto de datos de destino. Puede generar las celdas de código necesarias buscando el conjunto de datos deseado mediante **[!UICONTROL Data explorer]**. Haga clic con el botón derecho en la lista de conjuntos de datos y haga clic en **[!UICONTROL Query Data in Notebook]** para generar dos celdas de código en su bloc de notas. Estas dos celdas se describen con más detalle a continuación.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Para usar [!DNL Query Service] en [!DNL JupyterLab], primero debe crear una conexión entre el bloc de notas de [!DNL Python] que trabaja y [!DNL Query Service]. Esto se puede lograr ejecutando la primera celda generada.

```python
qs_connect()
```

En la segunda celda generada, la primera línea debe definirse antes que la consulta SQL. De manera predeterminada, la celda generada define una variable opcional (`df0`) que guarda los resultados de la consulta como un marco de datos Pandas. <br>El argumento `-c QS_CONNECTION` es obligatorio y le indica al núcleo que ejecute la consulta SQL en [!DNL Query Service]. Consulte el [apéndice](#optional-sql-flags-for-query-service) para obtener una lista de argumentos adicionales.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Se puede hacer referencia directamente a las variables de Python en una consulta SQL mediante sintaxis con formato de cadena y ajustando las variables entre paréntesis angulares (`{}`), como se muestra en el ejemplo siguiente:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrar datos de [!DNL ExperienceEvent] {#python-filter}

Para acceder y filtrar un conjunto de datos [!DNL ExperienceEvent] en un bloc de notas [!DNL Python], debe proporcionar el identificador del conjunto de datos (`{DATASET_ID}`) junto con las reglas de filtro que definen un intervalo de tiempo específico mediante operadores lógicos. Cuando se define un intervalo de tiempo, se ignora cualquier paginación especificada y se considera todo el conjunto de datos.

A continuación, se describe una lista de operadores de filtrado:

- `eq()`: igual a
- `gt()`: mayor que
- `ge()`: mayor o igual que
- `lt()`: menor que
- `le()`: menor o igual que
- `And()`: operador lógico AND
- `Or()`: operador lógico OR

La siguiente celda filtra un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y el final del 31 de diciembre de 2019.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## Portátiles R {#r-notebooks}

Los blocs de notas de R permiten paginar datos al acceder a conjuntos de datos. A continuación se muestra un código de muestra para leer datos con y sin paginación. Para obtener más información sobre los blocs de notas de Starter R disponibles, visite la sección [[!DNL JupyterLab] Launcher](./overview.md#launcher) en la guía del usuario de JupyterLab.

La siguiente documentación de R describe los siguientes conceptos:

- [Leer de un conjunto de datos](#r-read-dataset)
- [Escribir en un conjunto de datos](#write-r)
- [Filtrado de datos de ExperienceEvent](#r-filter)

### Lectura de un conjunto de datos en R {#r-read-dataset}

**Sin paginación:**

Al ejecutar el siguiente código, se leerá todo el conjunto de datos. Si la ejecución se realiza correctamente, los datos se guardarán como un marco de datos Pandas al que hace referencia la variable `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**Con paginación:**

Al ejecutar el siguiente código se leerán los datos del conjunto de datos especificado. La paginación se logra limitando y desplazando los datos a través de las funciones `limit()` y `offset()` respectivamente. La limitación de datos hace referencia al número máximo de puntos de datos que se van a leer, mientras que la compensación hace referencia al número de puntos de datos que se van a omitir antes de leer los datos. Si la operación de lectura se ejecuta correctamente, los datos se guardarán como un marco de datos Pandas al que hace referencia la variable `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Escribir en un conjunto de datos en R {#write-r}

Para escribir en un conjunto de datos de su bloc de notas de JupyterLab, seleccione la pestaña Icono de datos (resaltada a continuación) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL Schemas]**. Seleccione **[!UICONTROL Datasets]**, haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Write Data in Notebook]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Use **[!UICONTROL Write Data in Notebook]** para generar una celda de escritura con el conjunto de datos seleccionado.
- Use **[!UICONTROL Explore Data in Notebook]** para generar una celda de lectura con el conjunto de datos seleccionado.

Como alternativa, puede copiar y pegar la siguiente celda de código:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrar datos de [!DNL ExperienceEvent] {#r-filter}

Para acceder y filtrar un conjunto de datos [!DNL ExperienceEvent] en un bloc de notas R, debe proporcionar el identificador del conjunto de datos (`{DATASET_ID}`) junto con las reglas de filtrado que definen un intervalo de tiempo específico mediante operadores lógicos. Cuando se define un intervalo de tiempo, se ignora cualquier paginación especificada y se considera todo el conjunto de datos.

A continuación, se describe una lista de operadores de filtrado:

- `eq()`: igual a
- `gt()`: mayor que
- `ge()`: mayor o igual que
- `lt()`: menor que
- `le()`: menor o igual que
- `And()`: operador lógico AND
- `Or()`: operador lógico OR

La siguiente celda filtra un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y el final del 31 de diciembre de 2019.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## Portátiles PySpark 3 {#pyspark-notebook}

La documentación de PySpark a continuación describe los siguientes conceptos:

- [Inicializar sparkSession](#spark-initialize)
- [Leer y escribir datos](#magic)
- [Crear un marco de datos local](#pyspark-create-dataframe)
- [Filtrado de datos de ExperienceEvent](#pyspark-filter-experienceevent)

### Inicializando sparkSession {#spark-initialize}

Todos los blocs de notas de [!DNL Spark] 2.4 requieren que inicialice la sesión con el siguiente código de repetidor.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Usar %dataset para leer y escribir con un bloc de notas PySpark 3 {#magic}

Con la introducción de [!DNL Spark] 2.4, se proporciona magia personalizada de `%dataset` para su uso en portátiles PySpark 3 ([!DNL Spark] 2.4). Para obtener más información sobre los comandos mágicos disponibles en el núcleo de IPython, visite la [documentación mágica de IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Uso**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Descripción**

Un comando mágico [!DNL Data Science Workspace] personalizado para leer o escribir un conjunto de datos de un bloc de notas [!DNL PySpark] ([!DNL Python] 3 kernel).

| Nombre | Descripción | Requerido |
| --- | --- | --- |
| `{action}` | Tipo de acción que se va a realizar en el conjunto de datos. Hay dos acciones disponibles, &quot;leer&quot; o &quot;escribir&quot;. | Sí |
| `--datasetId {id}` | Se utiliza para proporcionar el ID del conjunto de datos que se va a leer o escribir. | Sí |
| `--dataFrame {df}` | El marco de datos de los pandas. <ul><li> Cuando la acción es &quot;leer&quot;, {df} es la variable donde están disponibles los resultados de la operación de lectura del conjunto de datos (como un marco de datos). </li><li> Cuando la acción es &quot;write&quot;, este marco de datos {df} se escribe en el conjunto de datos. </li></ul> | Sí |
| `--mode` | Un parámetro adicional que cambia la forma en que se leen los datos. Los parámetros permitidos son &quot;batch&quot; e &quot;interactive&quot;. De forma predeterminada, el modo está configurado en &quot;por lotes&quot;.<br> Se recomienda usar el modo &quot;interactivo&quot; para aumentar el rendimiento de las consultas en conjuntos de datos más pequeños. | Sí |

>[!TIP]
>
>Revise las tablas PySpark dentro de la sección [límites de datos del bloc de notas](#notebook-data-limits) para determinar si `mode` debe establecerse en `interactive` o `batch`.

**Ejemplos**

- **Leer ejemplo**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Ejemplo de escritura**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> Almacenar datos en caché utilizando `df.cache()` antes de escribir datos puede mejorar en gran medida el rendimiento del bloc de notas. Esto puede ayudarle si recibe cualquiera de los siguientes errores:
> 
> - Se ha anulado el trabajo debido a un error de fase... Solo puede comprimir RDD con el mismo número de elementos en cada partición.
> - Cliente RPC remoto desasociado y otros errores de memoria.
> - Rendimiento deficiente al leer y escribir conjuntos de datos.
> 
> Consulte la [guía de solución de problemas](../troubleshooting-guide.md) para obtener más información.

Puede generar automáticamente los ejemplos anteriores en la compra de JupyterLab mediante el siguiente método:

Seleccione la pestaña Icono de datos (resaltada a continuación) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL Schemas]**. Seleccione **[!UICONTROL Datasets]**, haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Write Data in Notebook]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.

- Use **[!UICONTROL Explore Data in Notebook]** para generar una celda de lectura.
- Use **[!UICONTROL Write Data in Notebook]** para generar una celda de escritura.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Crear un marco de datos local {#pyspark-create-dataframe}

Para crear un marco de datos local con PySpark 3, utilice consultas SQL. Por ejemplo:

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>También se puede especificar una muestra de semilla opcional, como un valor booleano con Replacement, una fracción doble o una semilla larga.

### Filtrar datos de [!DNL ExperienceEvent] {#pyspark-filter-experienceevent}

Para acceder y filtrar un conjunto de datos de [!DNL ExperienceEvent] en un bloc de notas de PySpark es necesario proporcionar la identidad del conjunto de datos (`{DATASET_ID}`), la identidad IMS de su organización y las reglas de filtrado que definen un intervalo de tiempo específico. Un intervalo de tiempo de filtrado se define mediante la función `spark.sql()`, donde el parámetro de función es una cadena de consulta SQL.

Las celdas siguientes filtran un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y el final del 31 de diciembre de 2019.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Portátiles Scala {#scala-notebook}

La documentación siguiente contiene ejemplos de los siguientes conceptos:

- [Inicializar sparkSession](#scala-initialize)
- [Leer un conjunto de datos](#read-scala-dataset)
- [Escribir en un conjunto de datos](#scala-write-dataset)
- [Crear un marco de datos local](#scala-create-dataframe)
- [Filtrado de datos de ExperienceEvent](#scala-experienceevent)

### Inicializando SparkSession {#scala-initialize}

Todos los portátiles Scala requieren que inicialice la sesión con el siguiente código de repetidor:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Leer un conjunto de datos {#read-scala-dataset}

En Scala, puede importar `clientContext` para obtener y devolver valores de Experience Platform, lo que elimina la necesidad de definir variables como `var userToken`. En el siguiente ejemplo de Scala, `clientContext` se usa para obtener y devolver todos los valores necesarios para leer un conjunto de datos.

>[!IMPORTANT]
>
> Almacenar datos en caché utilizando `df.cache()` antes de escribir datos puede mejorar en gran medida el rendimiento del bloc de notas. Esto puede ayudarle si recibe cualquiera de los siguientes errores:
> 
> - Se ha anulado el trabajo debido a un error de fase... Solo puede comprimir RDD con el mismo número de elementos en cada partición.
> - Cliente RPC remoto desasociado y otros errores de memoria.
> - Rendimiento deficiente al leer y escribir conjuntos de datos.
> 
> Consulte la [guía de solución de problemas](../troubleshooting-guide.md) para obtener más información.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Elemento | Descripción |
| ------- | ----------- |
| df1 | Variable que representa el marco de datos de Pandas que se utiliza para leer y escribir datos. |
| token de usuario | El token de usuario que se recupera automáticamente usando `clientContext.getUserToken()`. |
| service-token | El token de servicio que se recupera automáticamente usando `clientContext.getServiceToken()`. |
| ims-org | Identificador de organización que se recupera automáticamente usando `clientContext.getOrgId()`. |
| api-key | La clave de API que se recupera automáticamente usando `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise las tablas de Scala dentro de la sección [límites de datos del bloc de notas](#notebook-data-limits) para determinar si `mode` debe establecerse en `interactive` o `batch`.

Puede generar automáticamente el ejemplo anterior en la compra de JupyterLab mediante el siguiente método:

Seleccione la pestaña Icono de datos (resaltada a continuación) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL Schemas]**. Seleccione **[!UICONTROL Datasets]**, haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Explore Data in Notebook]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.

Y

- Use **[!UICONTROL Explore Data in Notebook]** para generar una celda de lectura.
- Use **[!UICONTROL Write Data in Notebook]** para generar una celda de escritura.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Escribir en un conjunto de datos {#scala-write-dataset}

En Scala, puede importar `clientContext` para obtener y devolver valores de Experience Platform, lo que elimina la necesidad de definir variables como `var userToken`. En el siguiente ejemplo de Scala, `clientContext` se usa para definir y devolver todos los valores necesarios para escribir en un conjunto de datos.

>[!IMPORTANT]
>
> Almacenar datos en caché utilizando `df.cache()` antes de escribir datos puede mejorar en gran medida el rendimiento del bloc de notas. Esto puede ayudarle si recibe cualquiera de los siguientes errores:
> 
> - Se ha anulado el trabajo debido a un error de fase... Solo puede comprimir RDD con el mismo número de elementos en cada partición.
> - Cliente RPC remoto desasociado y otros errores de memoria.
> - Rendimiento deficiente al leer y escribir conjuntos de datos.
> 
> Consulte la [guía de solución de problemas](../troubleshooting-guide.md) para obtener más información.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| elemento | descripción |
| ------- | ----------- |
| df1 | Variable que representa el marco de datos de Pandas que se utiliza para leer y escribir datos. |
| token de usuario | El token de usuario que se recupera automáticamente usando `clientContext.getUserToken()`. |
| service-token | El token de servicio que se recupera automáticamente usando `clientContext.getServiceToken()`. |
| ims-org | Identificador de organización que se recupera automáticamente usando `clientContext.getOrgId()`. |
| api-key | La clave de API que se recupera automáticamente usando `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise las tablas de Scala dentro de la sección [límites de datos del bloc de notas](#notebook-data-limits) para determinar si `mode` debe establecerse en `interactive` o `batch`.

### crear un marco de datos local {#scala-create-dataframe}

Para crear un marco de datos local con Scala, se requieren consultas SQL. Por ejemplo:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrar datos de [!DNL ExperienceEvent] {#scala-experienceevent}

Para acceder y filtrar un conjunto de datos de [!DNL ExperienceEvent] en un bloc de notas de Scala es necesario proporcionar la identidad del conjunto de datos (`{DATASET_ID}`), la identidad de IMS de su organización y las reglas de filtrado que definen un intervalo de tiempo específico. Un intervalo de tiempo de filtrado se define mediante la función `spark.sql()`, donde el parámetro de función es una cadena de consulta SQL.

Las celdas siguientes filtran un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y el final del 31 de diciembre de 2019.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## Próximos pasos

Este documento abarcaba las directrices generales para acceder a conjuntos de datos mediante cuadernos de JupyterLab. Para obtener ejemplos más detallados sobre la consulta de conjuntos de datos, visite la documentación de [Query Service in JupyterLab Notebooks](./query-service.md). Para obtener más información sobre cómo explorar y visualizar sus conjuntos de datos, visite el documento de [análisis de los datos mediante blocs de notas](./analyze-your-data.md).

## Indicadores SQL opcionales para [!DNL Query Service] {#optional-sql-flags-for-query-service}

Esta tabla describe los indicadores SQL opcionales que se pueden usar para [!DNL Query Service].

| **Indicador** | **Descripción** |
| --- | --- |
| `-h`, `--help` | Mostrar el mensaje de ayuda y salir. |
| `-n`, `--notify` | Alternar opción para notificar los resultados de la consulta. |
| `-a`, `--async` | El uso de este indicador ejecuta la consulta de forma asíncrona y puede liberar el núcleo mientras se ejecuta la consulta. Tenga cuidado al asignar resultados de consulta a variables, ya que puede ser indefinido si la consulta no está completa. |
| `-d`, `--display` | El uso de este indicador evita que se muestren los resultados. |
