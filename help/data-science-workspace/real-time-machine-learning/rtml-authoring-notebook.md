---
keywords: Experience Platform;guía para desarrolladores;Data Science Workspace;temas populares;aprendizaje automático en tiempo real;referencia de nodo;
solution: Experience Platform
title: Administrar portátiles de aprendizaje automático en tiempo real
description: La siguiente guía describe los pasos necesarios para crear una aplicación de aprendizaje automático en tiempo real en Adobe Experience Platform JupyterLab.
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 0%

---

# Administración de portátiles de aprendizaje automático en tiempo real (Alpha)

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real aún no está disponible para todos los usuarios. Esta función está en formato alfa y aún se está probando. Este documento está sujeto a cambios.

La siguiente guía describe los pasos necesarios para crear una aplicación de aprendizaje automático en tiempo real. Utilizando el Adobe proporcionado **[!UICONTROL ML]** en tiempo real de la plantilla de bloc de notas de Python, esta guía cubre la formación de un modelo, la creación de un DSL, la publicación de un DSL en Edge y la puntuación de la solicitud. A medida que avanza en la implementación del modelo de aprendizaje automático en tiempo real, se espera que modifique la plantilla para adaptarla a las necesidades de su conjunto de datos.

## Crear un bloc de notas de aprendizaje automático en tiempo real

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Notebooks]** en **Ciencia de datos**. A continuación, seleccione **[!UICONTROL JupyterLab]** y dedique un poco de tiempo para que se cargue el entorno.

![abrir JupyterLab](../images/rtml/open-jupyterlab.png)

Aparecerá el lanzador [!DNL JupyterLab]. Desplácese hacia abajo hasta *Aprendizaje automático en tiempo real* y seleccione el bloc de notas **[!UICONTROL ML]** en tiempo real. Se abre una plantilla que contiene celdas de bloc de notas de ejemplo con un conjunto de datos de ejemplo.

![python en blanco](../images/rtml/authoring-notebook.png)

## Importación y detección de nodos

Comience importando todos los paquetes necesarios para su modelo. Asegúrese de que se importa cualquier paquete que planee utilizar para la creación de nodos.

>[!NOTE]
>
>La lista de importaciones puede diferir según el modelo que desee realizar. Esta lista cambiará a medida que se añadan nuevos nodos con el paso del tiempo. Consulte la [guía de referencia de nodos](./node-reference.md) para obtener una lista completa de los nodos disponibles.

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

Con una de las siguientes opciones, va a escribir código [!DNL Python] para leer, preprocesar y analizar datos. A continuación, debe entrenar su propio modelo ML, serializarlo en formato ONNX y luego cargarlo en la tienda del modelo de aprendizaje automático en tiempo real.

