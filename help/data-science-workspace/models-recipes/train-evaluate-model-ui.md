---
keywords: Experience Platform;entrenar y evaluar;Workspace de ciencia de datos;temas populares;crear un modelo;crear una ejecución de formación
solution: Experience Platform
title: Entrenar y evaluar un modelo en la IU de Workspace de ciencia de datos
type: Tutorial
description: En Adobe Experience Platform Data Science Workspace, se crea un modelo de aprendizaje automático incorporando una fórmula existente que es adecuada para la intención del modelo. A continuación, se entrena y evalúa el Modelo para optimizar su eficiencia operativa y eficacia mediante el ajuste de sus Hiperparámetros asociados. Las fórmulas son reutilizables, lo que significa que se pueden crear varios modelos y adaptarlos a propósitos específicos con una sola fórmula.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# Entrenar y evaluar un modelo en la interfaz de usuario de Data Science Workspace

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

En Adobe Experience Platform Espacio de trabajo de ciencia de datos, se crea un modelo de aprendizaje automático mediante la incorporación de una fórmula existente que es adecuada para la intención del modelo. Luego, el modelo se entrena y evalúa para optimizar su eficiencia y eficacia operativa mediante el ajuste de sus hiperparámetros asociados. Las recetas son reutilizables, lo que significa que se pueden crear múltiples modelos y adaptarlos a propósitos específicos con una sola receta.

Este tutorial guía a través de los pasos para crear, entrenar y evaluar un modelo.

## Introducción

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

Este tutorial requiere una fórmula existente. Si no tiene una fórmula, seguir la [Importar una receta empaquetada en el tutorial de IU](./import-packaged-recipe-ui.md) antes de continuar.

## Crear un modelo

En Experience Platform, seleccione el **[!UICONTROL pestaña de modelos]** ubicado en el navegación izquierdo y, a continuación, seleccione el pestaña de exploración para vista los modelos existentes. Seleccione **[!UICONTROL Crear modelo]** cerca de la parte superior derecha de la página para iniciar el proceso de creación de un modelo.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Examine la lista de fórmulas existentes, busque y seleccione la fórmula que se utilizará para crear el modelo y seleccione **[!UICONTROL Siguiente]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Seleccione un conjunto de datos de entrada adecuado y seleccione **[!UICONTROL Siguiente]**. Esto establecerá el conjunto de datos de aprendizaje de entrada predeterminado para el modelo.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Proporcione un nombre para el modelo y revise las configuraciones del modelo predeterminado. Las configuraciones predeterminadas se aplicaron durante la creación de la fórmula, revise y modifique los valores de configuración haciendo doble clic en los valores.

Para proporcionar un nuevo conjunto de configuraciones, seleccione **[!UICONTROL Cargar nueva configuración]** y arrastre un archivo JSON que contenga configuraciones de modelo a la ventana del explorador. Seleccione **[!UICONTROL Finalizar]** para crear el modelo.

