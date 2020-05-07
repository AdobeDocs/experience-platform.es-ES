---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Formación de un modelo de aprendizaje automático en tiempo real
topic: Training a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 0%

---


# Formación de un modelo de aprendizaje automático en tiempo real

>[!IMPORTANT]
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

Este documento proporciona un tutorial para cargar un modelo ONNX en la tienda modelo de aprendizaje automático en tiempo real.

Mediante una de las siguientes opciones, se va a escribir código de pitón para leer, preprocesar y analizar datos. A continuación, debe formar su propio modelo ML, serializarlo en formato ONNX y, finalmente, cargarlo en la tienda modelo de aprendizaje automático en tiempo real. Además, al final del tutorial, se le proporcionará un ID de modelo que identifica el modelo entrenado para utilizarlo en el tutorial [de](./scoring-ml-model.md)puntuación.

* [Formación de un modelo mediante un bloc de notas Python](#training-model-python-notebook)
* [Capacitación de un modelo con su propio modelo ONNX](#train-using-own-onnx-model)
* [Formación de un modelo mediante la plantilla del generador de fórmulas](#train-using-recipe-builder)
* [Formación de un modelo mediante el flujo de trabajo de fórmula de Data Science Workplace](#recipe-workflow-train-model)


## Formación de un modelo mediante un bloc de notas Python {#training-model-python-notebook}

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Equipos portátiles]** en *Data Science*. A continuación, seleccione **[!UICONTROL JupyterLab]** y espere un poco de tiempo para que se cargue el entorno.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Inicio seleccionando el portátil Python 3 **en blanco** desde el iniciador de JupyterLab.

![python en blanco](../images/rtml/python-blank.png)

### Acceso a los datos {#access-data}

A continuación, seleccione el conjunto de datos que desee utilizar. Para acceder a un conjunto de datos de su bloc de notas de JupyterLab, seleccione la ficha **Datos** en la navegación izquierda de JupyterLab. Aparecerán los directorios *Datasets* y *Esquemas* . Seleccione **[!UICONTROL Conjuntos]** de datos y haga clic con el botón derecho y, a continuación, seleccione la opción **[!UICONTROL Explorar datos en el bloc de notas]** en el menú desplegable del conjunto de datos que desee utilizar. Aparece una entrada de código ejecutable en el bloc de notas.

![acceso al conjunto de datos](../images/rtml/access-dataset.png)

### Preparación del modelo

Utilice la siguiente plantilla para analizar, preprocesar, entrenar y evaluar su modelo ML. Para ver un ejemplo completo, utilice las capturas de pantalla que se proporcionan debajo de esta plantilla:

```python
from sklearn import svm, metrics
from sklearn.model_selection import train_test_split


data = df[input_columns]
target = df[target_column]
# Create a classifier: a support vector classifier
classifier = svm.SVC(gamma=0.001)

# Split data into train and test subsets
X_train, X_test, y_train, y_test = train_test_split(
    data, target, test_size=0.5, shuffle=False)

# We train the classifier
classifier.fit(X_train, y_train)

# Now do predictions
predicted = classifier.predict(X_test)


print("Classification report for classifier %s:\n%s\n"
      % (classifier, metrics.classification_report(y_test, predicted)))
disp = metrics.plot_confusion_matrix(classifier, X_test, y_test)
disp.figure_.suptitle("Confusion Matrix")
print("Confusion matrix:\n%s" % disp.confusion_matrix)
```

>[!NOTE]
>El ejemplo siguiente utiliza la biblioteca scikit-learn en lugar de cargar los datos de un conjunto de datos de la plataforma Adobe Experience Platform ingerida.

![ejemplo de instalación de scikit](../images/rtml/install-scikit.png)![Training](../images/rtml/train-example.png)

**Salida**

![salida para scikit](../images/rtml/train-example-response.png)

### Cargar el modelo

Una vez completado el paso anterior, debe serializar el modelo en un formato ONNX y cargarlo en la tienda de aprendizaje automático en tiempo real. Esto devuelve el `model_id` utilizado en el [siguiente tutorial](#next-steps).

Utilice la siguiente plantilla para convertir a ONNX y cargar el conjunto de datos:

```python
from rtml_nodelibs.nodes.standard.ml.artifact_utils
import ModelUpload
from rtml_nodelibs.core.nodefactory
import NodeFactory as nf
from skl2onnx.common.data_types
import FloatTensorType
from skl2onnx
import convert_sklearn

########## Save sklearn model in ONNX format at model_path ##########
inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
model_onnx = convert_sklearn(classifier, 'ScikitLearnModel', inputs)

model_path = "model.onnx"
os.environ["ONNX_MODEL_PATH"] = model_path

with open(model_path, "wb") as f:
  f.write(model_onnx.SerializeToString())

  ########## Upload the model from model_path to RTML model store ##########
  model = ModelUpload(params = {
    'model_path': model_path
  })

msg_model = model.process(None, 1)

model_id = msg_model.model['model_id']

print("Model ID : ", model_id)
```

**Respuesta**

![id de modelo](../images/rtml/model-id.png)

Una vez que haya recibido el `model_id`archivo, cópielo y continúe con los [siguientes pasos](#next-steps).


## Capacitación de un modelo con su propio modelo ONNX {#train-using-own-onnx-model}

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Equipos portátiles]** en *Data Science*. A continuación, seleccione **[!UICONTROL JupyterLab]** y espere un poco de tiempo para que se cargue el entorno.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Con el botón de carga ubicado en los blocs de notas de JupyterLab, cargue el modelo ONNX en el entorno de blocs de notas de Data Science Workspace.

![icono de carga](../images/rtml/upload.png)

A continuación, cree un nuevo bloc de notas en blanco seleccionando el icono del bloc de notas en blanco en Python 3 en el iniciador de JupyterLab.

![python en blanco](../images/rtml/python-blank.png)

En el bloc de notas en blanco, copie y pegue lo siguiente:

>[!NOTE]
> Asegúrese de proporcionar el modelo `model_path` de ONNX que ha cargado.

```python
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
 
model_path = <path/to/onnx_model>
########## Upload the model from model_path to RTML model store ##########
model = ModelUpload(params={'model_path': model_path})
 
msg_model = model.process(None, 1)
 
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

Después de ejecutar la celda de arriba, `model_id` se devuelve un valor. Copie el ID de modelo que se usará en el [siguiente tutorial](#next-steps).

## Formación de un modelo mediante una plantilla de fórmula prediseñada {#train-using-recipe-builder}

En la interfaz de usuario de Adobe Experience Platform, seleccione **[!UICONTROL Equipos portátiles]** en *Data Science*. A continuación, seleccione **[!UICONTROL JupyterLab]** y espere un poco de tiempo para que se cargue el entorno.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

A continuación, siga el tutorial [crear una fórmula con blocs de notas](../jupyterlab/create-a-recipe.md) Jupyter. Una vez completado, debe modificar el archivo canalización.py para que funcione la inferenciación en tiempo real.

>[!NOTE]
>Es necesario modificar la plantilla proporcionada por el área de trabajo de ciencia de datos para que se ajuste a su conjunto de datos.

Asegúrese de guardar el modelo en formato ONNX y establezca la variable de entorno en `ONNX_MODEL_PATH`. El ejemplo siguiente muestra cómo modificar el archivo de canalización mediante la plantilla del creador de fórmulas.

```python
def train(configProperties, data):

  print("Train Start")

########## Extract fields from configProperties ##########
learning_rate = float(configProperties['learning_rate'])
n_estimators = int(configProperties['n_estimators'])
max_depth = int(configProperties['max_depth'])

########## Fit model ##########
X_train = data.drop('weeklySalesAhead', axis = 1).values
y_train = data['weeklySalesAhead'].values

seed = 1234
model = GradientBoostingRegressor(learning_rate = learning_rate,
  n_estimators = n_estimators,
  max_depth = max_depth,
  random_state = seed)

model.fit(X_train, y_train)

########## Save sklearn model in ONNX format at model_path ##########
inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
model_onnx = convert_sklearn(model, 'ScikitLearnModel', inputs)

model_path = "retail_sales_model.onnx"
os.environ["ONNX_MODEL_PATH"] = model_path

with open(model_path, "wb") as f:
  f.write(model_onnx.SerializeToString())

print("Train Complete")

return model
```

Después de modificar el archivo canalización.py, ejecute **[!UICONTROL Formación]** y **[!UICONTROL Puntuación]**. Una vez completada, seleccione el botón **[!UICONTROL Crear fórmula]** .

![botones de entrenamiento y puntuación](../images/rtml/train-score.png)

Aparece un cuadro de diálogo de nombre. Escriba el nombre de la fórmula y seleccione **[!UICONTROL Aceptar]**. Aparecerá un nuevo cuadro de diálogo para avisarle de que ha comenzado la creación de fórmulas. Deje que transcurra algún tiempo para que se cree la fórmula.

![Cuadro de diálogo Fórmula](../images/rtml/recipe-dialog.png)

![Cuadro de diálogo Fórmula](../images/rtml/recipe-dialog-confrim.png)

Una vez creada una fórmula, puede visualizarse seleccionando Fórmulas **[!UICONTROL de]** Vista en el cuadro de diálogo proporcionado o bien, accediendo a **[!UICONTROL Modelos]** y, a continuación, seleccionando **[!UICONTROL Fórmulas]** en la navegación superior izquierda. Aparece una lista de fórmulas ordenadas por fecha de creación. Confirme que la nueva fórmula está en la parte superior.

![su fórmula](../images/rtml/view-recipe.png)

Seleccione la fórmula. Aparece la página de información general de la fórmula. En la navegación superior derecha, seleccione **[!UICONTROL Crear modelo]**.

![Descripción general de la fórmula](../images/rtml/create-model.png)

A continuación, seleccione un conjunto de datos adecuado. A continuación, haga clic en **[!UICONTROL Siguiente]** en el panel de navegación superior derecho.

![seleccionar conjunto de datos](../images/rtml/select-dataset.png)

Se abre la página de configuración. Proporcione un nombre para el modelo y revise las configuraciones de modelo predeterminadas. Las configuraciones predeterminadas se aplican durante la creación de fórmulas. Revise y modifique los valores de configuración haciendo clic en los valores con el doble. Para proporcionar un nuevo conjunto de configuraciones, haga clic en **[!UICONTROL Cargar nueva configuración]** y arrastre un archivo JSON que contenga configuraciones de modelo a la ventana del explorador. Seleccione **[!UICONTROL Finalizar]** para crear el modelo.

![Configurar modelo](../images/rtml/configure-model.png)

Una vez creado el modelo, debe esperar a que se complete la ejecución de la formación. Una vez finalizada la ejecución de la formación, puede seleccionar la ejecución de la formación para vista de sus detalles.

Seleccione una ejecución de formación. Una vez seleccionado, aparece un cuadro de diálogo de propiedades a la derecha. En este cuadro de diálogo, seleccione Registros **[!UICONTROL de Actividad de]** Vista.

![Ejecuciones de formación de vista](../images/rtml/view-training.png)

Aparecerá la ventana de diálogo Registros *de Actividad de* Vista. Seleccione la URL para los registros de *servidor* para descargar los registros y ver los detalles de la ejecución.

![Registros de vista](../images/rtml/view-logs.png)

Los registros son especialmente útiles para las ejecuciones fallidas a fin de ver qué ha fallado. Pero, en este caso, está buscando el `model-id` correspondiente al modelo ONNX que ha hecho. Copie la identificación del modelo.

>[!NOTE]
>No tienes que ejecutar un trabajo de puntuación. La puntuación de borde de aprendizaje automático en tiempo real se cubre en el [siguiente paso](#next-steps).

![Buscar ID de modelo](../images/rtml/find-model-id-logs.png)

## Formación de un modelo mediante el flujo de trabajo de fórmula de Data Science Workplace {#recipe-workflow-train-model}

Este es el mejor método para utilizarlo si está familiarizado con el código de Docker, git y Python. El uso del flujo de trabajo de Área de trabajo de ciencia de datos le ofrece la mayor flexibilidad y libertad para crear sus fórmulas. Puede extraer una imagen de acoplador base y crear su propio entorno de acoplador, depurar la fórmula con más facilidad, clonar las fórmulas prediseñadas para jugar con cualquier servicio de Área de trabajo de ciencias de datos, programar las ejecuciones de la fórmula y mucho más.

### Crear un esquema

El primer paso requiere que tenga un esquema de datos para el conjunto de datos. Se puede crear un esquema mediante la interfaz de usuario de la plataforma de experiencia de Adobe o API de plataforma.

>[!NOTE]
>Si ya tiene los datos que desea utilizar en la plataforma de Adobe Experience, vaya a [crear una fórmula](#create-a-python-recipe)Python.

* [Creación de un esquema mediante el tutorial de la interfaz de usuario del editor de esquema](../../xdm/tutorials/create-schema-ui.md)
* [Creación de un esquema mediante el tutorial de la API del editor de esquema](../../xdm/tutorials/create-schema-api.md)

### Ingestar los datos

A continuación, debe ingestar los datos con el esquema que acaba de crear. Esto se puede hacer mediante la API o la interfaz de usuario de la plataforma.

>[!NOTE]
>Si ya tiene los datos que desea utilizar en la plataforma de Adobe Experience, vaya a [crear una fórmula](#create-a-python-recipe)Python.

* [Introducción de datos en el tutorial de la interfaz de usuario de Adobe Experience Platform](../../ingestion/tutorials/ingest-batch-data.md)
* [Introducción de datos en el tutorial de la API de Adobe Experience Platform](../../ingestion/batch-ingestion/api-overview.md)

### Crear una fórmula Python {#create-a-python-recipe}

inicios de creación de fórmulas con empaquetado de archivos de origen para crear un archivo de archivo. Los archivos de origen definen la lógica de aprendizaje automático y los algoritmos utilizados para resolver un problema específico que se encuentra a la mano. Utilice el siguiente tutorial para crear una imagen Python Docker.

* [Empaquetar archivos de origen en una fórmula](../models-recipes/package-source-files-recipe.md)

Para completar el siguiente paso, debe tener una imagen de Docker en un Registro de Contenedor de Azure junto con la URL de imagen correspondiente. Seleccione uno de los vínculos de tutorial siguientes para terminar de crear una fórmula Python:

* [Importación de una fórmula empaquetada en la interfaz de usuario](../models-recipes/import-packaged-recipe-ui.md)
* [Importar una fórmula empaquetada mediante la API](../models-recipes/import-packaged-recipe-api.md)

### Crear una ejecución de formación

En Adobe Experience Platform Data Science Workspace, se crea un modelo de aprendizaje automático mediante la incorporación de una fórmula existente que es adecuada para la intención del modelo. A continuación, se capacita y evalúa al Modelo para optimizar su eficacia y eficiencia operativa mediante el ajuste de sus hiperparámetros asociados.

* [Formación y evaluación de un modelo en la interfaz de usuario](../models-recipes/train-evaluate-model-ui.md)
* [Formación y evaluación de un modelo en la API](../models-recipes/train-evaluate-model-api.md)

>[!IMPORTANT]
>En el archivo stream.py de la fórmula, guarde el modelo en formato ONNX dentro `model_path` y defina la variable de entorno en `ONNX_MODEL_PATH`. El motor de ejecución busca esta variable de entorno específica.

```python
def train(configProperties, data):
 
    print("Train Start")
 
    ########## Extract fields from configProperties ##########

    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])
 
 
    
    ########## Fit model ##########
    
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values
 
    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)
 
    model.fit(X_train, y_train)
     
    ########## Save sklearn model in ONNX format at model_path ##########
    inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
    model_onnx = convert_sklearn(model, 'ScikitLearnModel', inputs)
 
    model_path = "retail_sales_model.onnx"
    os.environ["ONNX_MODEL_PATH"] = model_path
 
    with open(model_path, "wb") as f:
        f.write(model_onnx.SerializeToString())
 
    print("Train Complete")
 
    return model
```

Una vez creado el modelo, debe esperar a que se complete la ejecución de la formación. Una vez finalizada la ejecución de la formación, puede seleccionar la ejecución de la formación para vista de sus detalles. Seleccione una ejecución de formación. Una vez seleccionado, aparece un cuadro de diálogo de propiedades a la derecha, seleccione Registros **[!UICONTROL de Actividad de]** Vista.

![Ejecuciones de formación de vista](../images/rtml/view-training.png)

Aparecerá la ventana de diálogo Registros *de Actividad de* Vista. Seleccione la URL para los registros de *servidor* para descargar los registros y ver los detalles de la ejecución.

![Registros de vista](../images/rtml/view-logs.png)

Los registros son especialmente útiles para las ejecuciones fallidas a fin de ver qué ha fallado. Pero, en este caso, está buscando el `model-id` correspondiente al modelo ONNX que ha hecho. Copie la identificación del modelo.

![Buscar ID de modelo](../images/rtml/find-model-id-logs.png)

No es necesario ejecutar un trabajo de puntuación en la fórmula. La puntuación de borde de aprendizaje automático en tiempo real se describe en el [siguiente tutorial](#next-steps).

## Pasos siguientes {#next-steps}

Siguiendo uno de los tutoriales anteriores, ha entrenado y cargado correctamente un modelo ONNX en la tienda modelo de aprendizaje automático en tiempo real y dispone de un `model_id` modelo que identifica su modelo. Continúe con el siguiente tutorial para aprender a [valorar el modelo](./scoring-ml-model.md)de aprendizaje automático en tiempo real.