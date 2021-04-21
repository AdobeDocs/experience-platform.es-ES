---
keywords: Experience Platform;modelo de aprendizaje automático;Data Science Workspace;temas populares;crear y publicar un modelo
solution: Experience Platform
title: Creación y publicación de un modelo de aprendizaje automático
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace proporciona los medios para lograr su objetivo utilizando la fórmula prediseñada de Product Recommendations. Siga este tutorial para ver cómo puede acceder y comprender los datos de venta minorista, crear y optimizar un modelo de aprendizaje automático y generar perspectivas en Data Science Workspace.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 0%

---

# Creación y publicación de un modelo de aprendizaje automático

![](../images/models-recipes/model-walkthrough/objective.png)

Supongamos que es propietario de un sitio web de venta minorista en línea. Cuando los clientes compran en su sitio web de venta minorista, desea presentarles recomendaciones de productos personalizadas para exponer una variedad de otros productos que su empresa ofrece. A lo largo de la existencia de su sitio web, ha recopilado continuamente datos de clientes y desea utilizar de alguna manera estos datos para generar recomendaciones de productos personalizadas.

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] proporciona los medios para lograr su objetivo utilizando la fórmula prediseñada de  [Product Recommendations](../pre-built-recipes/product-recommendations.md). Siga este tutorial para ver cómo puede acceder y comprender los datos de venta minorista, crear y optimizar un modelo de aprendizaje automático y generar perspectivas en [!DNL Data Science Workspace].

Este tutorial refleja el flujo de trabajo de [!DNL Data Science Workspace] y abarca los siguientes pasos para crear un modelo de aprendizaje automático:

