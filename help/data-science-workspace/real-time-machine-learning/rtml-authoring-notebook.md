---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Guía del usuario del portátil de aprendizaje automático en tiempo real
topic: Training and scoring a ML model
description: La siguiente guía describe los pasos necesarios para crear una aplicación de aprendizaje automático en tiempo real en Adobe Experience Platform JupyterLab.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---


# Guía del usuario de portátiles de aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

La siguiente guía describe los pasos necesarios para crear una aplicación de aprendizaje automático en tiempo real. Con el Adobe proporcionado para la plantilla de portátil ML **[!UICONTROL Python en tiempo]** real, esta guía cubre la formación de un modelo, la creación de un DSL, la publicación de DSL en Edge y la puntuación de la solicitud. A medida que avance en la implementación del modelo de aprendizaje automático en tiempo real, se espera modificar la plantilla para adaptarla a las necesidades del conjunto de datos.

## Creación de un bloc de notas de aprendizaje automático en tiempo real

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Equipos portátiles]** dentro de **Data Science**. A continuación, seleccione **[!UICONTROL JupyterLab]** y espere un poco de tiempo para que se cargue el entorno.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Aparece el [!DNL JupyterLab] iniciador. Desplácese hacia abajo hasta Aprendizaje *automático en tiempo* real y seleccione el bloc de notas ML **[!UICONTROL en tiempo]** real. Se abre una plantilla que contiene celdas de bloc de notas de ejemplo con un conjunto de datos de ejemplo.

![python en blanco](../images/rtml/authoring-notebook.png)

## Importación y detección de nodos

Inicio importando todos los paquetes necesarios para el modelo. Asegúrese de importar cualquier paquete que tenga pensado utilizar para la creación de nodos.

>[!NOTE]
>
>Su lista de las importaciones puede diferir según el modelo que desee hacer. Esta lista cambiará a medida que se agreguen nuevos nodos con el paso del tiempo. Consulte la guía [de referencia de](./node-reference.md) nodos para obtener una lista completa de los nodos disponibles.

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

La siguiente celda de código imprime una lista de nodos disponibles.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![lista de notas](../images/rtml/node-list.png)

## Formación de un modelo de aprendizaje automático en tiempo real

Mediante una de las siguientes opciones, se va a escribir [!DNL Python] código para leer, preprocesar y analizar datos. A continuación, debe formar su propio modelo ML, serializarlo en formato ONNX y luego cargarlo en la tienda modelo de aprendizaje automático en tiempo real.

