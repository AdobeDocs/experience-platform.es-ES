---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;%conjunto de datos;modo interactivo;modo por lotes;Spark sdk;python sdk;acceso a datos;acceso a datos del bloc de notas
solution: Experience Platform
title: Acceso a datos en equipos portátiles de Jupyterlab
topic-legacy: Developer Guide
description: Esta guía se centra en cómo utilizar los equipos portátiles Jupyter, creados dentro de Data Science Workspace para acceder a sus datos.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 9e41db60580146fa90542ed00ceedd4eecb88b47
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 8%

---

# Acceso a datos en [!DNL Jupyterlab] blocs de notas

Cada núcleo soportado proporciona funcionalidades incorporadas que permiten leer datos de Platform desde un conjunto de datos dentro de un bloc de notas. Actualmente, JupyterLab en Adobe Experience Platform Data Science Workspace admite portátiles para [!DNL Python], R, PySpark y Scala. Sin embargo, la compatibilidad con la paginación de datos se limita a los [!DNL Python] y los portátiles R. Esta guía se centra en cómo utilizar los portátiles JupyterLab para acceder a sus datos.

## Introducción

Antes de leer esta guía, consulte la [[!DNL JupyterLab] guía del usuario](./overview.md) para obtener una introducción de alto nivel a [!DNL JupyterLab] y su función dentro de Data Science Workspace.

## Límites de datos de equipos portátiles {#notebook-data-limits}

