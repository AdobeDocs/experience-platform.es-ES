---
keywords: Experience Platform;guía para desarrolladores;Data Science Workspace;temas populares;aprendizaje automático en tiempo real;referencia de nodo;
solution: Experience Platform
title: Referencia de nodo de aprendizaje automático en tiempo real
description: Un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar utilizando vínculos para formar un gráfico que represente una canalización ML. La tarea realizada por un nodo representa una operación en los datos de entrada, como una transformación de datos o esquema, o una inferencia de aprendizaje automático. El nodo envía el valor transformado o inferido a los nodos siguientes.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# Referencia de nodo de aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real aún no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

Un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar utilizando vínculos para formar un gráfico que represente una canalización ML. La tarea realizada por un nodo representa una operación en los datos de entrada, como una transformación de datos o esquema, o una inferencia de aprendizaje automático. El nodo envía el valor transformado o inferido a los nodos siguientes.

La siguiente guía describe las bibliotecas de nodos compatibles con el aprendizaje automático en tiempo real.

## Descubrimiento de nodos para su uso en la canalización ML

Copie el siguiente código en un [!DNL Python] bloc de notas para ver todos los nodos disponibles para usar.

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

### Carga del modelo

El nodo ModelUpload es un nodo de Adobe interno que toma una ruta de acceso del modelo y carga el modelo desde la ruta de acceso del modelo local al almacén del blob de aprendizaje automático en tiempo real.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode es un nodo de Adobe interno que toma un ID de modelo para extraer el modelo ONNX preentrenado y lo utiliza para puntuar en los datos entrantes.

>[!TIP]
>
>Especifique las columnas en el mismo orden en que desea que se puntuen los datos que se envíen al modelo ONNX.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

El siguiente nodo Pandas permite importar cualquier `pd.DataFrame` o cualquier función general de nivel superior de los paneles. Para obtener más información sobre los métodos Pandas, visite [Documentación de métodos Pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Para obtener más información sobre las funciones de nivel superior, visite [Guía de referencia de la API Pandas para funciones generales](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

El nodo siguiente utiliza `"import": "map"` para importar el nombre del método como una cadena en los parámetros, seguido de introducir los parámetros como una función de asignación. El ejemplo siguiente hace esto utilizando `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Una vez que haya colocado el mapa, tiene la opción de establecer `inplace` como `True` o `False`. Establezca `inplace` como `True` o `False` en función de si desea aplicar la transformación en su lugar o no. De forma predeterminada `"inplace": False` crea una columna nueva. La compatibilidad para proporcionar un nuevo nombre de columna se establece para añadirse en una versión posterior. La última línea `cols` puede ser un nombre de columna único o una lista de columnas. Especifique las columnas en las que desea aplicar la transformación. En este ejemplo `device` se ha especificado.

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

El nodo ScikitLearn permite importar cualquier modelo o escalador ScikitLearn ML. Utilice la siguiente tabla para obtener más información sobre cualquiera de los valores utilizados en el ejemplo:

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
| Funciones | Funciones de entrada al modelo (lista de cadenas). <br> Por ejemplo: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| etiqueta | Nombre de la columna de destino (cadena). |
| mode | Tren/prueba (cadena). |
| model_path | Ruta al modelo guardado localmente en formato onx. |
| params.model | Ruta de importación absoluta al modelo (cadena), por ejemplo: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Parámetros de modelo, consulte la [API sklearn (mapa/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) documentación para obtener más información. |
| node_instance.process(data_message_from_previous_node) | El método `process()` toma DataMsg del nodo anterior y aplica la transformación. Esto depende del nodo actual que se esté utilizando. |

### Split

Utilice el siguiente nodo para dividir su dataframe en tren y prueba pasando `train_size` o `test_size`. Esto devuelve un dataframe con un multi-índice. Puede acceder a los marcos de datos de prueba y tren utilizando el siguiente ejemplo, `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Pasos siguientes

El siguiente paso es crear nodos para utilizarlos en la puntuación de un modelo de aprendizaje automático en tiempo real. Para obtener más información, consulte la [Guía del usuario del ordenador portátil de aprendizaje automático en tiempo real](./rtml-authoring-notebook.md).
