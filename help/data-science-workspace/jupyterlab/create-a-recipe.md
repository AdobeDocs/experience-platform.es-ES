---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics;create recipe
solution: Experience Platform
title: Creación de una fórmula con blocs de notas Jupyter
topic: tutorial
type: Tutorial
description: Este tutorial irá a dos secciones principales. En primer lugar, creará un modelo de aprendizaje automático con una plantilla dentro de JupyterLab Notebook. A continuación, ejercerá el flujo de trabajo del bloc de notas a la fórmula dentro de JupyterLab para crear una fórmula dentro de Data Science Workspace.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '2335'
ht-degree: 0%

---


# Creación de una fórmula con blocs de notas Jupyter

Este tutorial irá a dos secciones principales. En primer lugar, creará un modelo de aprendizaje automático con una plantilla dentro de [!DNL JupyterLab Notebook]. A continuación, ejercerá el bloc de notas en el flujo de trabajo de fórmula dentro de [!DNL JupyterLab] para crear una fórmula dentro de [!DNL Data Science Workspace].

## Conceptos introducidos:

- **Fórmulas:** Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo AI o un conjunto de algoritmos, una lógica de procesamiento y una configuración necesarias para crear y ejecutar un modelo capacitado y, por tanto, ayuda a resolver problemas comerciales específicos.
- **Modelo:** Un modelo es una instancia de una fórmula de aprendizaje automático que se capacita mediante datos históricos y configuraciones para resolver un caso de uso comercial.
- **Formación:** La formación es el proceso de aprendizaje de patrones y perspectivas a partir de datos etiquetados.
- **Puntuación:** La puntuación es el proceso de generación de perspectivas a partir de datos mediante un modelo capacitado.

## Introducción al entorno del [!DNL JupyterLab] portátil

