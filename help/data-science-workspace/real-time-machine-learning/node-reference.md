---
keywords: Experience Platform;guía para desarrolladores;Área de trabajo de ciencia de datos;temas populares;Aprendizaje automático en tiempo real;referencia de nodo;
solution: Experience Platform
title: Referencia de nodo de aprendizaje automático en tiempo real
topic: Nodes reference
description: Un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar mediante vínculos para formar un gráfico que represente una canalización ML. La tarea que realiza un nodo representa una operación en datos de entrada, como una transformación de datos o esquemas, o una inferencia de aprendizaje automático. El nodo envía el valor transformado o inferido a los nodos siguientes.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# Referencia de nodo de aprendizaje automático en tiempo real (Alpha)

>[!IMPORTANT]
>
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

Un nodo es la unidad fundamental de la que se forman los gráficos. Cada nodo realiza una tarea específica y se puede encadenar mediante vínculos para formar un gráfico que represente una canalización ML. La tarea que realiza un nodo representa una operación en datos de entrada, como una transformación de datos o esquemas, o una inferencia de aprendizaje automático. El nodo envía el valor transformado o inferido a los nodos siguientes.

La siguiente guía describe las bibliotecas de nodos admitidas para aprendizaje automático en tiempo real.

## Descubrimiento de nodos para su uso en la canalización ML

Copie el siguiente código en un bloc de notas [!DNL Python] para vista de todos los nodos disponibles para su uso.

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

### ModelUpload

El nodo ModelUpload es un nodo de Adobe interno que toma una ruta de modelo y carga el modelo desde la ruta de modelo local al almacén de blob de aprendizaje automático en tiempo real.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode es un nodo de Adobe interno que necesita un ID de modelo para extraer el modelo ONNX preentrenado y utilizarlo para puntear en los datos entrantes.

>[!TIP]
>
>Especifique las columnas en el mismo orden en el que desea que se envíen los datos al modelo ONNX para puntuar.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

El siguiente nodo Pandas permite importar cualquier método `pd.DataFrame` o cualquier función general de nivel superior de los paneles. Para obtener más información sobre los métodos de Pandas, visite la [documentación de métodos de Pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Para obtener más información sobre las funciones de nivel superior, visite la [guía de referencia de API de Pandas para funciones generales](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

El nodo siguiente utiliza `"import": "map"` para importar el nombre del método como una cadena en los parámetros, seguido de introducir los parámetros como una función de mapa. El ejemplo siguiente lo hace mediante `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Después de haber implementado el mapa, tiene la opción de establecer `inplace` como `True` o `False`. Establezca `inplace` como `True` o `False` en función de si desea aplicar la transformación en su lugar o no. De forma predeterminada `"inplace": False` crea una nueva columna. Se ha configurado la compatibilidad para proporcionar un nuevo nombre de columna para agregarlo en una versión posterior. La última línea `cols` puede ser un nombre de columna único o una lista de columnas. Especifique las columnas en las que desea aplicar la transformación. En este ejemplo se especifica `device`.

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

El nodo ScikitLearn permite importar cualquier modelo o escalador de ScikitLearn ML. Utilice la tabla siguiente para obtener más información sobre cualquiera de los valores utilizados en el ejemplo:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valor | Descripción |
| --- | --- |
| características | Características de entrada al modelo (lista de cadenas). <br> Por ejemplo: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nombre de columna de destinatario (cadena). |
| modo | Tren/prueba (cadena). |
| model_path | Ruta al modelo guardado localmente en formato onnx. |
| params.model | Ruta de importación absoluta al modelo (cadena), por ejemplo: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Para obtener más información, consulte la documentación de [sklearn API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) para obtener más información. |
| node_instance.process(data_message_from_previous_node) | El método `process()` toma DataMsg del nodo anterior y aplica la transformación. Esto depende del nodo actual que se esté utilizando. |

### Split

Utilice el nodo siguiente para dividir su datafame en tren y prueba pasando `train_size` o `test_size`. Esto devuelve un dataframe con un multi-índice. Puede acceder a los marcos de datos de prueba y tren mediante el siguiente ejemplo, `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Pasos siguientes

El siguiente paso es crear nodos para utilizarlos en la puntuación de un modelo de aprendizaje automático en tiempo real. Para obtener más información, visite la [guía del usuario del bloc de notas de aprendizaje automático en tiempo real](./rtml-authoring-notebook.md).
