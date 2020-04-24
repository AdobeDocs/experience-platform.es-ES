---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: Guía del SDK de la plataforma
topic: SDK authoring
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Guía del SDK de la plataforma

Este tutorial le proporciona información sobre la conversión `data_access_sdk_python` al nuevo Python `platform_sdk` en Python y R. Este tutorial proporciona información sobre las siguientes operaciones:

- [Generar autenticación](#build-authentication)
- [Lectura básica de los datos](#basic-reading-of-data)
- [Escritura básica de datos](#basic-writing-of-data)

## Generar autenticación {#build-authentication}

La autenticación es necesaria para realizar llamadas a Adobe Experience Platform y está compuesta por una clave de API, un ID de organización de IMS, un token de usuario y un token de servicio.

### Python

Si está utilizando un bloc de notas Jupyter, utilice el código siguiente para crear el `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Si no está utilizando Jupyter Notebook o necesita cambiar la organización de IMS, utilice el siguiente código de muestra:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Si está utilizando un bloc de notas Jupyter, utilice el código siguiente para crear el `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Si no está utilizando Jupyter Notebook o necesita cambiar la organización de IMS, utilice el siguiente código de muestra:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Lectura básica de los datos {#basic-reading-of-data}

Con el nuevo SDK de plataforma, el tamaño máximo de lectura es de 32 GB, con un tiempo máximo de lectura de 10 minutos.

Si el tiempo de lectura tarda demasiado, puede intentar utilizar una de las siguientes opciones de filtrado:

- [Filtrado de datos por desplazamiento y límite](#filter-by-offset-and-limit)
- [Filtrado de datos por fecha](#filter-by-date)
- [Filtrado de datos por columna](#filter-by-selected-columns)
- [Obtención de resultados ordenados](#get-sorted-results)

>[!NOTE] La organización de IMS se establece dentro de la `client_context`.

### Python

Para leer datos en Python, utilice el código de muestra siguiente:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Para leer los datos en R, utilice el código de muestra siguiente:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrar por desplazamiento y límite {#filter-by-offset-and-limit}

Ya no se admite el filtrado por ID de lote, por lo que debe utilizar `offset` y `limit`.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Filtrar por fecha {#filter-by-date}

La granularidad del filtro de fechas ahora se define mediante la marca de tiempo, en lugar de establecerse por el día.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

El nuevo SDK de plataforma admite las siguientes operaciones:

| Operación | Función |
| --------- | -------- |
| Es igual a (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Greater than or equal to (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| And (`&`) | `And()` |
| O (`|`) | `Or()` |

## Filtrar por columnas seleccionadas {#filter-by-selected-columns}

Para restringir aún más la lectura de datos, también puede filtrar por nombre de columna.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Obtener resultados ordenados {#get-sorted-results}

Los resultados recibidos se pueden ordenar por columnas especificadas del conjunto de datos de destinatario y en su orden (asc/desc) respectivamente.

En el siguiente ejemplo, dataframe se ordena primero por &quot;column-a&quot; en orden ascendente. Las filas que tienen los mismos valores para &quot;columna-a&quot; se ordenan por &quot;columna-b&quot; en orden descendente.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Escritura básica de datos {#basic-writing-of-data}

>[!NOTE] La organización de IMS se establece dentro de la `client_context`.

Para escribir datos en Python y R, utilice uno de los siguientes ejemplos:

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Pasos siguientes

Una vez configurado el cargador de datos, los datos se preparan y luego se dividen en los conjuntos de datos `platform_sdk` y `train` `val` . Para obtener más información sobre la preparación de datos y la ingeniería de características, visite la sección sobre la preparación de [datos y la ingeniería](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) de características en el tutorial para crear una fórmula con portátiles JupyterLab.