1. [Preparar los datos](#prepare-your-data)
2. [Crear el modelo](#author-your-model)
3. [Capacite y evalúe su modelo](#train-and-evaluate-your-model)
4. [Operacionalizar el modelo](#operationalize-your-model)

## Primeros pasos

Antes de iniciar este tutorial, debe tener los siguientes requisitos previos:

- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

- Recursos de habilitación. Póngase en contacto con el representante de su cuenta para que le proporcionen los siguientes artículos.
   - Fórmula de Recommendations
   - Conjunto de datos de entrada de Recommendations
   - Esquema de entrada de Recommendations
   - Conjunto de datos de salida de Recommendations
   - Esquema de salida de Recommendations
   - Conjunto de datos dorados postValues
   - Esquema de conjunto de datos dorado

- Descargue los tres archivos [!DNL Jupyter Notebook] requeridos del [Adobe public [!DNL Git] repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs), se utilizarán para mostrar el flujo de trabajo [!DNL JupyterLab] en [!DNL Data Science Workspace].

Una explicación práctica de los siguientes conceptos clave utilizados en este tutorial:
- [[!DNL Experience Data Model]](../../xdm/home.md): El esfuerzo de estandarización liderado por Adobe para definir esquemas estándar como  [!DNL Profile] y ExperienceEvent para la gestión de la experiencia del cliente.
- Conjuntos de datos: Construcción de almacenamiento y administración para datos reales. Instancia de instancia física de un [Esquema XDM](../../xdm/schema/field-dictionary.md).
- Lotes: Los conjuntos de datos están formados por lotes. Un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad.
- [!DNL JupyterLab]:  [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) es una interfaz basada en web de código abierto para Project  [!DNL Jupyter] y está estrechamente integrada en  [!DNL Experience Platform].

## Prepare sus datos {#prepare-your-data}

Para crear un modelo de aprendizaje automático que realice recomendaciones de productos personalizadas a los clientes, se deben analizar las compras anteriores de los clientes en el sitio web. En esta sección se explica cómo se incorporan estos datos en [!DNL Platform] a [!DNL Adobe Analytics] y cómo se transforman esos datos en un conjunto de datos de funciones que utilizará el modelo de aprendizaje automático.

### Explorar los datos y comprender los esquemas

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Datasets]** para enumerar todos los conjuntos de datos existentes y seleccione el conjunto de datos que desea explorar. En este caso, el conjunto de datos [!DNL Analytics] **Golden Data Set postValues**.

![](../images/models-recipes/model-walkthrough/dataset-browse.png)

Se abre la página de actividad del conjunto de datos, que enumera información relacionada con su conjunto de datos. Puede seleccionar **[!UICONTROL Preview Dataset]** cerca de la esquina superior derecha para examinar los registros de muestra. También puede ver el esquema del conjunto de datos seleccionado. Seleccione el vínculo de esquema en el carril derecho. Aparece una ventana emergente, al seleccionar el vínculo en **[!UICONTROL schema name]** se abre el esquema en una nueva pestaña.

![](../images/models-recipes/model-walkthrough/dataset-activity.png)


![](../images/models-recipes/model-walkthrough/schema-view.png)

Los demás conjuntos de datos se han rellenado previamente con lotes para obtener una vista previa. Puede ver estos conjuntos de datos repitiendo los pasos anteriores.

| Nombre del conjunto de datos | Esquema | Descripción |
| ----- | ----- | ----- |
| Conjunto de datos dorados postValues | Esquema de conjunto de datos dorado | [!DNL Analytics] datos de origen de su sitio web |
| Conjunto de datos de entrada de Recommendations | Esquema de entrada de Recommendations | Los datos [!DNL Analytics] se transforman en un conjunto de datos de capacitación mediante una canalización de funciones. Estos datos se utilizan para entrenar el modelo de aprendizaje automático de Product Recommendations. `itemid` y  `userid` corresponden a un producto comprado por ese cliente. |
| Conjunto de datos de salida de Recommendations | Esquema de salida de Recommendations | El conjunto de datos para el que se almacenan los resultados de puntuación, contendrá la lista de productos recomendados para cada cliente. |

## Cree el modelo {#author-your-model}

El segundo componente del ciclo de vida [!DNL Data Science Workspace] implica la creación de fórmulas y modelos. La fórmula de Product Recommendations está diseñada para generar recomendaciones de productos a escala mediante la utilización de datos de compras anteriores y aprendizaje automático.

Las fórmulas son la base de un modelo, ya que contienen algoritmos de aprendizaje automático y lógica diseñada para resolver problemas específicos. Lo que es más importante, las fórmulas le permiten democratizar el aprendizaje automático en su organización, lo que permite a otros usuarios acceder a un modelo para casos de uso diferentes sin necesidad de escribir ningún código.

### Explorar la fórmula de Product Recommendations

En el Experience Platform, vaya a **[!UICONTROL Models]** desde la columna de navegación izquierda y, a continuación, seleccione **[!UICONTROL Recipes]** en la barra de navegación superior para ver una lista de las fórmulas disponibles para su organización.

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

A continuación, busque y abra el **[!UICONTROL Recommendations Recipe]** proporcionado seleccionando su nombre. Aparecerá la página de información general de la fórmula.

![](../images/models-recipes/model-walkthrough/Recipe-view.png)

A continuación, en el carril derecho, seleccione **[!UICONTROL Recommendations Input Schema]** para ver el esquema que alimenta la fórmula. Los campos de esquema &quot;[!UICONTROL itemId]&quot; y &quot;[!UICONTROL userId]&quot; corresponden a un producto comprado ([!UICONTROL interactionType]) por ese cliente en un momento específico ([!UICONTROL timestamp]). Siga los mismos pasos para revisar los campos del **[!UICONTROL Recommendations Output Schema]**.

![](../images/models-recipes/model-walkthrough/input-output.png)

Ahora ha revisado los esquemas de entrada y salida requeridos por la fórmula de Product Recommendations. Continúe con la siguiente sección para aprender a crear, entrenar y evaluar un modelo de Recommendations de producto.

## Capacite y evalúe su modelo {#train-and-evaluate-your-model}

Ahora que los datos están preparados y la fórmula está lista, puede crear, entrenar y evaluar su modelo de aprendizaje automático.

### Crear un modelo

Un modelo es una instancia de una fórmula, que permite entrenar y puntuar con datos a escala.

En el Experience Platform, vaya a **[!UICONTROL Models]** desde la columna de navegación izquierda y, a continuación, seleccione **[!UICONTROL Recipes]** en la barra de navegación superior. Muestra una lista de las fórmulas disponibles para su organización. Seleccione la fórmula de recomendación de producto.

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

En la página de fórmula, seleccione **[!UICONTROL Create Model]**.

![crear modelo](../images/models-recipes/model-walkthrough/create-model-recipe.png)

El flujo de trabajo crear modelo comienza por seleccionar una fórmula. Seleccione **[!UICONTROL Recommendations Recipe]** y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha.

![](../images/models-recipes/model-walkthrough/create-model.png)

A continuación, proporcione un nombre de modelo. Las configuraciones disponibles para el modelo se enumeran que contienen configuraciones para los comportamientos de capacitación y puntuación predeterminados del modelo. Revise las configuraciones y seleccione **[!UICONTROL Finish]**.

![](../images/models-recipes/model-walkthrough/configure-model.png)

Se le redirige la página de información general de sus modelos con una nueva ejecución de formación generada. Una ejecución de formación se genera de forma predeterminada cuando se crea un modelo.

![](../images/models-recipes/model-walkthrough/model-overview.png)

Puede optar por esperar a que finalice la ejecución de formación o continuar creando una nueva ejecución de formación en la siguiente sección.

### Capacitar el modelo mediante hiperparámetros personalizados

En la página **Información general del modelo**, seleccione **[!UICONTROL Train]** cerca de la parte superior derecha para crear una nueva ejecución de formación. Seleccione el mismo conjunto de datos de entrada que utilizó al crear el modelo y seleccione **[!UICONTROL Next]**.

![](../images/models-recipes/model-walkthrough/select-train.png)

Aparece la página **[!UICONTROL Configuration]**. Aquí puede configurar el valor de las ejecuciones de formación `num_recommendations`, también conocido como hiperparámetro. Un modelo preparado y optimizado utilizará los hiperparámetros de mejor rendimiento según los resultados de la ejecución de la formación.

Los hiperparámetros no se pueden aprender, por lo que deben asignarse antes de que se ejecuten las formaciones. El ajuste de hiperparámetros puede cambiar la precisión del modelo entrenado. Dado que la optimización de un modelo es un proceso iterativo, puede ser necesario realizar múltiples ejercicios de capacitación antes de que se logre una evaluación satisfactoria.

>[!TIP]
>
>Establezca `num_recommendations` en 10.

![](../images/models-recipes/model-walkthrough/training-configuration.png)

Aparecen puntos de datos adicionales en el gráfico de evaluación del modelo. Esto puede tardar hasta varios minutos en aparecer una vez finalizada la ejecución.

![](../images/models-recipes/model-walkthrough/training-graphs.png)

### Evaluar el modelo

Cada vez que se completa una ejecución de formación, puede ver las métricas de evaluación resultantes para determinar el rendimiento del modelo.

Para revisar las métricas de evaluación (Precisión y Reclamación) para cada ejecución de capacitación completada, seleccione la ejecución de capacitación.

![](../images/models-recipes/model-walkthrough/select-training-run.png)

Puede explorar la información proporcionada para cada métrica de evaluación. Cuanto más altas sean estas métricas, mejor será el rendimiento del modelo.

![](../images/models-recipes/model-walkthrough/metrics.png)

Puede ver el conjunto de datos, el esquema y los parámetros de configuración utilizados para cada formación ejecutada en el carril correcto. Vuelva a la página Modelo e identifique la formación de mayor rendimiento ejecutada observando sus métricas de evaluación.

## Operacionalice el modelo {#operationalize-your-model}

El último paso del flujo de trabajo de ciencia de datos es poner en marcha el modelo para obtener una puntuación y consumir perspectivas del almacén de datos.

### Puntuación y generación de perspectivas

En la página de información general del modelo de recomendaciones de productos, seleccione el nombre de la ejecución de formación de mejor rendimiento, con los valores de precisión y recuperación más altos.

![puntuación de la mejor ejecución](../images/models-recipes/model-walkthrough/select-training-run.png)

A continuación, en la parte superior derecha de la página de detalles de la ejecución de la formación, seleccione **[!UICONTROL Score]**.

![seleccionar puntuación](../images/models-recipes/model-walkthrough/select-score.png)

A continuación, seleccione **[!UICONTROL Recommendations Input Dataset]** como conjunto de datos de entrada de puntuación, que es el mismo conjunto de datos que utilizó al crear el modelo y ejecutar sus ejecuciones de formación. A continuación, seleccione **[!UICONTROL Next]**.

![](../images/models-recipes/model-walkthrough/score-input.png)

Una vez que tenga el conjunto de datos de entrada, seleccione **[!UICONTROL Recommendations Output Dataset]** como conjunto de datos de salida de puntuación. Los resultados de puntuación se almacenan en este conjunto de datos como un lote.

![](../images/models-recipes/model-walkthrough/score-output.png)

Finalmente, revise las configuraciones de puntuación. Estos parámetros contienen los conjuntos de datos de entrada y salida seleccionados anteriormente, junto con los esquemas adecuados. Seleccione **[!UICONTROL Finish]** para comenzar la ejecución de la puntuación. La ejecución puede tardar varios minutos en completarse.

![](../images/models-recipes/model-walkthrough/score-finish.png)

### Ver perspectivas puntuadas

Una vez finalizada correctamente la ejecución de puntuación, puede obtener una vista previa de los resultados y ver las perspectivas generadas.

En la página ejecuciones de puntuación , seleccione la ejecución de puntuación completada y, a continuación, seleccione **[!UICONTROL Preview Scoring Results Dataset]** en el carril derecho.

![](../images/models-recipes/model-walkthrough/preview-scores.png)

En la tabla de vista previa, cada fila contiene recomendaciones de producto para un cliente en particular, etiquetadas como [!UICONTROL recommendations] y [!UICONTROL userId] respectivamente. Dado que el hiperparámetro [!UICONTROL num_recommendations] se estableció en 10 en las capturas de pantalla de muestra, cada fila de recomendaciones puede contener hasta 10 identidades de producto delimitadas por un signo de número (#).

![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## Pasos siguientes {#next-steps}

Este tutorial le introdujo en el flujo de trabajo de [!DNL Data Science Workspace], demostrando cómo los datos sin procesar se pueden convertir en información útil a través del aprendizaje automático. Para obtener más información sobre el uso de [!DNL Data Science Workspace], continúe con la siguiente guía sobre la [creación del esquema de ventas minoristas y el conjunto de datos](./create-retails-sales-dataset.md).
