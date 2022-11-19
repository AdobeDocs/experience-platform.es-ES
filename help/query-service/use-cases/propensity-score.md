---
title: Determinar Una Puntuación De Propensión Mediante Un Modelo Predictivo Generado Por El Aprendizaje Automático
description: Aprenda a utilizar el servicio de consulta para aplicar su modelo predictivo a los datos de Platform. Este documento muestra cómo utilizar los datos de Platform para predecir la propensión de un cliente a realizar compras en cada visita.
source-git-commit: af1c8f94d1758b3a4e7ea00c46b0f9a71a01c6be
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Determinar una puntuación de tendencia utilizando un modelo predictivo generado por el aprendizaje automático

Con el servicio de consulta, puede aprovechar los datos de Experience Platform en las plataformas de aprendizaje automático para generar modelos predictivos, como puntuaciones de tendencia. En esta guía se explica cómo utilizar Query Service para enviar datos a su plataforma de aprendizaje automático con el fin de formar un modelo en un bloc de notas computacional. El modelo entrenado se puede aplicar a los datos mediante SQL para predecir la propensión de compra de un cliente en cada visita.

## Primeros pasos

Como parte de este proceso requiere que imparta un modelo de aprendizaje automático, este documento asume un conocimiento práctico de uno o más entornos de aprendizaje automático.