La creación de una fórmula desde cero se puede realizar dentro de [!DNL Data Science Workspace]. Para realizar inicios, vaya a [Adobe Experience Platform](https://platform.adobe.com) y haga clic en la ficha **[!UICONTROL Equipos portátiles]** de la izquierda. Para crear un nuevo bloc de notas, seleccione la plantilla Generador de fórmulas en el [!DNL JupyterLab Launcher].

El [!UICONTROL bloc de notas Generador] de fórmulas le permite ejecutar ejecuciones de puntuación y formación dentro del bloc de notas. Esto le ofrece la flexibilidad de realizar cambios en sus `train()` y `score()` métodos entre la ejecución de experimentos en los datos de capacitación y puntuación. Una vez que esté satisfecho con los resultados de la formación y la puntuación, puede crear una fórmula para utilizarla [!DNL Data Science Workspace] con la funcionalidad de fórmula integrada en el bloc de notas del Creador de fórmulas.

>[!NOTE]
>
>El bloc de notas del Creador de fórmulas admite trabajar con todos los formatos de archivo, pero actualmente la funcionalidad Crear fórmula solo es compatible [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder.png)

Al hacer clic en el bloc de notas del Creador de fórmulas desde el iniciador, el bloc de notas se abre en la ficha. La plantilla utilizada en el bloc de notas es la fórmula Python Retail Sales Forecasting (Previsión de ventas minoristas de Python) que también se puede encontrar en [este repositorio público](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Observará que en la barra de herramientas hay tres acciones adicionales: **[!UICONTROL Tren]**, **[!UICONTROL Puntuación]** y **[!UICONTROL Crear fórmula]**. Estos iconos solo aparecen en el [!UICONTROL bloc de notas del Generador] de fórmulas. Se hablará de más información sobre estas acciones [en la sección](#training-and-scoring) Formación y puntuación después de crear la fórmula en el bloc de notas.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Edite los archivos de fórmulas

Para realizar modificaciones en los archivos de fórmulas, vaya a la celda de Jupyter correspondiente a la ruta de archivo. Por ejemplo, si desea realizar cambios en `evaluator.py`, busque `%%writefile demo-recipe/evaluator.py`.

Inicio realizando los cambios necesarios en la celda y, cuando termine, simplemente ejecute la celda. El `%%writefile filename.py` comando escribirá el contenido de la celda en la `filename.py`. Deberá ejecutar manualmente la celda de cada archivo con cambios.

>[!NOTE]
>
>Debe ejecutar las celdas manualmente cuando corresponda.

## Introducción al bloc de notas del Creador de fórmulas

Ahora que conoce los conceptos básicos del entorno del [!DNL JupyterLab] portátil, puede empezar a mirar los archivos que conforman una fórmula del modelo de aprendizaje automático. Los archivos de los que hablaremos se muestran aquí:

- [Archivo de requisitos](#requirements-file)
- [Archivos de configuración](#configuration-files)
- [Cargador de datos de formación](#training-data-loader)
- [Cargador de datos de puntuación](#scoring-data-loader)
- [Archivo de canalización](#pipeline-file)
- [Archivo de evaluador](#evaluator-file)
- [Archivo de Data Saver](#data-saver-file)

### Archivo de requisitos {#requirements-file}

El archivo de requisitos se utiliza para declarar bibliotecas adicionales que desee utilizar en la fórmula. Puede especificar el número de versión si hay una dependencia. Para buscar bibliotecas adicionales, visite https://anaconda.org. La lista de las bibliotecas principales que ya se están utilizando incluye:

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Las bibliotecas o versiones específicas que agregue pueden ser incompatibles con las bibliotecas anteriores.

### Archivos de configuración {#configuration-files}

Los archivos de configuración `training.conf` y `scoring.conf`, se utilizan para especificar los conjuntos de datos que desea utilizar para la formación y la puntuación, así como para agregar hiperparámetros. Existen configuraciones independientes para la capacitación y la puntuación.

Los usuarios deben completar las siguientes variables antes de ejecutar la formación y la puntuación:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Para buscar el conjunto de datos y los ID de esquema, vaya a la ficha Datos de los blocs de notas de la barra de navegación izquierda (debajo del icono de carpeta).

![](../images/jupyterlab/create-recipe/datasets.png)

La misma información se puede encontrar en [Adobe Experience Platform](https://platform.adobe.com/) en las fichas **[Esquema](https://platform.adobe.com/schema)** y **[Conjuntos](https://platform.adobe.com/dataset/overview)** de datos.

De forma predeterminada, se establecen los siguientes parámetros de configuración al acceder a los datos:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Cargador de datos de formación {#training-data-loader}

El objetivo del cargador de datos de formación es crear instancias de los datos utilizados para crear el modelo de aprendizaje automático. Normalmente, hay dos tareas que el cargador de datos de formación realizará:
- Cargar datos desde [!DNL Platform]
- Preparación de datos e ingeniería de características

Las dos secciones siguientes abarcarán la carga de datos y la preparación de datos.

### Carga de datos {#loading-data}

En este paso se utiliza el dataframe [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)pandas. Los datos se pueden cargar desde archivos en [!DNL Adobe Experience Platform] el uso del [!DNL Platform] SDK (`platform_sdk`) o de fuentes externas mediante las funciones `read_csv()` o `read_json()` de pandas.

- [[!DNL Platform SDK]](#platform-sdk)
- [Fuentes externas](#external-sources)

>[!NOTE]
>
>En el bloc de notas del Creador de fórmulas, los datos se cargan mediante el cargador de `platform_sdk` datos.

### [!DNL Platform] SDK {#platform-sdk}

Para ver un tutorial detallado sobre el uso del cargador de `platform_sdk` datos, visite la guía del SDK de la [plataforma](../authoring/platform-sdk.md). Este tutorial proporciona información sobre la autenticación de compilación, la lectura básica de datos y la escritura básica de datos.

### Fuentes externas {#external-sources}

Esta sección muestra cómo importar un archivo JSON o CSV a un objeto pandas. La documentación oficial de la biblioteca de pandas puede encontrarse aquí:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

En primer lugar, aquí se muestra un ejemplo de importación de un archivo CSV. El `data` argumento es la ruta al archivo CSV. Esta variable se importó desde la `configProperties` sección [](#configuration-files)anterior.

```PYTHON
df = pd.read_csv(data)
```

También puede importar desde un archivo JSON. El `data` argumento es la ruta al archivo CSV. Esta variable se importó desde la `configProperties` sección [](#configuration-files)anterior.

```PYTHON
df = pd.read_json(data)
```

Ahora los datos están en el objeto dataframe y se pueden analizar y manipular en la [siguiente sección](#data-preparation-and-feature-engineering).

### Desde el SDK de acceso a datos (obsoleto)

>[!CAUTION]
>
> `data_access_sdk_python` ya no se recomienda, consulte [Convertir código de acceso a datos en SDK](../authoring/platform-sdk.md) de plataforma para obtener una guía sobre el uso del cargador de `platform_sdk` datos.

Los usuarios pueden cargar datos mediante el SDK de acceso a datos. La biblioteca se puede importar en la parte superior de la página incluyendo la línea:

`from data_access_sdk_python.reader import DataSetReader`

A continuación, utilizamos el `load()` método para obtener el conjunto de datos de formación del `trainingDataSetId` como se establece en el archivo de configuración (`recipe.conf`).

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>
>Como se indica en la sección [Archivo de](#configuration-files)configuración, al acceder a los datos desde [!DNL Experience Platform]:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Ahora que tiene sus datos, puede comenzar con la preparación de datos y la ingeniería de características.

### Preparación de datos e ingeniería de características {#data-preparation-and-feature-engineering}

Una vez cargados los datos, los datos se preparan y luego se dividen en los `train` y los `val` conjuntos de datos. A continuación se muestra el código de muestra:

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

En este ejemplo, se están realizando cinco tareas en el conjunto de datos original:
- agregar `week` y `year` columnas
- convertir `storeType` en una variable de indicador
- convertir `isHoliday` en una variable numérica
- compensación `weeklySales` para obtener valor de ventas futuro y pasado
- dividir datos, por fecha, en `train` y `val` conjunto de datos

En primer lugar, se crean `week` y `year` las columnas y se convierte la `date` columna original en [!DNL Python] datetime [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). Los valores de semana y año se extraen del objeto datetime.

A continuación, `storeType` se convierte en tres columnas que representan los tres tipos de tiendas diferentes (`A`, `B`y `C`). Cada uno contendrá un valor booleano para el estado que `storeType` sea true. Se quitará la `storeType` columna.

De manera similar, `weeklySales` cambia el `isHoliday` booleano a una representación numérica, uno o cero.

Estos datos se dividen entre `train` y `val` dataset.

La `load()` función debe completarse con el `train` conjunto de datos y `val` como resultado.

### Cargador de datos de puntuación {#scoring-data-loader}

El procedimiento para cargar datos para la puntuación es similar al de cargar datos de formación en la `split()` función. Utilizamos el SDK de acceso a datos para cargar datos de los `scoringDataSetId` que se encuentran en nuestro `recipe.conf` archivo.

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

Después de cargar los datos, se realiza la preparación de los datos y la ingeniería de características.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

Dado que el propósito de nuestro modelo es predecir futuras ventas semanales, deberá crear un conjunto de datos de puntuación utilizado para evaluar el rendimiento de la predicción del modelo.

Este bloc de notas del Generador de fórmulas hace esto compensando nuestras ventas semanales a partir de 7 días. Observe que hay mediciones para 45 almacenes cada semana para que pueda desplazar los `weeklySales` valores 45 conjuntos de datos hacia adelante en una nueva columna llamada `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Del mismo modo, puede crear una columna `weeklySalesLag` desplazando 45 hacia atrás. Con esto también puede calcular la diferencia en las ventas semanales y almacenarlas en la columna `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Dado que está desactivando los `weeklySales` puntos de datos 45 conjuntos de datos hacia adelante y 45 conjuntos de datos hacia atrás para crear nuevas columnas, los primeros y últimos 45 puntos de datos tendrán valores NaN. Puede eliminar estos puntos de nuestro conjunto de datos utilizando la `df.dropna()` función que elimina todas las filas que tienen valores NaN.

```PYTHON
df.dropna(0, inplace=True)
```

La `load()` función del cargador de datos de puntuación debe completarse con el conjunto de datos de puntuación como resultado.

### Archivo de canalización {#pipeline-file}

El `pipeline.py` archivo incluye lógica para la formación y la puntuación.

### Capacitación {#training}

El propósito de la formación es crear un modelo con las funciones y etiquetas de su conjunto de datos de formación.

>[!NOTE]
> 
>_Las funciones_ hacen referencia a la variable de entrada utilizada por el modelo de aprendizaje automático para predecir las _etiquetas_.

La `train()` función debe incluir el modelo de capacitación y devolver el modelo capacitado. Algunos ejemplos de distintos modelos se pueden encontrar en la documentación [de la guía de usuario](https://scikit-learn.org/stable/user_guide.html)scikit-learn.

Después de elegir el modelo de formación, ajustará el conjunto de datos de formación x e y al modelo y la función devolverá el modelo entrenado. Un ejemplo que lo muestra es el siguiente:

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

Tenga en cuenta que, según la aplicación, tendrá argumentos en su `GradientBoostingRegressor()` función. `xTrainingDataset` debe contener las características utilizadas para la formación, mientras `yTrainingDataset` que debe contener las etiquetas.

### Puntuación {#scoring}

La `score()` función debe contener el algoritmo de puntuación y devolver una medición para indicar el rendimiento del modelo. La `score()` función utiliza las etiquetas de conjunto de datos de puntuación y el modelo entrenado para generar un conjunto de funciones predichas. Estos valores predichos se comparan con las características reales del conjunto de datos de puntuación. En este ejemplo, la `score()` función utiliza el modelo entrenado para predecir las características mediante las etiquetas del conjunto de datos de puntuación. Se devuelven las características predichas.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### Archivo de evaluador {#evaluator-file}

El `evaluator.py` archivo contiene lógica sobre cómo desea evaluar la fórmula formada, así como sobre cómo deben dividirse los datos de capacitación. En el ejemplo de ventas minoristas, se incluirá la lógica para cargar y preparar los datos de capacitación. Pasaremos por las dos secciones siguientes.

### Dividir el conjunto de datos {#split-the-dataset}

La fase de preparación de datos para la capacitación requiere dividir el conjunto de datos que se utilizará para la capacitación y las pruebas. Estos datos se utilizarán implícitamente para evaluar el modelo después de que se haya formado. `val` Este proceso es independiente de la puntuación.

Esta sección mostrará la `split()` función que primero cargará datos en el bloc de notas y luego limpiará los datos eliminando columnas no relacionadas en el conjunto de datos. Desde allí, podrá realizar ingeniería de funciones, que es el proceso para crear funciones relevantes adicionales a partir de las funciones sin procesar existentes en los datos. A continuación se puede ver un ejemplo de este proceso junto con una explicación.

La `split()` función se muestra a continuación. El dataframe proporcionado en el argumento se dividirá en las variables `train` y `val` que se devolverá.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Evaluar el modelo entrenado {#evaluate-the-trained-model}

La `evaluate()` función se realiza después de que el modelo esté entrenado y devuelve una métrica para indicar el rendimiento del modelo. La `evaluate()` función utiliza las etiquetas de conjunto de datos de prueba y el modelo Capacitado para predecir un conjunto de funciones. Estos valores predichos se comparan con las características reales del conjunto de datos de prueba. Los algoritmos de puntuación comunes incluyen:
- [Error medio de porcentaje absoluto (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Error absoluto medio (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Error de raíz media cuadrada (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


La `evaluate()` función de la muestra de ventas minoristas se muestra a continuación:

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

Observe que la función devuelve un `metric` objeto que contiene una matriz de métricas de evaluación. Estas métricas se utilizarán para evaluar el rendimiento del modelo capacitado.

### Archivo de Data Saver {#data-saver-file}

El `datasaver.py` archivo contiene la `save()` función para guardar la predicción al probar la puntuación. La `save()` función tomará la predicción y, mediante [!DNL Experience Platform Catalog] API, escribirá los datos en el `scoringResultsDataSetId` especificado en el `scoring.conf` archivo.

El ejemplo utilizado en la fórmula de muestra de ventas minoristas se muestra aquí. Tenga en cuenta el uso de `DataSetWriter` la biblioteca para escribir datos en Platform:

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## Formación y puntuación {#training-and-scoring}

Cuando haya terminado de realizar cambios en el bloc de notas y quiera entrenar la fórmula, puede hacer clic en los botones asociados en la parte superior de la barra para crear una ejecución de formación en la celda. Al hacer clic en el botón, aparecerá un registro de comandos y resultados de la secuencia de comandos de formación en el bloc de notas (debajo de la `evaluator.py` celda). Conda primero instala todas las dependencias y luego se inicia la formación.

Tenga en cuenta que debe ejecutar la formación al menos una vez para poder ejecutar la puntuación. Al hacer clic en el botón **[!UICONTROL Ejecutar puntuación]** , se anotará en el modelo entrenado que se generó durante la formación. La secuencia de comandos de puntuación aparecerá en `datasaver.py`.

Para depurar, si desea ver la salida oculta, agregue `debug` al final de la celda de salida y vuelva a ejecutarla.

## Crear fórmula {#create-recipe}

Cuando haya terminado de editar la fórmula y esté satisfecho con el resultado de la prueba/puntuación, puede crear una fórmula a partir del bloc de notas pulsando **[!UICONTROL Crear fórmula]** en la navegación superior derecha.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Después de pulsar el botón, se le pedirá que introduzca un nombre de fórmula. Este nombre representa la fórmula real en la que se creó [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Una vez que presione **[!UICONTROL Aceptar]** podrá navegar a la nueva fórmula en [Adobe Experience Platform](https://platform.adobe.com/). Puede hacer clic en el botón Fórmulas **[!UICONTROL de]** Vista para llevarlo a la ficha **[!UICONTROL Fórmulas]** en Modelos **[!UICONTROL ML]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Una vez completado el proceso, la fórmula tendrá este aspecto:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - No eliminar ninguna de las celdas de archivo
> - No edite la `%%writefile` línea en la parte superior de las celdas del archivo
> - No crear fórmulas en diferentes blocs de notas al mismo tiempo


## Pasos siguientes {#next-steps}

Al completar este tutorial, ha aprendido a crear un modelo de aprendizaje automático en el bloc de notas del Creador de fórmulas. También ha aprendido a ejercitar el flujo de trabajo del bloc de notas para la fórmula dentro del bloc de notas para crear una fórmula dentro de [!DNL Data Science Workspace].

Para continuar aprendiendo a trabajar con recursos dentro de [!DNL Data Science Workspace], visite el menú desplegable [!DNL Data Science Workspace] Fórmulas y modelos.

## Recursos adicionales {#additional-resources}

El siguiente vídeo está diseñado para ayudarle a crear e implementar modelos.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