- [Formación de su propio modelo en portátiles JupyterLab](#training-your-own-model)
- [Carga de su propio modelo ONNX preentrenado en portátiles JupyterLab](#pre-trained-model-upload)

### Formación de su propio modelo {#training-your-own-model}

Inicio cargando los datos de la formación.

>[!NOTE]
>
>En la plantilla ML **en tiempo** real, el conjunto de datos [CSV de seguro de](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) automóvil se toma de [!DNL Github].

![Carga de datos de capacitación](../images/rtml/load_training.png)

Si desea utilizar un conjunto de datos desde Adobe Experience Platform, quite el comentario de la celda siguiente. A continuación, debe reemplazar `DATASET_ID` por el valor adecuado.

![conjunto de datos rtml](../images/rtml/rtml-dataset.png)

Para acceder a un conjunto de datos del [!DNL JupyterLab] bloc de notas, seleccione la ficha **Datos** en la navegación izquierda de [!DNL JupyterLab]. Aparecerán los directorios **[!UICONTROL Datasets]** y **[!UICONTROL Esquemas]** . Seleccione **[!UICONTROL Conjuntos]** de datos y haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Explorar datos en el bloc de notas]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas. Esta célula tiene tu `dataset_id`.

![acceso al conjunto de datos](../images/rtml/access-dataset.png)

Una vez completada, haga clic con el botón secundario y elimine la celda que generó en la parte inferior del bloc de notas.

### Propiedades de formación

Mediante la plantilla proporcionada, modifique cualquiera de las propiedades de formación incluidas en `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Preparación del modelo

Con la plantilla ML **[!UICONTROL en tiempo]** real, debe analizar, preprocesar, entrenar y evaluar su modelo ML. Esto se lleva a cabo mediante la aplicación de transformaciones de datos y la creación de una canalización de formación.

**Transformaciones de datos**

La celda Transformaciones **[!UICONTROL de]** datos de plantillas ML **en tiempo** real debe modificarse para que funcione con su propio conjunto de datos. Generalmente esto implica cambiar el nombre de las columnas, el resumen de datos y la preparación de datos o la ingeniería de funciones.

>[!NOTE]
>
>El siguiente ejemplo se ha resumido para fines de legibilidad mediante `[ ... ]`. Vista y expanda la sección de transformaciones de datos de plantillas ML *en tiempo* real para la celda de código completa.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid' : 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x : x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

Ejecute la celda proporcionada para ver un resultado de ejemplo. La tabla de resultados devuelta por el `carinsurancedataset.csv` conjunto de datos devuelve las modificaciones que ha definido.

![Ejemplo de transformaciones de datos](../images/rtml/table-return.png)

**Canalización de formación**

A continuación, debe crear la canalización de formación. Este aspecto será similar al de cualquier otro archivo de canalización de formación, excepto que necesita convertir y generar un archivo ONNX.

Mediante las transformaciones de datos definidas en la celda anterior, modifique la plantilla. El siguiente código resaltado se utiliza para generar un archivo ONNX en la canalización de funciones. Vista de la plantilla ML *en tiempo* real para la celda de código de canalización completa.

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

Una vez que haya completado la canalización de formación y haya modificado los datos mediante transformaciones de datos, utilice la siguiente celda para ejecutar la formación.

```python
model = train(config_properties, df_final)
```

### Generar y cargar un modelo ONNX

Una vez que haya completado una ejecución de formación exitosa, debe generar un modelo ONNX y cargar el modelo capacitado en la tienda modelo de aprendizaje automático en tiempo real. Después de ejecutar las siguientes celdas, el modelo ONNX aparece en el carril izquierdo junto con todos los demás portátiles.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>Cambie el valor de la `model_path` cadena (`model.onnx`) para cambiar el nombre del modelo.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>La siguiente celda no es editable ni eliminable y es necesaria para que funcione la aplicación de aprendizaje automático en tiempo real.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

![modelo ONNX](../images/rtml/onnx-model-rail.png)

### Carga de su propio modelo ONNX preentrenado {#pre-trained-model-upload}

Utilizando el botón de carga ubicado en [!DNL JupyterLab] los portátiles, cargue el modelo ONNX preentrenado en el entorno de [!DNL Data Science Workspace] portátiles.

![icono de carga](../images/rtml/upload.png)

A continuación, cambie el valor de la `model_path` cadena en el bloc de notas ML *en tiempo* real para que coincida con el nombre del modelo ONNX. Una vez completada, ejecute la celda de ruta *del modelo* Set y, a continuación, ejecute la *carga del modelo en la celda RTML Model Store* . La ubicación del modelo y la ID del modelo se devuelven en la respuesta cuando se realiza correctamente.

![cargar su propio modelo](../images/rtml/upload-own-model.png)

## Creación de un idioma específico del dominio (DSL)

Esta sección describe cómo crear un DSL. Va a crear los nodos que incluyen cualquier preprocesamiento de datos junto con el nodo ONNX. A continuación, se crea un gráfico DSL con nodos y bordes. Borra los nodos de conexión utilizando un formato basado en tupla (node_1, node_2). El gráfico no debería tener ciclos.

>[!IMPORTANT]
>
>El uso del nodo ONNX es obligatorio. Sin el nodo ONNX, la aplicación no tendrá éxito.

### Creación de nodos

>[!NOTE]
>
> Es probable que tenga varios nodos según el tipo de datos que se esté utilizando. En el siguiente ejemplo se describe sólo un nodo en la plantilla ML *en tiempo* real. Vista la sección Creación *de* nodos de plantillas ML *en tiempo* real para la celda de código completa.

El nodo Pandas siguiente utiliza `"import": "map"` para importar el nombre del método como una cadena en los parámetros, seguido de introducir los parámetros como una función de mapa. El ejemplo siguiente lo hace mediante `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. Después de haber colocado el mapa, tiene la opción de establecer `inplace` como `True` o `False`. Establezca `inplace` como `True` o `False` en función de si desea aplicar la transformación en su lugar o no. De forma predeterminada, `"inplace": False` crea una nueva columna. Se ha configurado la compatibilidad para proporcionar un nuevo nombre de columna para agregarlo en una versión posterior. La última línea `cols` puede ser un nombre de columna o una lista de columnas. Especifique las columnas en las que desea aplicar la transformación. En este ejemplo `leasing` se especifica. Para obtener más información sobre los nodos disponibles y cómo utilizarlos, visite la guía de referencia de [nodos](./node-reference.md).

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### Generar el gráfico DSL

Con los nodos creados, el siguiente paso es encadenar los nodos para crear un gráfico.

Inicio enumerando todos los nodos que forman parte del gráfico creando una matriz.

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

A continuación, conecte los nodos con los bordes. Cada tupla es una [!DNL Edge] conexión.

>[!TIP]
>
> Dado que los nodos dependen linealmente entre sí (cada nodo depende de la salida del nodo anterior), puede crear vínculos utilizando una simple comprensión de lista Python. Agregue sus propias conexiones si un nodo depende de varias entradas.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Una vez conectados los nodos, cree el gráfico. La celda siguiente es obligatoria y no se puede editar ni eliminar.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Una vez completado, se devuelve un `edge` objeto que contiene cada uno de los nodos y los parámetros asignados a ellos.

![retorno de borde](../images/rtml/edge-return.png)

## Publicar en Edge (Hub)

>[!NOTE]
>
>El aprendizaje automático en tiempo real se implementa y administra temporalmente en Adobe Experience Platform Hub. Para obtener más información, consulte la sección de información general sobre la arquitectura [de aprendizaje automático en tiempo](./home.md#architecture)real.

Ahora que ha creado un gráfico DSL, puede implementarlo en el [!DNL Edge].

>[!IMPORTANT]
>
>No publicar con [!DNL Edge] frecuencia, esto puede sobrecargar los [!DNL Edge] nodos. No se recomienda publicar el mismo modelo varias veces.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### Actualización del DSL y republicación en Edge (opcional)

Si no necesita actualizar su DSL, puede saltar a la [puntuación](#scoring).

>[!NOTE]
>
>Las siguientes celdas solo son necesarias si desea actualizar un DSL existente que se haya publicado en Edge.

Es probable que sus modelos sigan desarrollándose. En lugar de crear un servicio completamente nuevo, es posible actualizar un servicio existente con el nuevo modelo. Puede definir un nodo que desee actualizar, asignarle un nuevo ID y luego volver a cargar el nuevo DSL en el [!DNL Edge].

En el ejemplo siguiente, el nodo 0 se actualiza con un nuevo ID.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![Nodo actualizado](../images/rtml/updated-node.png)

Después de actualizar el ID de nodo, podrá volver a publicar un DSL actualizado en Edge.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

Se le devuelve el DSL actualizado.

![DSL actualizado](../images/rtml/updated-dsl.png)

## Puntuación {#scoring}

Después de publicar en [!DNL Edge], la puntuación se realiza mediante una solicitud de POST de un cliente. Normalmente, esto se puede hacer desde una aplicación cliente que necesita puntuaciones ML. También puedes hacerlo desde Postman. La plantilla ML **[!UICONTROL en tiempo]** real utiliza EdgeUtils para demostrar este proceso.

>[!NOTE]
>
>Se requiere un pequeño tiempo de procesamiento antes de anotar inicios.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Utilizando el mismo esquema que se utilizó en la formación, se generan datos de puntuación de muestra. Estos datos se utilizan para crear un marco de datos de puntuación y luego se convierten en un diccionario de puntuación. Vista de la plantilla ML *en tiempo* real para la celda de código completa.

![Datos de puntuación](../images/rtml/generate-score-data.png)

### Puntuación con el extremo de Edge

Utilice la siguiente celda dentro de la plantilla ML *en tiempo* real para realizar una puntuación con respecto a su [!DNL Edge] servicio.

![Puntuación con borde](../images/rtml/scoring-edge.png)

Una vez finalizada la puntuación, se devuelve la dirección URL, la carga útil y el resultado de puntuación [!DNL Edge] de la [!DNL Edge] .

## Lista de las aplicaciones implementadas desde el [!DNL Edge]

Para generar una lista de las aplicaciones implementadas actualmente en el [!DNL Edge], ejecute la siguiente celda de código. Esta celda no se puede editar ni eliminar.

```python
services = edge_utils.list_deployed_services()
print(services)
```

La respuesta devuelta es una matriz de los servicios implementados.

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## Eliminar una aplicación o un ID de servicio implementados de la [!DNL Edge] (opcional)

>[!CAUTION]
>
>Esta celda se utiliza para eliminar la aplicación Edge implementada. No utilice la siguiente celda a menos que necesite eliminar una aplicación implementada [!DNL Edge] .

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Pasos siguientes

Siguiendo el tutorial anterior, ha entrenado y cargado correctamente un modelo ONNX en la tienda modelo de aprendizaje automático en tiempo real. Además, ha marcado e implementado su modelo de aprendizaje automático en tiempo real. Si desea obtener más información sobre los nodos disponibles para la creación de modelos, visite la guía [de referencia de](./node-reference.md)nodos.