>[!IMPORTANT]
>
>Para los blocs de notas PySpark y Scala si recibe un error con el motivo &quot;Cliente RPC remoto desasociado&quot;. Esto suele significar que el controlador o un ejecutor se está quedando sin memoria. Intente cambiar al modo [&quot;batch&quot;](#mode) para resolver este error.

La siguiente información define la cantidad máxima de datos que se pueden leer, qué tipo de datos se han utilizado y el intervalo de tiempo estimado que se tarda en leer los datos.

Para [!DNL Python] y R, se utilizó un servidor portátil configurado con 40 GB de RAM para los puntos de referencia. Para PySpark y Scala, se utilizó un clúster de databricks configurado en 64 GB de RAM, 8 núcleos, 2 DBU con un máximo de 4 trabajadores para los puntos de referencia descritos a continuación.

Los datos de esquema de ExperienceEvent utilizados variaron en su tamaño a partir de mil filas (1K) de hasta mil millones de filas (1B). Tenga en cuenta que para las métricas PySpark y [!DNL Spark] se ha utilizado un intervalo de fechas de 10 días para los datos XDM.

Los datos de esquema ad hoc se preprocesaron utilizando [!DNL Query Service] Crear tabla como selección (CTAS). Estos datos también variaron en el tamaño a partir de mil filas (1K) que oscilaban entre mil millones de filas (1B).

### Cuándo utilizar el modo por lotes frente al modo interactivo {#mode}

Al leer conjuntos de datos con portátiles PySpark y Scala, tiene la opción de utilizar el modo interactivo o el modo por lotes para leer el conjunto de datos. Interactive se realiza para obtener resultados rápidos, mientras que el modo por lotes es para conjuntos de datos grandes.

- Para los portátiles PySpark y Scala, el modo por lotes debe usarse cuando se leen 5 millones de filas de datos o más. Para obtener más información sobre la eficacia de cada modo, consulte las tablas de límite de datos [PySpark](#pyspark-data-limits) o [Scala](#scala-data-limits) a continuación.

### [!DNL Python] límites de datos del bloc de notas

**Esquema XDM ExperienceEvent:** debería poder leer un máximo de 2 millones de filas (unos 6,1 GB de datos en disco) de datos XDM en menos de 22 minutos. La adición de filas adicionales puede provocar errores.

| Número de filas | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Tamaño en disco (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (en segundos) | 20,3 | 86,8 | 63 | 659 | 1315 |

**esquema ad hoc:** debe poder leer un máximo de 5 millones de filas (~5,6 GB de datos en disco) de datos que no sean XDM (ad-hoc) en menos de 14 minutos. La adición de filas adicionales puede provocar errores.

| Número de filas | 1K | 10K | 100 K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Tamaño en disco (en MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (en segundos) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### Límites de datos de portátiles R

**Esquema XDM ExperienceEvent:** debería poder leer un máximo de 1 millón de filas de datos XDM (datos de 3 GB en disco) en menos de 13 minutos.

| Número de filas | 1K | 10K | 100 K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Tamaño en disco (MB) | 18,73 | 187,5 | 308 | 3000 |
| Núcleo R (en segundos) | 14,03 | 69,6 | 86,8 | 775 |

**esquema ad hoc:** debe poder leer un máximo de 3 millones de filas de datos ad hoc (datos de 293 MB en disco) en unos 10 minutos.

| Número de filas | 1K | 10K | 100 K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Tamaño en disco (en MB) | 0,082 | 0,612 | 9.0 | 91 | 188 | 293 |
| SDK R (en segundos) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Límites de datos de portátiles PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**Esquema XDM ExperienceEvent:** en el modo interactivo debe poder leer un máximo de 5 millones de filas (unos 13,42 GB de datos en disco) de datos XDM en unos 20 minutos. El modo interactivo solo admite hasta 5 millones de filas. Si desea leer conjuntos de datos más grandes, se sugiere cambiar al modo por lotes. En el modo por lotes, debería poder leer un máximo de 500 millones de filas (unos 1,31 TB de datos en disco) de datos XDM en unas 14 horas.

| Número de filas | 1K | 10K | 100 K | 1M | 2M | 3M | 5M | 10M | 50 M | 100 M | 500 M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamaño en disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| SDK (modo interactivo) | 33s | 32,4 s | 55.1s | 253,5 s | 489,2 | 729,6 s | 1206,8 s | - | - | - | - |
| SDK (modo por lotes) | 815,8 s | 492,8 s | 379,1s | 637,4 s | 624,5 s | 869,2 | 1104.1s | 1786s | 5387,2 s | 10624,6s | 50547s |

**esquema ad hoc:** En el modo interactivo, debe poder leer un máximo de 5 millones de filas (unos 5,36 GB de datos en disco) de datos que no sean XDM en menos de 3 minutos. En el modo Lote, debería poder leer un máximo de 100 millones de filas (unos 1,05 TB de datos en disco) de datos que no sean XDM en unos 18 minutos.

| Número de filas | 1K | 10K | 100 K | 1M | 2M | 3M | 5M | 10M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Tamaño en disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modo interactivo del SDK (en segundos) | 28,2 s | 18,6 s | 20,8 s | 20,9s | 23,8 s | 21,7 s | 24,7 s | - | - | - | - | - |
| Modo por lotes de SDK (en segundos) | 428,8 s | 578,8 s | 641,4 s | 538,5 s | 630,9s | 467,3 s | 411s | 675s | 702s | 719,2 | 1022.1s | 1122,3s |

### [!DNL Spark] Límites de datos de portátiles (kernel Scala):  {#scala-data-limits}

**Esquema XDM ExperienceEvent:** en el modo interactivo debe poder leer un máximo de 5 millones de filas (unos 13,42 GB de datos en disco) de datos XDM en unos 18 minutos. El modo interactivo solo admite hasta 5 millones de filas. Si desea leer conjuntos de datos más grandes, se sugiere cambiar al modo por lotes. En el modo por lotes, debería poder leer un máximo de 500 millones de filas (unos 1,31 TB de datos en disco) de datos XDM en unas 14 horas.

| Número de filas | 1K | 10K | 100 K | 1M | 2M | 3M | 5M | 10M | 50 M | 100 M | 500 M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamaño en disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| Modo interactivo del SDK (en segundos) | 37,9 s | 22,7 s | 45,6 s | 231,7 s | 444,7 s | 660,6 s | 1100s | - | - | - | - |
| Modo por lotes de SDK (en segundos) | 374,4 s | 398,5 s | 527s | 487,9s | 588,9s | 829s | 939.1s | 1441s | 5473,2 s | 10118,8 | 49207,6 |

**esquema ad hoc:** En el modo interactivo, debe poder leer un máximo de 5 millones de filas (unos 5,36 GB de datos en disco) de datos que no sean XDM en menos de 3 minutos. En el modo por lotes, debería poder leer un máximo de 100 millones de filas (unos 1,05 TB de datos en disco) de datos que no sean XDM en unos 16 minutos.

| Número de filas | 1K | 10K | 100 K | 1M | 2M | 3M | 5M | 10M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Tamaño en disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modo interactivo del SDK (en segundos) | 35,7 s | 31s | 19,5 s | 25,3 s | 23s | 33,2 s | 25,5 s | - | - | - | - | - |
| Modo por lotes de SDK (en segundos) | 448,8 s | 459,7 s | 519s | 475,8 s | 599,9s | 347,6 s | 407,8 s | 397s | 518,8 s | 487,9s | 760,2 s | 975,4 s |

## Portátiles Python {#python-notebook}

[!DNL Python] los blocs de notas permiten paginar datos al acceder a conjuntos de datos. A continuación se muestra el código de muestra para leer datos con o sin paginación. Para obtener más información sobre los portátiles Python de inicio disponibles, visite la sección [[!DNL JupyterLab] Launcher](./overview.md#launcher) dentro de la guía del usuario de JupyterLab.

La documentación de Python a continuación describe los siguientes conceptos:

- [Lectura desde un conjunto de datos](#python-read-dataset)
- [Escribir en un conjunto de datos](#write-python)
- [Datos de consulta](#query-data-python)
- [Filtrar datos de ExperienceEvent](#python-filter)

### Leer desde un conjunto de datos en Python {#python-read-dataset}

**Sin paginación:**

Al ejecutar el siguiente código se leerá todo el conjunto de datos. Si la ejecución se realiza correctamente, los datos se guardarán como un dataframe de Pandas al que hace referencia la variable `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Con paginación:**

Al ejecutar el siguiente código se leerán los datos del conjunto de datos especificado. La paginación se logra limitando y compensando los datos a través de las funciones `limit()` y `offset()` respectivamente. La limitación de datos se refiere al número máximo de puntos de datos que se deben leer, mientras que la compensación se refiere al número de puntos de datos que se deben omitir antes de leer los datos. Si la operación de lectura se ejecuta correctamente, los datos se guardarán como un dataframe de Pandas al que hace referencia la variable `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Escribir en un conjunto de datos en Python {#write-python}

Para escribir en un conjunto de datos en su bloc de notas de JupyterLab, seleccione la pestaña Icono de datos (resaltado abajo) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL schemas]**. Seleccione **[!UICONTROL Datasets]** y haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Escribir datos en el bloc de notas]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.

![](../images/jupyterlab/data-access/write-dataset.png)

- Utilice **[!UICONTROL Escribir datos en el bloc de notas]** para generar una celda de escritura con el conjunto de datos seleccionado.
- Utilice **[!UICONTROL Explorar datos en el bloc de notas]** para generar una celda de lectura con el conjunto de datos seleccionado.
- Utilice **[!UICONTROL Datos de consulta en el bloc de notas]** para generar una celda de consulta básica con el conjunto de datos seleccionado.

Como alternativa, puede copiar y pegar la siguiente celda de código. Reemplace `{DATASET_ID}` y `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Consultar datos utilizando [!DNL Query Service] en [!DNL Python] {#query-data-python}

[!DNL JupyterLab] on  [!DNL Platform] permite utilizar SQL en un  [!DNL Python] bloc de notas para acceder a los datos a través del servicio de consulta de  [Adobe Experience Platform](https://www.adobe.com/go/query-service-home-en). El acceso a los datos a través de [!DNL Query Service] puede resultar útil para tratar con conjuntos de datos grandes debido a sus tiempos de ejecución superiores. Tenga en cuenta que la consulta de datos mediante [!DNL Query Service] tiene un límite de tiempo de procesamiento de diez minutos.

Antes de utilizar [!DNL Query Service] en [!DNL JupyterLab], asegúrese de tener una comprensión práctica de la sintaxis [[!DNL Query Service] SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

Para realizar consultas de datos mediante [!DNL Query Service] es necesario proporcionar el nombre del conjunto de datos de destino. Puede generar las celdas de código necesarias buscando el conjunto de datos deseado mediante el **[!UICONTROL Explorador de datos]**. Haga clic con el botón derecho en la lista de conjuntos de datos y haga clic en **[!UICONTROL Query Data in Notebook]** para generar dos celdas de código en el bloc de notas. Estas dos celdas se describen con más detalle a continuación.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Para utilizar [!DNL Query Service] en [!DNL JupyterLab], primero debe crear una conexión entre el bloc de notas [!DNL Python] en funcionamiento y [!DNL Query Service]. Esto se puede lograr ejecutando la primera celda generada.

```python
qs_connect()
```

En la segunda celda generada, la primera línea debe definirse antes que la consulta SQL. De forma predeterminada, la celda generada define una variable opcional (`df0`) que guarda los resultados de la consulta como un dataframe de Pandas. <br>El  `-c QS_CONNECTION` argumento es obligatorio y le indica al núcleo que ejecute la consulta SQL con  [!DNL Query Service]. Consulte el [apéndice](#optional-sql-flags-for-query-service) para obtener una lista de argumentos adicionales.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Se puede hacer referencia a las variables Python directamente dentro de una consulta SQL utilizando sintaxis con formato de cadena y ajustando las variables entre llaves (`{}`), como se muestra en el siguiente ejemplo:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrar [!DNL ExperienceEvent] datos {#python-filter}

Para acceder y filtrar un conjunto de datos [!DNL ExperienceEvent] en un bloc de notas [!DNL Python], debe proporcionar el ID del conjunto de datos (`{DATASET_ID}`) junto con las reglas de filtro que definen un intervalo de tiempo específico mediante operadores lógicos. Cuando se define un intervalo de tiempo, se ignora cualquier paginación especificada y se considera todo el conjunto de datos.

A continuación se describe una lista de operadores de filtrado:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`: Operador AND lógico
- `Or()`: Operador OR lógico

La siguiente celda filtra un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y finales del 31 de diciembre de 2019.

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

Los portátiles R permiten paginar los datos al acceder a los conjuntos de datos. A continuación se muestra el código de muestra para leer datos con o sin paginación. Para obtener más información sobre los portátiles R de inicio disponibles, visite la sección [[!DNL JupyterLab] Launcher](./overview.md#launcher) dentro de la guía del usuario de JupyterLab.

La documentación R que aparece a continuación describe los siguientes conceptos:

- [Lectura desde un conjunto de datos](#r-read-dataset)
- [Escribir en un conjunto de datos](#write-r)
- [Filtrar datos de ExperienceEvent](#r-filter)

### Leer desde un conjunto de datos en R {#r-read-dataset}

**Sin paginación:**

Al ejecutar el siguiente código se leerá todo el conjunto de datos. Si la ejecución se realiza correctamente, los datos se guardarán como un dataframe de Pandas al que hace referencia la variable `df0`.

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

Al ejecutar el siguiente código se leerán los datos del conjunto de datos especificado. La paginación se logra limitando y compensando los datos a través de las funciones `limit()` y `offset()` respectivamente. La limitación de datos se refiere al número máximo de puntos de datos que se deben leer, mientras que la compensación se refiere al número de puntos de datos que se deben omitir antes de leer los datos. Si la operación de lectura se ejecuta correctamente, los datos se guardarán como un dataframe de Pandas al que hace referencia la variable `df0`.

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

Para escribir en un conjunto de datos en su bloc de notas de JupyterLab, seleccione la pestaña Icono de datos (resaltado abajo) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL schemas]**. Seleccione **[!UICONTROL Datasets]** y haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Escribir datos en el bloc de notas]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Utilice **[!UICONTROL Escribir datos en el bloc de notas]** para generar una celda de escritura con el conjunto de datos seleccionado.
- Utilice **[!UICONTROL Explorar datos en el bloc de notas]** para generar una celda de lectura con el conjunto de datos seleccionado.

Como alternativa, puede copiar y pegar la siguiente celda de código:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrar [!DNL ExperienceEvent] datos {#r-filter}

Para acceder y filtrar un conjunto de datos [!DNL ExperienceEvent] en un bloc de notas R, debe proporcionar el ID del conjunto de datos (`{DATASET_ID}`) junto con las reglas de filtro que definen un intervalo de tiempo específico mediante operadores lógicos. Cuando se define un intervalo de tiempo, se ignora cualquier paginación especificada y se considera todo el conjunto de datos.

A continuación se describe una lista de operadores de filtrado:

- `eq()`: Igual a
- `gt()`: Bueno que
- `ge()`: Bueno que o igual a
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`: Operador AND lógico
- `Or()`: Operador OR lógico

La siguiente celda filtra un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y finales del 31 de diciembre de 2019.

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

La siguiente documentación de PySpark describe los siguientes conceptos:

- [Inicializar sparkSession](#spark-initialize)
- [Lectura y escritura de datos](#magic)
- [Crear un datafame local](#pyspark-create-dataframe)
- [Filtrar datos de ExperienceEvent](#pyspark-filter-experienceevent)

### Inicializando sparkSession {#spark-initialize}

Todos los [!DNL Spark] blocs de notas 2.4 requieren que inicialice la sesión con el siguiente código repetitivo.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Uso de %dataset para leer y escribir con un bloc de notas PySpark 3 {#magic}

Con la introducción de [!DNL Spark] 2.4, `%dataset` la magia personalizada se suministra para su uso en portátiles PySpark 3 ([!DNL Spark] 2.4). Para obtener más información sobre los comandos mágicos disponibles en el núcleo IPython, visite la [documentación mágica de IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Uso**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Descripción**

Un comando mágico personalizado [!DNL Data Science Workspace] para leer o escribir un conjunto de datos de un bloc de notas [!DNL PySpark] ([!DNL Python] 3 kernel).

| Nombre | Descripción | Requerido |
| --- | --- | --- |
| `{action}` | Tipo de acción que se realizará en el conjunto de datos. Hay dos acciones disponibles: &quot;leer&quot; o &quot;escribir&quot;. | Sí |
| `--datasetId {id}` | Se utiliza para proporcionar el ID del conjunto de datos para leer o escribir. | Sí |
| `--dataFrame {df}` | Los pandas dataframe. <ul><li> Cuando la acción es &quot;leída&quot;, {df} es la variable donde los resultados de la operación de lectura del conjunto de datos están disponibles (como un dataframe). </li><li> Cuando la acción es &quot;write&quot;, este dataframe {df} se escribe en el conjunto de datos. </li></ul> | Sí |
| `--mode` | Un parámetro adicional que cambia la forma en que se leen los datos. Los parámetros permitidos son &quot;por lotes&quot; e &quot;interactivo&quot;. De forma predeterminada, el modo está configurado en &quot;batch&quot;.<br> Se recomienda el modo &quot;interactivo&quot; para aumentar el rendimiento de la consulta en conjuntos de datos más pequeños. | Sí |

>[!TIP]
>
>Revise las tablas PySpark en la sección [límites de datos del bloc de notas](#notebook-data-limits) para determinar si `mode` debe establecerse en `interactive` o `batch`.

**Ejemplos**

- **Ejemplo** de lectura:  `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Ejemplo** de escritura:  `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> El almacenamiento en caché de datos mediante `df.cache()` antes de escribir datos puede mejorar considerablemente el rendimiento del bloc de notas. Esto puede ayudarle si está recibiendo cualquiera de los siguientes errores:
> 
> - Trabajo anulado debido a un error en la etapa ... Solo puede comprimir RDD con el mismo número de elementos en cada partición.
> - Cliente RPC remoto desasociado y otros errores de memoria.
> - Rendimiento deficiente al leer y escribir conjuntos de datos.

> 
> 
Consulte la [guía de solución de problemas](../troubleshooting-guide.md) para obtener más información.

Puede generar automáticamente los ejemplos anteriores en JupyterLab buy utilizando el siguiente método:

Seleccione la pestaña Icono de datos (resaltado abajo) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL schemas]**. Seleccione **[!UICONTROL Datasets]** y haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Escribir datos en el bloc de notas]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.

- Utilice **[!UICONTROL Explorar datos en el bloc de notas]** para generar una celda de lectura.
- Utilice **[!UICONTROL Escribir datos en el bloc de notas]** para generar una celda de escritura.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Crear un dataframe local {#pyspark-create-dataframe}

Para crear un dataframe local utilizando PySpark 3, utilice consultas SQL. Por ejemplo:

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
>También puede especificar una muestra de origen opcional, como un booleano con Sustitución, fracción doble o una semilla larga.

### Filtrar [!DNL ExperienceEvent] datos {#pyspark-filter-experienceevent}

El acceso y el filtrado de un conjunto de datos [!DNL ExperienceEvent] en un bloc de notas de PySpark requiere que proporcione la identidad del conjunto de datos (`{DATASET_ID}`), la identidad IMS de su organización y las reglas de filtro que definan un intervalo de tiempo específico. Un intervalo de tiempo de filtrado se define mediante la función `spark.sql()`, donde el parámetro de función es una cadena de consulta SQL.

Las siguientes celdas filtran un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y finales del 31 de diciembre de 2019.

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
- [Crear un datafame local](#scala-create-dataframe)
- [Filtrar datos de ExperienceEvent](#scala-experienceevent)

### Inicializando SparkSession {#scala-initialize}

Todos los blocs de notas Scala requieren que inicialice la sesión con el siguiente código repetitivo:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Leer un conjunto de datos {#read-scala-dataset}

En Scala, puede importar `clientContext` para obtener y devolver valores de Platform, lo que elimina la necesidad de definir variables como `var userToken`. En el ejemplo de Scala que se muestra a continuación, `clientContext` se utiliza para obtener y devolver todos los valores necesarios para leer un conjunto de datos.

>[!IMPORTANT]
>
> El almacenamiento en caché de datos mediante `df.cache()` antes de escribir datos puede mejorar considerablemente el rendimiento del bloc de notas. Esto puede ayudarle si está recibiendo cualquiera de los siguientes errores:
> 
> - Trabajo anulado debido a un error en la etapa ... Solo puede comprimir RDD con el mismo número de elementos en cada partición.
> - Cliente RPC remoto desasociado y otros errores de memoria.
> - Rendimiento deficiente al leer y escribir conjuntos de datos.

> 
> 
Consulte la [guía de solución de problemas](../troubleshooting-guide.md) para obtener más información.

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
| df1 | Variable que representa el dataframe de Pandas utilizado para leer y escribir datos. |
| user-token | El token de usuario que se obtiene automáticamente mediante `clientContext.getUserToken()`. |
| service-token | El token de servicio que se obtiene automáticamente mediante `clientContext.getServiceToken()`. |
| ims-org | El ID de organización de IMS que se obtiene automáticamente mediante `clientContext.getOrgId()`. |
| api-key | La clave de API que se obtiene automáticamente mediante `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise las tablas Scala de la sección [límites de datos del bloc de notas](#notebook-data-limits) para determinar si `mode` debe establecerse en `interactive` o `batch`.

Puede generar automáticamente el ejemplo anterior en JupyterLab buy utilizando el siguiente método:

Seleccione la pestaña Icono de datos (resaltado abajo) en la navegación izquierda de JupyterLab. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL schemas]**. Seleccione **[!UICONTROL Datasets]** y haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Explorar datos en el bloc de notas]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas.
Y
- Utilice **[!UICONTROL Explorar datos en el bloc de notas]** para generar una celda de lectura.
- Utilice **[!UICONTROL Escribir datos en el bloc de notas]** para generar una celda de escritura.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Escribir en un conjunto de datos {#scala-write-dataset}

En Scala, puede importar `clientContext` para obtener y devolver valores de Platform, lo que elimina la necesidad de definir variables como `var userToken`. En el ejemplo Scala que se muestra a continuación, `clientContext` se utiliza para definir y devolver todos los valores necesarios para escribir en un conjunto de datos.

>[!IMPORTANT]
>
> El almacenamiento en caché de datos mediante `df.cache()` antes de escribir datos puede mejorar considerablemente el rendimiento del bloc de notas. Esto puede ayudarle si está recibiendo cualquiera de los siguientes errores:
> 
> - Trabajo anulado debido a un error en la etapa ... Solo puede comprimir RDD con el mismo número de elementos en cada partición.
> - Cliente RPC remoto desasociado y otros errores de memoria.
> - Rendimiento deficiente al leer y escribir conjuntos de datos.

> 
> 
Consulte la [guía de solución de problemas](../troubleshooting-guide.md) para obtener más información.

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

| Elemento | descripción |
| ------- | ----------- |
| df1 | Variable que representa el dataframe de Pandas utilizado para leer y escribir datos. |
| user-token | El token de usuario que se obtiene automáticamente mediante `clientContext.getUserToken()`. |
| service-token | El token de servicio que se obtiene automáticamente mediante `clientContext.getServiceToken()`. |
| ims-org | El ID de organización de IMS que se obtiene automáticamente mediante `clientContext.getOrgId()`. |
| api-key | La clave de API que se obtiene automáticamente mediante `clientContext.getApiKey()`. |

>[!TIP]
>
>Revise las tablas Scala de la sección [límites de datos del bloc de notas](#notebook-data-limits) para determinar si `mode` debe establecerse en `interactive` o `batch`.

### crear un dataframe local {#scala-create-dataframe}

Para crear un dataframe local mediante Scala, se requieren consultas SQL. Por ejemplo:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrar [!DNL ExperienceEvent] datos {#scala-experienceevent}

El acceso y el filtrado de un conjunto de datos [!DNL ExperienceEvent] en un bloc de notas Scala requiere que proporcione la identidad del conjunto de datos (`{DATASET_ID}`), la identidad IMS de su organización y las reglas de filtro que definan un intervalo de tiempo específico. Un intervalo de tiempo de filtrado se define mediante la función `spark.sql()`, donde el parámetro de función es una cadena de consulta SQL.

Las siguientes celdas filtran un conjunto de datos [!DNL ExperienceEvent] a los datos existentes exclusivamente entre el 1 de enero de 2019 y finales del 31 de diciembre de 2019.

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

## Pasos siguientes

Este documento abarcaba las directrices generales para acceder a conjuntos de datos mediante blocs de notas de JupyterLab. Para obtener ejemplos más detallados sobre la consulta de conjuntos de datos, visite la documentación [Query Service in JupyterLab blocs de notas](./query-service.md) . Para obtener más información sobre cómo explorar y visualizar sus conjuntos de datos, visite el documento sobre [análisis de sus datos mediante blocs de notas](./analyze-your-data.md).

## Indicadores SQL opcionales para [!DNL Query Service] {#optional-sql-flags-for-query-service}

Esta tabla describe los indicadores SQL opcionales que se pueden utilizar para [!DNL Query Service].

| **Indicador** | **Descripción** |
| --- | --- |
| `-h`, `--help` | Mostrar el mensaje de ayuda y salir. |
| `-n`,  `--notify` | Alterne la opción para notificar los resultados de la consulta. |
| `-a`,  `--async` | El uso de este indicador ejecuta la consulta asincrónicamente y puede liberar el núcleo mientras se ejecuta la consulta. Tenga cuidado al asignar resultados de consulta a variables, ya que puede no estar definido si la consulta no se ha completado. |
| `-d`,  `--display` | El uso de este indicador evita que se muestren los resultados. |
