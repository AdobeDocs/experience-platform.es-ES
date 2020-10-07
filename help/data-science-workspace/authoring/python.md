---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api;read python;write python
solution: Experience Platform
title: Acceso a datos mediante Python
topic: tutorial
type: Tutorial
description: El siguiente documento contiene ejemplos de cómo acceder a datos en Python para utilizarlos en Área de trabajo de ciencias de datos.
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Acceso a datos mediante Python

El siguiente documento contiene ejemplos de cómo acceder a los datos mediante Python para utilizarlos en Área de trabajo de ciencias de datos. Para obtener información sobre el acceso a los datos mediante portátiles JupyterLab, visite la documentación de acceso [a los datos de los portátiles de](../jupyterlab/access-notebook-data.md) JupyterLab.

## Lectura de un conjunto de datos

Después de configurar las variables de entorno y completar la instalación, el conjunto de datos ahora se puede leer en el dataframe de pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SELECCIONAR columnas del conjunto de datos

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obtener información de partición:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Cláusula DISTINCT

La cláusula DISTINCT permite recuperar todos los valores distintos en un nivel de fila/columna, eliminando todos los valores de duplicado de la respuesta.

A continuación se muestra un ejemplo del uso de la `distinct()` función:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### cláusula WHERE

Puede utilizar ciertos operadores en Python para ayudar a filtrar el conjunto de datos.

>[!NOTE]
>
>Las funciones utilizadas para filtrar distinguen entre mayúsculas y minúsculas.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

A continuación se muestra un ejemplo del uso de estas funciones de filtrado:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### Cláusula ORDER BY

La cláusula ORDER BY permite ordenar los resultados recibidos por una columna específica en un orden específico (ascendente o descendente). Esto se lleva a cabo mediante la `sort()` función .

A continuación se muestra un ejemplo del uso de la `sort()` función:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula LIMIT

La cláusula LIMIT permite limitar el número de registros recibidos del conjunto de datos.

A continuación se muestra un ejemplo del uso de la `limit()` función:

```python
df = dataset_reader.limit(100).read()
```

### Cláusula OFFSET

La cláusula OFFSET permite omitir filas, desde el principio, hasta el inicio de devolver filas desde un punto posterior. En combinación con LIMIT, se puede utilizar para iterar filas en bloques.

A continuación se muestra un ejemplo del uso de la `offset()` función:

```python
df = dataset_reader.offset(100).read()
```

## Escritura de un conjunto de datos

Para escribir en un conjunto de datos, debe proporcionar el dataframe pandas al conjunto de datos.

### Escribiendo el juego de datos de pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Directorio de Userspace (Verificación)

Para trabajos de ejecución más prolongada, es posible que tenga que almacenar pasos intermedios. En casos como este, puede leer y escribir en un espacio de usuario.

>[!NOTE]
>
>Las rutas a los datos **no se almacenan** . Debe almacenar la ruta correspondiente a sus datos respectivos.

### Escribir en espacio de usuario

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Leer desde el espacio de usuario

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Pasos siguientes

Adobe Experience Platform Data Science Workspace proporciona un ejemplo de fórmula que utiliza los ejemplos de código anteriores para leer y escribir datos. Si desea obtener más información sobre cómo utilizar Python para acceder a sus datos, consulte el repositorio [de](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)Data Science Workspace Python GitHub.