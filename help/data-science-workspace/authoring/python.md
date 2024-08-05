---
keywords: Experience Platform; hogar; temas populares; acceso a los datos; SDK de Python; API de acceso a datos; leer python; escribir python
solution: Experience Platform
title: Acceso a datos usando Python en Data Science Espacio de trabajo
type: Tutorial
description: El siguiente documento contiene ejemplos sobre cómo acceder a datos en Python para su uso en Data Science Espacio de trabajo.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Acceso a datos con Python en Data Science Espacio de trabajo

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

El siguiente documento contiene ejemplos sobre cómo acceder a los datos mediante Python para utilizarlo en Data Science Workspace. Para obtener información sobre el acceso a los datos mediante los blocs de notas de JupyterLab, visite la documentación de [acceso a los datos de los blocs de notas de JupyterLab](../jupyterlab/access-notebook-data.md).

## Lectura de un conjunto de datos

Después de configurar las variables de entorno y completar la instalación, el conjunto de datos ahora se puede leer en el marco de datos de pandas.

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

La cláusula DISTINCT le permite obtener todos los valores distintos en un nivel de fila/columna, eliminando todos los valores duplicado de la respuesta.

A continuación se muestra un ejemplo de uso de la `distinct()` función:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### Cláusula WHERE

Puede utilizar ciertos operadores en Python para filtrar el conjunto de datos.

>[!NOTE]
>
>Las funciones utilizadas para el filtrado distinguen entre mayúsculas y minúsculas.

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

La cláusula ORDER BY permite ordenar los resultados recibidos por una columna especificada en un orden específico (ascendente o descendente). Esto se hace mediante la función `sort()`.

A continuación se muestra un ejemplo de uso de la `sort()` función:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula LIMIT

La cláusula LIMIT le permite limitar el número de registros recibidos del conjunto de datos.

A continuación se muestra un ejemplo de uso de la `limit()` función:

```python
df = dataset_reader.limit(100).read()
```

### Cláusula OFFSET

La cláusula OFFSET permite omitir filas, desde el principio, para comenzar a devolver filas desde un punto posterior. En combinación con LIMIT, esto se puede utilizar para repetir filas en bloques.

A continuación se muestra un ejemplo del uso de la función `offset()`:

```python
df = dataset_reader.offset(100).read()
```

## Escribir un conjunto de datos

Para escribir en un conjunto de datos, debe proporcionar el marco de datos de pandas a su conjunto de datos.

### Escribiendo el marco de datos de los pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Directorio del espacio de usuario (Checkpoints)

Para trabajos de mayor duración, es posible que deba tienda pasos intermedios. En casos gustar este, puede leer y escribir en un espacio de usuario.

>[!NOTE]
>
>Las rutas a los datos no **se almacenan**. Debe tienda la ruta correspondiente a sus datos respectivos.

### Escribir en el espacio de usuario

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Leer desde espacio de usuario

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Pasos siguientes

Adobe Experience Platform Data Science Workspace proporciona un ejemplo de fórmula que utiliza los ejemplos de código anteriores para leer y escribir datos. Si desea obtener más información sobre cómo usar Python para acceder a sus datos, consulte el [Repositorio de GitHub de Python de Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
