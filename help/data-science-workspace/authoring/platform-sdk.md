---
keywords: Experience Platform;guía para desarrolladores;SDK;SDK de acceso a datos;Data Science Workspace;temas populares
solution: Experience Platform
title: Creación de modelos mediante el SDK de la plataforma Adobe Experience Platform
topic-legacy: SDK authoring
description: Este tutorial le proporciona información sobre la conversión de data_access_sdk_python al nuevo Python platform_sdk en Python y R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 38c493e6306e493f4ef5caf90509bda6f4d80023
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Creación de modelos con Adobe Experience Platform [!DNL Platform] SDK

Este tutorial le proporciona información sobre la conversión `data_access_sdk_python` al nuevo Python `platform_sdk` en Python y R. Este tutorial proporciona información sobre las siguientes operaciones:

- [Generar autenticación](#build-authentication)
- [Lectura básica de los datos](#basic-reading-of-data)
- [Escritura básica de datos](#basic-writing-of-data)

## Generar autenticación {#build-authentication}

La autenticación es necesaria para realizar llamadas a [!DNL Adobe Experience Platform], y se compone de clave de API, ID de organización de IMS, un token de usuario y un token de servicio.

### Python

Si está utilizando Jupyter Notebook, utilice el siguiente código para crear el `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Si no utiliza Jupyter Notebook o necesita cambiar la organización de IMS, utilice el siguiente ejemplo de código:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Si está utilizando Jupyter Notebook, utilice el siguiente código para crear el `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Si no utiliza Jupyter Notebook o necesita cambiar la organización de IMS, utilice el siguiente ejemplo de código:

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

Con el nuevo [!DNL Platform] SDK, el tamaño máximo de lectura es de 32 GB, con un tiempo máximo de lectura de 10 minutos.

Si el tiempo de lectura está tardando demasiado, puede intentar utilizar una de las siguientes opciones de filtrado:

- [Filtrado de datos por desplazamiento y límite](#filter-by-offset-and-limit)
- [Filtrado de datos por fecha](#filter-by-date)
- [Filtrado de datos por columna](#filter-by-selected-columns)
- [Obtención de resultados ordenados](#get-sorted-results)

>[!NOTE]
>
>La organización IMS se configura dentro de la variable `client_context`.

### Python

Para leer datos en Python, utilice el siguiente ejemplo de código:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Para leer los datos en R, utilice el siguiente ejemplo de código:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrar por desplazamiento y límite {#filter-by-offset-and-limit}

Dado que ya no se admite el filtrado por ID de lote, para ampliar el ámbito de lectura de los datos, debe utilizar `offset` y `limit`.

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

La granularidad del filtrado de fechas ahora se define mediante la marca de tiempo, en lugar de configurarse por día.

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

El nuevo [!DNL Platform] El SDK admite las siguientes operaciones:

| Operación | Función |
| --------- | -------- |
| Es igual a (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Mayor o igual que (`>=`) | `ge()` |
| Menos de (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| Y (`&`) | `And()` |
| O (`|`) | `Or()` |

## Filtrar por columnas seleccionadas {#filter-by-selected-columns}

Para restringir aún más la lectura de los datos, también puede filtrar por nombre de columna.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Obtener resultados ordenados {#get-sorted-results}

Los resultados recibidos se pueden ordenar por columnas especificadas del conjunto de datos de destino y en su orden (asc/desc) respectivamente.

En el siguiente ejemplo, dataframe se ordena primero por &quot;column-a&quot; en orden ascendente. Las filas que tienen los mismos valores para la &quot;columna-a&quot; se ordenan por &quot;columna-b&quot; en orden descendente.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Escritura básica de datos {#basic-writing-of-data}

>[!NOTE]
>
>La organización IMS se configura dentro de la variable `client_context`.

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

Una vez que haya configurado la variable `platform_sdk` cargador de datos, los datos se preparan y luego se dividen en el `train` y `val` conjuntos de datos. Para obtener más información sobre la preparación de datos y la ingeniería de características, visite la sección de [preparación de datos e ingeniería de características](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) en el tutorial para crear una fórmula con [!DNL JupyterLab] portátiles.
