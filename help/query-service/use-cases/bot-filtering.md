---
title: Filtrado de bots en Query Service con aprendizaje automático
description: Este documento proporciona información general sobre cómo utilizar Query Service y el aprendizaje automático para determinar la actividad de bots y filtrar sus acciones a partir del tráfico de visitantes de sitios web en línea.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 5%

---

# Filtrado de bots en [!DNL Query Service] con aprendizaje automático

La actividad de bots puede afectar a las métricas de análisis y dañar la integridad de los datos. Adobe Experience Platform [!DNL Query Service] se puede utilizar para mantener la calidad de los datos mediante el proceso de filtrado de bots.

El filtrado para bots permite mantener la calidad de sus datos eliminando ampliamente la contaminación de los datos que resulta de la interacción no humana con su sitio web. Este proceso se logra mediante la combinación de consultas SQL y aprendizaje automático.

La actividad de bots se puede identificar de varias formas. El enfoque adoptado en este documento se centra en los picos de actividad, en este caso, el número de acciones realizadas por un usuario en un periodo de tiempo determinado. Inicialmente, una consulta SQL establece arbitrariamente un umbral para el número de acciones realizadas durante un periodo de tiempo para calificarse como actividad de bots. Este umbral se refina dinámicamente utilizando un modelo de aprendizaje automático para mejorar la precisión de estas relaciones.

Este documento proporciona información general y ejemplos detallados de las consultas de filtrado de bots SQL y los modelos de aprendizaje automático necesarios para configurar el proceso en su entorno.

## Primeros pasos

Como parte de este proceso requiere que imparta un modelo de aprendizaje automático, este documento asume un conocimiento práctico de uno o más entornos de aprendizaje automático.

Este ejemplo utiliza [!DNL Jupyter Notebook] como entorno de desarrollo. Aunque hay muchas opciones disponibles, [!DNL Jupyter Notebook] se recomienda porque es una aplicación web de código abierto que tiene bajos requisitos de cálculo. Puede [descargado del sitio oficial](https://jupyter.org/).

## Uso [!DNL Query Service] para definir un umbral para la actividad de bots

Los dos atributos utilizados para extraer datos para la detección de bots son:

* ID de visitante de Experience Cloud (ECID, también conocido como MCID): Proporciona un identificador universal y persistente que identifica a los visitantes en todas las soluciones de Adobe.
* Marca de tiempo: Esto proporciona la hora y la fecha en formato UTC cuando se produjo una actividad en el sitio web.

>[!NOTE]
>
>El uso de `mcid` sigue encontrándose en referencias de espacio de nombres al ID de visitante de Experience Cloud como se ve en el ejemplo siguiente.

La siguiente instrucción SQL proporciona un ejemplo inicial para identificar la actividad de bots. La instrucción supone que si un visitante hace 50 clics en un minuto, entonces el usuario es un bot.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

La expresión filtra los ECID (`mcid`) de todos los visitantes que alcanzan el umbral pero no abordan los picos de tráfico de otros intervalos.

## Mejore la detección de bots con el aprendizaje automático

La instrucción SQL inicial se puede refinar para que se convierta en una consulta de extracción de funciones para aprendizaje automático. La consulta mejorada debería producir más características para una variedad de intervalos para la formación de modelos de aprendizaje automático con gran precisión.

La sentencia de ejemplo se expande de un minuto con hasta 60 clics, para incluir períodos de cinco minutos y 30 minutos con recuentos de clics de 300 y 1800 respectivamente.

La sentencia de ejemplo recopila el número máximo de clics para cada ECID (`mcid`) durante las distintas duraciones. La sentencia inicial se ha ampliado para incluir periodos de un minuto (60 segundos), 5 minutos (300 segundos) y una hora (1800 segundos).

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

El resultado de esta expresión puede ser similar a la tabla proporcionada a continuación.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Identificar nuevos umbrales de pico mediante el aprendizaje automático

A continuación, exporte el conjunto de datos de consulta resultante al formato CSV y, a continuación, impórtelo en [!DNL Jupyter Notebook]. Desde ese entorno, puede entrenar un modelo de aprendizaje automático utilizando las bibliotecas de aprendizaje automático actuales. Consulte la guía de solución de problemas para obtener más información sobre [cómo exportar datos de [!DNL Query Service] en formato CSV](../troubleshooting-guide.md#export-csv)

Los umbrales de pico ad hoc establecidos inicialmente no están basados en datos y, por lo tanto, carecen de precisión. Los modelos de aprendizaje automático pueden utilizarse para entrenar parámetros como umbrales. Como resultado, puede aumentar la eficacia de la consulta reduciendo el número de `GROUP BY` mediante la eliminación de funciones innecesarias.

Este ejemplo utiliza la biblioteca de aprendizaje automático Scikit-Learn que se instala de forma predeterminada con [!DNL Jupyter Notebook]. La biblioteca python &quot;pandas&quot; también se importa para su uso aquí. Los siguientes comandos se introducen en [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

A continuación, debe entrenar un clasificador de árbol de decisiones en el conjunto de datos y observar la lógica resultante del modelo.

La biblioteca &quot;Matplotlib&quot; se utiliza para visualizar el clasificador del árbol de decisiones en el ejemplo siguiente.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

Los valores devueltos por [!DNL Jupyter Notebook] para este ejemplo, son los siguientes:

```text
Model Accuracy: 0.99935
```

![Salida estadística de [!DNL Jupyter Notebook] modelo de aprendizaje automático.](../images/use-cases/jupiter-notebook-output.png)

Los resultados del modelo mostrado en el ejemplo anterior son más del 99 % precisos.

Como el clasificador de árbol de decisiones se puede entrenar utilizando datos de [!DNL Query Service] en una cadencia normal que utiliza consultas programadas, puede garantizar la integridad de los datos filtrando la actividad de bots con un alto grado de precisión. Mediante el uso de los parámetros derivados del modelo de aprendizaje automático, las consultas originales se pueden actualizar con los parámetros altamente precisos creados por el modelo.

El modelo de ejemplo determinó con un alto grado de precisión que cualquier visitante con más de 130 interacciones en cinco minutos son bots. Esta información ahora se puede utilizar para restringir las consultas SQL de filtrado de bots.

## Pasos siguientes

Al leer este documento, tiene una mejor comprensión de cómo usar [!DNL Query Service] y aprendizaje automático para determinar y filtrar la actividad de bots.

Otros documentos que demuestren los beneficios de [!DNL Query Service] para la información estratégica comercial de su organización, se usa la variable [caso de uso de exploración abandonado](./abandoned-browse.md) ejemplo.
