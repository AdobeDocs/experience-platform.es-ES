---
keywords: Experience Platform; guía de desarrolladores; Data Science Espacio de trabajo; temas populares; Aprendizaje automático en tiempo real; nodo referencia;
solution: Experience Platform
title: Referencia del nodo de aprendizaje automático en tiempo real
description: Una nodo es la unidad fundamental a partir de la cual se forman los gráficos. Cada nodo realiza un tarea específico y se pueden encadenar mediante vínculos para formar un gráfico que represente una canalización de aprendizaje automático. El tarea realizado por un nodo representa una operación en datos de entrada, como un transformación de datos o esquema, o una inferencia de aprendizaje automático. El nodo genera el valor transformado o inferido en los nodo siguientes.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 9030a5482d4ea2b54426680cef92b89e68ef5b33
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Referencia de nodo de aprendizaje automático en tiempo real (Alpha)

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real aún no está disponible para todos los usuarios. Esta función está en formato alfa y aún se está probando. Este documento está sujeto a cambios.

Un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar mediante vínculos para formar un gráfico que represente una canalización XML. La tarea realizada por un nodo representa una operación en los datos de entrada, como una transformación de datos o esquemas o una inferencia de aprendizaje automático. El nodo genera el valor transformado o inferido en el nodo o nodos siguientes.

La siguiente guía describe las bibliotecas de nodos compatibles con el aprendizaje automático en tiempo real.

## Descubrimiento de nodos para su uso en la canalización XML

Copie el siguiente código en un bloc de notas [!DNL Python] para ver todos los nodos que están disponibles para su uso.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Respuesta de ejemplo**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Nodos estándar

Los nodos estándar se basan en bibliotecas de ciencia de datos de código abierto como Pandas y ScikitLearn.

### Carga de modelos

El nodo ModelUpload es un Adobe Systems nodo interno que toma una model_path y carga el modelo desde la ruta del modelo local hasta el tienda de blob de aprendizaje automático en tiempo real.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode es un Adobe Systems nodo interno que toma un ID de modelo para recibir el modelo ONNX previamente entrenado y lo utiliza para puntuar en los datos entrantes.

>[!TIP]
>
>Especifique las columnas en el mismo orden en el que desea que se envíen los datos al modelo ONNX para la puntuación.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

El siguiente nodo de pandas le permite importar cualquier `pd.DataFrame` método o función general de nivel superior de pandas. Para obtener más información acerca de los métodos Pandas, visita la documentación[&#128279;](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html) de los métodos Pandas. Para obtener más información sobre las funciones de nivel superior, visita la guía de referencia de [la API de Pandas para funciones](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html) generales.

El nodo siguiente se utiliza `"import": "map"` para importar el nombre del método como una cadena en los parámetros, seguido de la introducción de los parámetros como una función de asignación. El ejemplo siguiente lo hace utilizando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Una vez que tenga el mapa en su lugar, tiene la opción de establecer `inplace` como `True` o `False`. Establezca `inplace` como `True` o `False` en función de si desea aplicar transformación in situ o no. De forma predeterminada `"inplace": False` , crea una columna nueva. La compatibilidad para proporcionar un nuevo nombre de columna se añadirá en una versión posterior. La última línea `cols` puede ser un solo nombre de columna o una lista de columnas. Especifique las columnas en las que desea aplicar la transformación. En este ejemplo se especifica `device`.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

El nodo ScikitLearn le permite importar cualquier modelo o escalador ML de ScikitLearn. Utilice la tabla siguiente para obtener más información sobre cualquiera de los valores utilizados en el ejemplo:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valor | Descripción |
| --- | --- |
| características | Funciones de entrada al modelo (lista de cadenas). <br> Por ejemplo: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| etiqueta | Nombre de la columna de destino (cadena). |
| modo | Tren/prueba (cuerda). |
| model_path | Ruta al modelo de guardado localmente en onnx formato. |
| params.model | Ruta de acceso de importación absoluta al modelo (cadena), p. ej.: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Para obtener más información sobre los hiperparámetros del modelo, consulte la [documentación de la API sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html). |
| node_instance.process(data_message_from_previous_node) | El método `process()` toma DataMsg del nodo anterior y aplica la transformación. Esto depende del nodo actual que se esté utilizando. |

### División

Utilice el siguiente nodo para dividir el marco de datos en entrenamiento y prueba pasando `train_size` o `test_size`. Devuelve un marco de datos con un índice múltiple. Puede acceder a los marcos de datos de prueba y entrenamiento con el siguiente ejemplo, `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Pasos siguientes

El siguiente paso es crear nodos para utilizarlos en la puntuación de un modelo de aprendizaje automático en tiempo real. Para obtener más información, visite la [Guía del usuario del bloc de notas de Aprendizaje automático en tiempo real](./rtml-authoring-notebook.md).