Este ejemplo utiliza [!DNL Jupyter Notebook] como entorno de desarrollo. Aunque hay muchas opciones disponibles, [!DNL Jupyter Notebook] se recomienda porque es una aplicación web de código abierto que tiene bajos requisitos de cálculo. Puede [descargado del sitio oficial](https://jupyter.org/).

Si aún no lo ha hecho, siga los pasos para [connect [!DNL Jupyter Notebook] con el servicio de consulta de Adobe Experience Platform](../clients/jupyter-notebook.md) antes de continuar con esta guía.

Las bibliotecas utilizadas en este ejemplo incluyen:

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## Importar tablas de análisis de Platform a [!DNL Jupyter Notebook] {#import-analytics-tables}

Para generar un modelo de puntuación de tendencia, se debe importar una proyección de los datos de análisis almacenados en Platform en [!DNL Jupyter Notebook]. Desde un [!DNL Python] 3 [!DNL Jupyter Notebook] conectado a Query Service, los siguientes comandos importan un conjunto de datos de comportamiento del cliente de Luma, un almacén de ropa ficticia. Como los datos de Platform se almacenan con el formato Experience Data Model (XDM) , se debe generar un objeto JSON de muestra que se ajuste a la estructura del esquema. Consulte la documentación para obtener instrucciones sobre cómo [generar el objeto JSON de muestra](../../xdm/ui/sample.md).

![La variable [!DNL Jupyter Notebook] tablero con varios comandos resaltados.](../images/use-cases/jupyter-commands.png)

El resultado muestra una vista tabularizada de todas las columnas del conjunto de datos de comportamiento de Luma dentro del [!DNL Jupyter Notebook] tablero.

![El resultado tabularizado del conjunto de datos de comportamiento del cliente importado de Luma dentro de [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Preparar los datos para el aprendizaje automático {#prepare-data-for-machine-learning}

Se debe identificar una columna objetivo para entrenar un modelo de aprendizaje automático. Como la propensión a comprar es el objetivo para este caso de uso, la variable `analytic_action` se elige como columna de destino en los resultados de Luma. El valor `productPurchase` es el indicador de una compra de cliente. La variable `purchase_value` y `purchase_num` también se eliminan, ya que están directamente relacionadas con la acción de compra del producto.

Los comandos para realizar estas acciones son los siguientes:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

A continuación, los datos del conjunto de datos de Luma deben transformarse en representaciones adecuadas. Se requieren dos pasos:

1. Transforme las columnas que representan números en columnas numéricas. Para ello, convierta explícitamente el tipo de datos en la variable `dataframe`.
1. Transforme también columnas categóricas en columnas numéricas.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Una técnica denominada *una codificación activa* se utiliza para convertir las variables de datos categóricas para su uso con algoritmos de aprendizaje profundo y automático. Esto a su vez mejora las predicciones así como la precisión de clasificación de un modelo. Utilice la variable `Sklearn` biblioteca para representar cada valor categórico en una columna independiente.

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

Los datos definidos como `X` está tabularizado y aparece como se muestra a continuación:

![La salida tabularizada de X dentro de [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Ahora que los datos necesarios para el aprendizaje automático están disponibles, pueden ajustarse a los modelos de aprendizaje automático preconfigurados [!DNL Python]&#39;s `sklearn` biblioteca. [!DNL Logistics Regression] se utiliza para entrenar el modelo de propensión y permite ver la precisión de los datos de prueba. En este caso, es de aproximadamente el 85%.

La variable [!DNL Logistic Regression] el algoritmo y el método de división de prueba de tren, utilizado para calcular el rendimiento de los algoritmos de aprendizaje automático, se importan en el bloque de código siguiente:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

La precisión de los datos de prueba es 0,8518518518518519.

A través del uso de la Regresión Logística, puede visualizar las razones de una compra y ordenar las características que determinan la propensión por su importancia clasificada en pedidos descendentes. Las primeras columnas indican una causa mayor que conduce al comportamiento de compra. Estas últimas columnas indican factores que no conducen al comportamiento de compra.

El código para visualizar los resultados como dos gráficos de barras es el siguiente:

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

A continuación se muestra una visualización de gráficos de barras verticales de los resultados:

![La visualización de las 10 principales funciones que definen una tendencia a comprar o no.](../images/use-cases/visualized-results.png)

Se pueden discernir varios patrones en el gráfico de barras. Los temas Punto de venta (POS) y Llamada del canal como reembolso son los factores más importantes que deciden un comportamiento de compra. Mientras que los temas de llamada como quejas y facturas son funciones importantes para definir el comportamiento de no compra. Se trata de perspectivas cuantificables y procesables que los especialistas en marketing pueden aprovechar para llevar a cabo campañas de marketing destinadas a abordar la tendencia a la compra de estos clientes.

## Utilice el servicio de consulta para aplicar el modelo entrenado {#use-query-service-to-apply-trained-model}

Una vez creado el modelo entrenado, debe aplicarse a los datos que se mantienen en el Experience Platform. Para ello, la lógica de la canalización de aprendizaje automático debe convertirse a SQL. Los dos componentes clave de esta transición son los siguientes:

- En primer lugar, SQL debe reemplazar a la variable [!DNL Logistics Regression] para obtener la probabilidad de una etiqueta de predicción. El modelo creado por la Regresión Logística produjo el modelo de regresión `y = wX + c`  donde pesos `w` e intercepción `c` son la salida del modelo. Las funciones SQL se pueden usar para multiplicar los pesos y obtener una probabilidad.

- En segundo lugar, el proceso de ingeniería alcanzado en [!DNL Python] con una codificación activa también debe incorporarse a SQL. Por ejemplo, en la base de datos original, tenemos `geo_county` para almacenar el municipio, pero la columna se convierte a `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. La siguiente instrucción SQL realiza la misma transformación, donde `w1`, `w2`y `w3` puede sustituirse por los pesos aprendidos del modelo en [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Para las funciones numéricas, puede multiplicar directamente las columnas con los pesos, como se ve en la instrucción SQL a continuación.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Una vez obtenidos los números, se pueden portar a una función sigmoid donde el algoritmo de regresión logística produce las predicciones finales. En la siguiente declaración, `intercept` es el número de la intersección en la regresión.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### Un ejemplo completo

En una situación en la que tiene dos columnas (`c1` y `c2`), si `c1` tiene dos categorías, la variable [!DNL Logistic Regression] está entrenado con la siguiente función:
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
El equivalente en SQL es el siguiente:

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
La variable [!DNL Python] el código para automatizar el proceso de traducción es el siguiente:

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

Cuando se utiliza SQL para deducir la base de datos, el resultado es el siguiente:

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

Los resultados tabularizados muestran la tendencia a comprar para cada sesión de cliente con `0` lo que significa que no hay inclinación a comprar y `1` lo que significa una tendencia confirmada a comprar.

![Los resultados tabularizados de la inferencia de la base de datos utilizando SQL.](../images/use-cases/inference-results.png)

## Uso de datos de muestra: Agrupamiento {#working-on-sampled-data}

En el caso de que los tamaños de datos sean demasiado grandes para que el equipo local almacene los datos para la formación de modelos, puede tomar muestras en lugar de los datos completos del servicio de consulta. Para saber cuántos datos se necesitan para realizar muestras desde el servicio de consulta, puede aplicar una técnica llamada bootstrapping. A este respecto, el arrancamiento significa que el modelo se entrena varias veces con varias muestras y se inspecciona la varianza de las precisiones del modelo entre las distintas muestras. Para ajustar el ejemplo del modelo de propensión dado arriba, primero, encapsula todo el flujo de trabajo de aprendizaje automático en una función . El código es el siguiente:

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

Esta función se puede ejecutar varias veces en un bucle, por ejemplo, 10 veces. La diferencia con respecto al código anterior es que ahora el ejemplo no se toma de toda la tabla, sino solo una muestra de filas. Por ejemplo, el código de muestra siguiente solo toma 1000 filas. Se pueden almacenar las precisiones de cada iteración.

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

A continuación, se ordenan las precisiones del modelo arrancado. Después de lo cual, las cantidades 10 y 90 de las precisiones del modelo se convierten en un intervalo de confianza del 95% para las precisiones del modelo con el tamaño de muestra dado.

![El comando print para mostrar el intervalo de confianza de la puntuación de tendencia.](../images/use-cases/confidence-interval.png)

La figura anterior indica que si solo toma 1000 filas para entrenar sus modelos, puede esperar que las precisiones caigan entre aproximadamente el 84% y el 88%. Puede ajustar el `LIMIT` en las consultas del servicio de consulta basadas en sus necesidades para garantizar el rendimiento de los modelos.