- [Formación de su propio modelo en portátiles JupyterLab](#training-your-own-model)
- [Carga de su propio modelo ONNX preentrenado en los portátiles JupyterLab](#pre-trained-model-upload)

### Formación de su propio modelo {#training-your-own-model}

Comience cargando los datos de formación.

>[!NOTE]
>
>En la plantilla **ML** en tiempo real, el [conjunto de datos CSV del seguro del coche](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) se ha tomado de [!DNL Github].

![Cargar datos de formación](../images/rtml/load_training.png)

Si desea utilizar un conjunto de datos desde dentro de Adobe Experience Platform, quite la marca de comentario de la celda de abajo. Siguiente, debe reemplazarlo `DATASET_ID` por el valor apropiado.

![conjunto de datos RTML](../images/rtml/rtml-dataset.png)

Para acceder a un conjunto de datos del [!DNL JupyterLab] bloc de notas, seleccione el **&#x200B;**&#x200B;pestaña datos del navegación izquierdo de [!DNL JupyterLab]. Aparecen los directorios **[!UICONTROL Datasets]** y **[!UICONTROL Schemas]**. Seleccione **[!UICONTROL Conjuntos de datos]**, haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Explorar datos en el bloc de notas]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en la parte inferior del bloc de notas. Esta celda contiene su `dataset_id`.

![acceso al conjunto de datos](../images/rtml/access-dataset.png)

Una vez finalizado, haga clic con el botón secundario y elimine la celda que generó en la parte inferior del bloc de notas.

### Propiedades de formación

Utilizando la plantilla proporcionada, modifique cualquiera de las propiedades de formación dentro de `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Preparar el modelo

Con la plantilla **[!UICONTROL ML]** en tiempo real, debe analizar, preprocesar, entrenar y evaluar su modelo ML. Para ello, aplique transformaciones de datos y cree una canalización de formación.

**Transformaciones de datos**

La celda **[!UICONTROL Real-time ML]** templates **Data Transformations** debe modificarse para que funcione con su propio conjunto de datos. Normalmente, esto implica cambiar el nombre de las columnas, el resumen de datos y la preparación de datos/ingeniería de funciones.

>[!NOTE]
>
>El siguiente ejemplo se condensó con fines de legibilidad usando `[ ... ]`. Vea y expanda la sección *Transformaciones de datos de plantillas en tiempo real de ML* para la celda de código completa.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid': 'ecid',
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

df1['city'] = df1.groupby('country')['city'].transform(lambda x: x.fillna(x.mode()))
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

Ejecute la celda proporcionada para ver un resultado de ejemplo. La tabla de salida devuelta por el `carinsurancedataset.csv` conjunto de datos devuelve las modificaciones definidas.

![Ejemplo de transformaciones de datos](../images/rtml/table-return.png)

**Flujo de capacitación**

Siguiente debe crear la canalización de aprendizaje. Se verá como cualquier otro archivo de canalización de aprendizaje, excepto que debe convertir y generar un archivo ONNX.

Mediante las transformaciones de datos definidas en la celda anterior, modifique el plantilla. El siguiente código resaltado a continuación se utiliza para generar un archivo ONNX en la canalización de funciones. Vea la *plantilla ML* en tiempo real para la celda completa del código de canalización.

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

Una vez que haya completado una ejecución de formación correcta, debe generar un modelo de ONNX y cargar el modelo entrenado en la tienda del modelo de aprendizaje automático en tiempo real. Después de ejecutar las celdas siguientes, el modelo ONNX aparece en el carril izquierdo junto con todos los demás portátiles.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>Cambie el valor de cadena `model_path` (`model.onnx`) para cambiar el nombre de su modelo.

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
 
print("Model ID: ", model_id)
```

![Modelo ONNX](../images/rtml/onnx-model-rail.png)

### Carga de su propio modelo ONNX preentrenado {#pre-trained-model-upload}

Con el botón de carga ubicado en [!DNL JupyterLab] blocs de notas, cargue su modelo ONNX entrenado previamente en el entorno de [!DNL Data Science Workspace] blocs de notas.

![icono de carga](../images/rtml/upload.png)

A continuación, cambie el valor de la cadena `model_path` en el bloc de notas *ML* en tiempo real para que coincida con el nombre de su modelo ONNX. Una vez finalizado, ejecute la celda *Establecer ruta de acceso del modelo* y, a continuación, ejecute la celda *Cargar el modelo al almacén de modelos RTML*. La ubicación y el ID del modelo se devuelven en la respuesta cuando se realiza correctamente.

![cargando propio modelo](../images/rtml/upload-own-model.png)

## Creación de idioma específico del dominio (DSL)

Esta sección describe la creación de un DSL. Va a crear los nodos que incluyan cualquier preprocesamiento de datos junto con el nodo ONNX. A continuación, se crea un gráfico DSL con nodos y bordes. Los extremos conectan nodos mediante un formato basado en tuplas (node_1, node_2). El gráfico no debe tener ciclos.

>[!IMPORTANT]
>
>El uso del nodo ONNX es obligatorio. Sin el nodo ONNX, la aplicación no tendrá éxito.

### Creación de nodos

>[!NOTE]
>
> Es probable que tenga varios nodos según el tipo de datos que utilice. El siguiente ejemplo describe solo un nodo único en la plantilla *ML* en tiempo real. Consulte la sección *Creación de nodos* de las plantillas *ML* en tiempo real de la celda de código completa.

El nodo Pandas siguiente utiliza `"import": "map"` para importar el nombre del método como una cadena en los parámetros, seguido de la introducción de los parámetros como una función de asignación. El ejemplo siguiente hace esto usando `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. Una vez preparada la asignación, tiene la opción de establecer `inplace` como `True` o `False`. Establezca `inplace` como `True` o `False` en función de si desea aplicar la transformación local o no. De forma predeterminada `"inplace": False` crea una nueva columna. Se ha configurado la compatibilidad para proporcionar un nuevo nombre de columna para que se añada en una versión posterior. La última línea `cols` puede ser un solo nombre de columna o una lista de columnas. Especifique las columnas en las que desea aplicar la transformación. En este ejemplo se especifica `leasing`. Para obtener más información sobre los nodos disponibles y cómo utilizarlos, visite la [guía de referencia de nodos](./node-reference.md).

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

### Creación del gráfico DSL

Con los nodos creados, el siguiente paso es encadenar los nodos para crear un gráfico.

Comience enumerando todos los nodos que forman parte del gráfico creando una matriz.

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

A continuación, conecte los nodos con los bordes. Cada tupla es una conexión [!DNL Edge].

>[!TIP]
>
> Como los nodos dependen linealmente entre sí (cada nodo depende de la salida del nodo anterior), puede crear vínculos mediante una comprensión simple de la lista de Python. Agregue sus propias conexiones si un nodo depende de varias entradas.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Una vez que los nodos estén conectados, cree el gráfico. La celda siguiente es obligatoria y no se puede editar ni eliminar.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Una vez finalizado, se devuelve un objeto `edge` que contiene cada uno de los nodos y los parámetros asignados a ellos.

![retorno de borde](../images/rtml/edge-return.png)

## Publish a Edge (Hub)

>[!NOTE]
>
>El aprendizaje automático en tiempo real se implementa y administra temporalmente en el Adobe Experience Platform Hub. Para obtener más información, visita la sección de descripción general de [la arquitectura](./home.md#architecture) del aprendizaje automático en tiempo real.

Ahora que ha creado un gráfico DSL, puede implementar el [!DNL Edge]gráfico al archivo .

>[!IMPORTANT]
>
>No publicar a [!DNL Edge] menudo, esto puede sobrecargar los [!DNL Edge] nodos. No se recomienda Publicación el mismo modelo varias veces.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### Actualización de DSL y republicación en Edge (opcional)

Si no necesitas actualizar tu DSL, puedes saltar a [puntuación](#scoring).

>[!NOTE]
>
>Las siguientes celdas solo son necesarias si desea actualizar una DSL existente que se haya publicado en Edge.

Es probable que sus modelos sigan desarrollándose. En lugar de crear un servicio completamente nuevo, es posible actualizar un servicio existente con el nuevo modelo. Puede definir un nodo que desee actualizar, asignarle un nuevo ID y, a continuación, volver a cargar el nuevo DSL en [!DNL Edge].

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

Después de actualizar el ID del nodo, puede volver a publicar un DSL actualizado en Edge.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

Se le devolverá el DSL actualizado.

![DSL actualizado](../images/rtml/updated-dsl.png)

## Puntuación {#scoring}

Después de publicar en [!DNL Edge], la puntuación se realiza mediante una solicitud de POST de un cliente. Normalmente, esto se puede hacer desde una aplicación cliente que necesita puntuaciones ML. También puede hacerlo desde Postman. El **[!UICONTROL plantilla de ML]** en tiempo real utiliza EdgeUtils para demostrar este proceso.

>[!NOTE]
>
>Se requiere un pequeño tiempo de procesamiento antes de que comience la puntuación.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Si se utiliza la misma esquema que se utilizó en aprendizaje, se generan datos de puntuación de muestra. Estos datos se utilizan para versión un marco de datos de puntuación y luego se convierten en un diccionario de puntuación. vista la plantilla de ML ** en tiempo real para la celda de código completa.

![Datos de puntuación](../images/rtml/generate-score-data.png)

### Puntuación frente al extremo de Edge

Utilice la siguiente celda dentro de la plantilla *ML* en tiempo real para puntuar en el servicio [!DNL Edge].

![Puntuación frente a edge](../images/rtml/scoring-edge.png)

Una vez completada la puntuación, se devuelve la dirección URL [!DNL Edge], la carga útil y el resultado obtenido de [!DNL Edge].

## Enumere las aplicaciones implementadas a partir de [!DNL Edge]

Para generar un lista de las aplicaciones implementadas actualmente en el [!DNL Edge], ejecute la siguiente celda de código. Esta celda no se puede editar ni eliminar.

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

## Eliminar una aplicación implementada o ID de servicio de [!DNL Edge] (opcional)

>[!CAUTION]
>
>Esta celda se utiliza para eliminar la aplicación de Edge implementada. No utilice la celda siguiente a menos que necesite eliminar una aplicación [!DNL Edge] implementada.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Pasos siguientes

Al seguir el tutorial anterior, ha entrenado y cargado correctamente un modelo de ONNX en la tienda del modelo de aprendizaje automático en tiempo real. Además, ha puntuado e implementado su modelo de aprendizaje automático en tiempo real. Si desea obtener más información sobre los nodos disponibles para la creación de modelos, visite la [guía de referencia de nodos](./node-reference.md).
