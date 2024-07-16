---
keywords: Experience Platform;entrenar y evaluar;Workspace de ciencia de datos;temas populares;crear un modelo;crear una ejecución de formación
solution: Experience Platform
title: Entrenar y evaluar un modelo en la IU de Workspace de ciencia de datos
type: Tutorial
description: En Adobe Experience Platform Data Science Workspace, se crea un modelo de aprendizaje automático incorporando una fórmula existente que es adecuada para la intención del modelo. A continuación, se entrena y evalúa el Modelo para optimizar su eficiencia operativa y eficacia mediante el ajuste de sus Hiperparámetros asociados. Las fórmulas son reutilizables, lo que significa que se pueden crear varios modelos y adaptarlos a propósitos específicos con una sola fórmula.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 1%

---

# Entrenar y evaluar un modelo en la interfaz de usuario de Data Science Workspace

En Adobe Experience Platform Data Science Workspace, se crea un modelo de aprendizaje automático incorporando una fórmula existente que es adecuada para la intención del modelo. A continuación, se entrena y evalúa el Modelo para optimizar su eficiencia operativa y eficacia mediante el ajuste de sus Hiperparámetros asociados. Las fórmulas son reutilizables, lo que significa que se pueden crear varios modelos y adaptarlos a propósitos específicos con una sola fórmula.

Este tutorial explica los pasos para crear, entrenar y evaluar un modelo.

## Introducción

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

Este tutorial requiere una fórmula existente. Si no tiene una fórmula, siga el tutorial [Importar una fórmula empaquetada en la interfaz de usuario](./import-packaged-recipe-ui.md) antes de continuar.

## Crear un modelo

En Experience Platform, seleccione la pestaña **[!UICONTROL Modelos]** ubicada en el panel de navegación izquierdo y, a continuación, seleccione la pestaña Examinar para ver los modelos existentes. Seleccione **[!UICONTROL Crear modelo]** cerca de la parte superior derecha de la página para iniciar el proceso de creación de un modelo.

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

Se muestran todas las ejecuciones de formación existentes con sus estados de formación actuales. Para los modelos creados con la interfaz de usuario [!DNL Data Science Workspace], se genera y ejecuta automáticamente una ejecución de formación utilizando las configuraciones predeterminadas y el conjunto de datos de formación de entrada.

Cree una nueva ejecución de formación seleccionando **[!UICONTROL Entrenar]** cerca de la parte superior derecha de la página Información general del modelo.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Seleccione el conjunto de datos de entrada de formación para la ejecución de formación y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Se mostrarán las configuraciones predeterminadas proporcionadas durante la creación del modelo. Para cambiarlas y modificarlas en consecuencia, haga doble clic en los valores. Seleccione **[!UICONTROL Finalizar]** para crear y ejecutar la ejecución de formación.

>[!NOTE]
>
>Las configuraciones son únicas y específicas de la fórmula deseada, lo que significa que las configuraciones de la fórmula de ventas minoristas no funcionarán para la fórmula de Recommendations del producto. Consulte la sección [reference](#reference) para obtener una lista de las configuraciones de la fórmula de ventas minoristas.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Evaluación del modelo

En Experience Platform, seleccione la pestaña **[!UICONTROL Modelos]** ubicada en el panel de navegación izquierdo y, a continuación, seleccione la pestaña Examinar para ver los modelos existentes. Busque y seleccione el hipervínculo adjunto al nombre del modelo que desea evaluar.

![seleccionar modelo](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Se muestran todas las ejecuciones de formación existentes con sus estados de formación actuales. Con varias ejecuciones de formación completadas, las métricas de evaluación se pueden comparar en distintas ejecuciones de formación en el gráfico de evaluación Modelo. Seleccione una métrica de evaluación mediante la lista desplegable situada encima del gráfico.

La métrica Porcentaje de error absoluto medio (MAPE) expresa la precisión como un porcentaje del error. Se utiliza para identificar el experimento de mayor rendimiento. Cuanto más bajo sea el MAPE, mejor.

![descripción general de las ejecuciones de formación](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

La métrica &quot;Precisión&quot; describe el porcentaje de instancias relevantes en comparación con el total de *instancias recuperadas*. La precisión se puede ver como la probabilidad de que un resultado seleccionado aleatoriamente sea correcto.

![ejecutando varias ejecuciones](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Al seleccionar una ejecución de formación específica, se proporcionan los detalles de dicha ejecución abriendo la página de evaluación. Esto se puede hacer incluso antes de que se haya completado la ejecución. En la página de evaluación, puede ver otras métricas de evaluación, parámetros de configuración y visualizaciones específicos de la ejecución de la formación.

![registros de vista previa](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

También puede descargar registros de actividad para ver los detalles de la ejecución. Los registros son especialmente útiles para las ejecuciones fallidas para ver qué ha fallado.

![registros de actividad](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Los hiperparámetros no se pueden entrenar y un modelo debe optimizarse probando diferentes combinaciones de hiperparámetros. Repita este proceso de formación y evaluación del modelo hasta que haya llegado a un modelo optimizado.

## Pasos siguientes

Este tutorial lo guió en la creación, formación y evaluación de un modelo en [!DNL Data Science Workspace]. Una vez que haya llegado a un modelo optimizado, puede usar el modelo entrenado para generar perspectivas siguiendo el tutorial [Puntuar un modelo en la interfaz de usuario](./score-model-ui.md).

## Referencia {#reference}

### Configuraciones de fórmula de ventas minoristas

Los hiperparámetros determinan el comportamiento de entrenamiento del Modelo, la modificación de los hiperparámetros afectará la precisión y precisión del Modelo:

| Hiperparámetro | Descripción | Intervalo recomendado |
| --- | --- | --- |
| learning_rate | La tasa de aprendizaje reduce la contribución de cada árbol según learning_rate. Hay un equilibrio entre learning_rate y n_estimators. | 0,1 |
| n_estimadores | Número de etapas de ampliación que se van a realizar. El aumento de degradado es bastante robusto para un ajuste excesivo, por lo que un gran número suele resultar en un mejor rendimiento. | 100 |
| max_depth | Profundidad máxima de los estimadores de regresión individuales. La profundidad máxima limita el número de nodos en el árbol. Ajuste este parámetro para obtener el mejor rendimiento; el mejor valor depende de la interacción de las variables de entrada. | 3 |

Los parámetros adicionales determinan las propiedades técnicas del modelo:

| Clave de parámetro | Tipo | Descripción |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Cadena | Lista de atributos de esquema de entrada separados por comas. |
| `ACP_DSW_TARGET_FEATURES` | Cadena | Lista de atributos de esquema de salida separados por comas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina si se pueden modificar las características de entrada y salida |
| `tenantId` | Cadena | Este ID garantiza que los recursos que cree tengan un espacio de nombres correcto y estén contenidos en la organización. [Siga los pasos aquí](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar su ID de inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Cadena | El esquema de entrada utilizado para entrenar un modelo. |
| `evaluation.labelColumn` | Cadena | Etiqueta de columna para visualizaciones de evaluación. |
| `evaluation.metrics` | Cadena | Lista separada por comas de las métricas de evaluación que se utilizarán para evaluar un modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Cadena | Esquema de salida utilizado para puntuar un modelo. |