>[!NOTE]
>
>Las configuraciones son únicas y específicas de la fórmula deseada, lo que significa que las configuraciones de la fórmula de ventas minoristas no funcionarán para la fórmula de Recommendations del producto. Consulte la sección [reference](#reference) para obtener una lista de las configuraciones de la fórmula de ventas minoristas.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Crear una ejecución de formación

En Experience Platform, seleccione la pestaña **[!UICONTROL Modelos]** ubicada en el panel de navegación izquierdo y, a continuación, seleccione la pestaña Examinar para ver los modelos existentes. Busque y seleccione el hipervínculo adjunto al nombre del modelo que desea entrenar.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Se muestran todas las ejecuciones de formación existentes con sus estados de formación actuales. Para los modelos creados con la interfaz usuario [!DNL Data Science Workspace] , se genera y ejecuta automáticamente una ejecución aprendizaje utilizando las configuraciones predeterminadas y los aprendizaje conjunto de datos de entrada.

Crear una nueva aprendizaje ejecutar seleccionando **[!UICONTROL Tren]** cerca de la parte superior derecha del Página de descripción general del modelo.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Seleccione el conjunto de datos de entrada de aprendizaje para la ejecución aprendizaje y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Las configuraciones predeterminadas proporcionadas durante la creación del modelo se muestran, cambian y modifican en consecuencia haciendo clic en los valores doble. Seleccione **[!UICONTROL Finalizar]** para crear y ejecutar la ejecución aprendizaje.

>[!NOTE]
>
>Las configuraciones son únicas y específicas de la fórmula prevista, lo que significa que las configuraciones de la fórmula de ventas minoristas no funcionarán para el producto Recommendations la fórmula. Consulte la sección de [referencia](#reference) para obtener una lista de las configuraciones de las fórmulas de ventas minoristas.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Evaluación del modelo

En Experience Platform, seleccione la pestaña **[!UICONTROL Modelos]** ubicada en el panel de navegación izquierdo y, a continuación, seleccione la pestaña Examinar para ver los modelos existentes. Busque y seleccione el hipervínculo adjunto al nombre del modelo que desea evaluar.

![Seleccionar modelo](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Se enumeran todas las ejecuciones de aprendizaje existentes con sus estados aprendizaje actuales. Con varias ejecuciones de aprendizaje completadas, las métricas de evaluación se pueden comparar en diferentes ejecuciones de aprendizaje en el gráfico de evaluación del modelo. Seleccione un Métrica de evaluación mediante el menú desplegable lista situado encima del gráfico.

La métrica Porcentaje de error absoluto medio (MAPE) expresa la precisión como un porcentaje del error. Se utiliza para identificar el experimento de mayor rendimiento. Cuanto más bajo sea el MAPE, mejor.

![descripción general de las ejecuciones de formación](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

La métrica &quot;Precisión&quot; describe el porcentaje de instancias relevantes en comparación con el total de *instancias recuperadas*. La precisión se puede ver como la probabilidad de que un resultado seleccionado aleatoriamente sea correcto.

![ejecutando varias ejecuciones](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Al seleccionar una ejecución de aprendizaje específica se proporcionan los detalles de esa ejecución al abrir el Página de evaluación. Esto se puede hacer incluso antes de que se haya completado la ejecución. En la página de evaluación, puede ver otras métricas de evaluación, parámetros de configuración y visualizaciones específicos de la ejecución de la formación.

![registros de vista previa](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

También puede descargar registros de actividad para ver los detalles de la ejecución. Los registros son especialmente útiles para las ejecuciones fallidas para ver qué ha fallado.

![registros de actividad](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Los hiperparámetros no se pueden entrenar y un modelo debe optimizarse probando diferentes combinaciones de hiperparámetros. Repita este aprendizaje de modelo y este proceso de evaluación hasta que haya llegado a un modelo optimizado.

## Pasos siguientes

Este tutorial guiarle a través de la creación, aprendizaje y evaluación de un modelo en [!DNL Data Science Workspace]. Una vez que haya llegado a un modelo optimizado, puede usar el modelo entrenado para generar información siguiendo el [modelo de puntuación de un IU](./score-model-ui.md) tutorial.

## Referencia {#reference}

### Configuraciones de fórmula de ventas minoristas

Los hiperparámetros determinan el comportamiento de entrenamiento del Modelo, la modificación de los hiperparámetros afectará la precisión y precisión del Modelo:

| Hiperparámetro | Descripción | Intervalo recomendado |
| --- | --- | --- |
| learning_rate | La tasa de aprendizaje reduce la contribución de cada árbol en un learning_rate. Hay un equilibrio entre learning_rate y n_estimators. | 0,1 |
| n_estimadores | Número de etapas de ampliación que se van a realizar. El aumento de degradado es bastante robusto para un ajuste excesivo, por lo que un gran número suele resultar en un mejor rendimiento. | 100 |
| max_depth | Profundidad máxima de los estimadores de regresión individual. La profundidad máxima limita el número de nodos del árbol. Ajuste este parámetro para obtener el mejor rendimiento; El mejor valor depende de la interacción de las variables de entrada. | 3 |

Parámetros adicionales determinan las propiedades técnicas del modelo:

| Clave de parámetro | Tipo | Descripción |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Cadena | Lista de atributos de esquema de entrada separados por comas. |
| `ACP_DSW_TARGET_FEATURES` | Cadena | Lista de atributos de esquema de salida separados por comas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina si se pueden modificar las características de entrada y salida |
| `tenantId` | Cadena | Este ID garantiza que los recursos que cree tengan un espacio de nombres correcto y estén contenidos en la organización. [Siga los pasos que se indican a continuación](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar su ID de inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Cadena | El esquema de entrada utilizado para entrenar un modelo. |
| `evaluation.labelColumn` | Cadena | Etiqueta de columna para visualizaciones de evaluación. |
| `evaluation.metrics` | Cadena | lista separadas por comas de métricas de evaluación que se utilizarán para evaluar un modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Cadena | El resultado esquema utilizado para puntuar un modelo. |
