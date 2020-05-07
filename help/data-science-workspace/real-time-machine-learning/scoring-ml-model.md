---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Puntuación de un modelo de aprendizaje automático en tiempo real
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Puntuación de un modelo de aprendizaje automático en tiempo real

>[!IMPORTANT]
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

Este tutorial le muestra cómo utilizar nodos de aprendizaje automático en tiempo real para procesar previamente los datos entrantes y puntearlos con respecto al modelo ONNX.

>[!IMPORTANT]
> - Las funciones utilizadas en los nodos no se pueden serializar. Por ejemplo, una función lambda utilizada en un nodo pandas.
> - Hay una suspensión de 60 segundos después de que la implementación de Edge se realice manualmente. Esto se puede transferir al método score_edge de EdgeUtils.


>[!NOTE]
>Para obtener una puntuación de un modelo para utilizarlo en el aprendizaje automático en tiempo real, debe haber completado el tutorial anterior sobre la [formación de un modelo para el aprendizaje automático en tiempo real](./training-ml-model.md)

## Crear un bloc de notas nuevo

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Equipos portátiles]** en *Data Science*. A continuación, seleccione **[!UICONTROL JupyterLab]** y espere un poco de tiempo para que se cargue el entorno.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Inicio seleccionando el portátil Python 3 **en blanco** desde el iniciador de JupyterLab.

![python en blanco](../images/rtml/python-blank.png)

## Importación y detección de nodos

Inicio importando todos los paquetes necesarios para el modelo. Asegúrese de importar todos los paquetes que planee utilizar para la creación de nodos.

>[!NOTE]
>La lista de las importaciones puede diferir según el modelo que haya hecho.

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

Para ver la lista de nodos disponibles, copie y pegue el siguiente ejemplo en el bloc de notas.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

La respuesta recibida es una lista de nodos.

![lista de notas](../images/rtml/node-list.png)

## Creación de nodos para la puntuación de bordes

A continuación, debe definir y crear un nodo para la puntuación de borde. Reemplace el `model_id` en el ejemplo con el ID de modelo que recibió al completar la formación en el tutorial [](./training-ml-model.md)anterior. En este ejemplo se utiliza el nodo Pandas para importar un método pd.DataDrame o una función general de nivel superior pandas. La función de mapa se importa y se utiliza para crear dos nodos. Para obtener más información sobre los nodos disponibles y cómo utilizarlos, visite la guía de referencia de [nodos](./node-reference.md).

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## Generar DSL de gráfico

Con los nodos creados, el siguiente paso es encadenar los nodos para crear un gráfico.

Inicio enumerando todos los nodos que forman parte del gráfico.

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

A continuación, conecte los nodos con los bordes. Cada tupla es una conexión de borde.

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

Una vez conectados los nodos, cree el gráfico.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## Publicar en Edge

Ahora que ha creado un gráfico, puede implementarlo en el borde.

>[!IMPORTANT]
>No publicar en Edge con frecuencia, esto puede sobrecargar los nodos Edge. No se recomienda publicar el mismo modelo varias veces.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Cliente Edge

Después de publicar en Edge, la puntuación se realiza mediante una solicitud POST de un cliente. Normalmente, esto se puede hacer desde una aplicación cliente que necesita puntuaciones ML. También puedes hacerlo desde Postman. En este caso, EdgeUtils se utiliza para mostrar el proceso.

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

Una vez finalizada la puntuación, se devuelve la URL del borde, la carga útil y la salida puntuada del borde.

![puntuación completada](../images/rtml/scoring-complete.png)

## Eliminación de una aplicación implementada desde Edge (opcional)

>!![CAUTION]
Esta celda se utiliza para eliminar la aplicación Edge implementada. No utilice la siguiente celda a menos que necesite eliminar una aplicación Edge implementada.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Pasos siguientes

Siguiendo el tutorial anterior, ha marcado e implementado correctamente su modelo de aprendizaje automático en tiempo real. Si desea obtener más información sobre los nodos disponibles para la creación de modelos, visite la guía [de referencia de](./node-reference.md)nodos.



