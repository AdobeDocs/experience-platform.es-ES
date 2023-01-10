---
keywords: Experience Platform;inicio;temas populares;acceso a datos;python sdk;api de acceso a datos;leer python;escribir python
solution: Experience Platform
title: Acceso a datos mediante Python en Data Science Workspace
type: Tutorial
description: El siguiente documento contiene ejemplos sobre cómo acceder a los datos en Python para utilizarlos en Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Acceso a datos mediante Python en Data Science Workspace

El siguiente documento contiene ejemplos sobre cómo acceder a datos mediante Python para su uso en Data Science Workspace. Para obtener información sobre el acceso a los datos mediante los blocs de notas de JupyterLab, visite [Acceso a los datos de los portátiles JupyterLab](../jupyterlab/access-notebook-data.md) documentación.

## Leer un conjunto de datos

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

La cláusula DISTINCT permite recuperar todos los valores distintos a nivel de fila/columna, eliminando todos los valores duplicados de la respuesta.

Un ejemplo de uso de la variable `distinct()` a continuación:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### cláusula WHERE

Puede utilizar ciertos operadores en Python para ayudar a filtrar el conjunto de datos.

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

A continuación se puede ver un ejemplo del uso de estas funciones de filtrado:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### Cláusula ORDER BY

La cláusula ORDER BY permite ordenar los resultados recibidos por una columna especificada en un orden específico (ascendente o descendente). Esto se hace usando la variable `sort()` función.

Un ejemplo de uso de la variable `sort()` a continuación:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula LIMIT

La cláusula LIMIT permite limitar el número de registros recibidos del conjunto de datos.

Un ejemplo de uso de la variable `limit()` a continuación:

```python
df = dataset_reader.limit(100).read()
```

### Cláusula OFFSET

La cláusula OFFSET permite omitir filas, desde el principio, para empezar a devolver filas desde un punto posterior. En combinación con LIMIT, esto puede utilizarse para iterar filas en bloques.

Un ejemplo de uso de la variable `offset()` a continuación:

```python
df = dataset_reader.offset(100).read()
```

## Escritura de un conjunto de datos

Para escribir en un conjunto de datos, debe proporcionar el dataframe pandas a su conjunto de datos.

### Escribiendo el dataframe de pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Directorio de espacio de usuario (señalando)

Para trabajos de ejecución más largos, es posible que deba almacenar pasos intermedios. En casos como este, puede leer y escribir en un espacio de usuario.

>[!NOTE]
>
>Las rutas a los datos son **not** almacenado. Debe almacenar la ruta correspondiente a sus datos respectivos.

### Escribir en userspace

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

Adobe Experience Platform Data Science Workspace proporciona un ejemplo de fórmula que utiliza los ejemplos de código anteriores para leer y escribir datos. Si desea obtener más información sobre cómo utilizar Python para acceder a sus datos, consulte la [Repositorio Python GitHub de Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
