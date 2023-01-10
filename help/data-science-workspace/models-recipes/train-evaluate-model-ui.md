---
keywords: Experience Platform;entrenar y evaluar;Data Science Workspace;temas populares;crear un modelo;crear una ejecución de formación
solution: Experience Platform
title: Capacitar y evaluar un modelo en la interfaz de usuario de Data Science Workspace
type: Tutorial
description: En Adobe Experience Platform Data Science Workspace, se crea un modelo de aprendizaje automático mediante la incorporación de una fórmula existente que es adecuada para la intención del modelo. A continuación, el Modelo es entrenado y evaluado para optimizar su eficacia y eficiencia operativa mediante el ajuste de sus hiperparámetros asociados. Las fórmulas son reutilizables, lo que significa que se pueden crear varios modelos y adaptarlos a propósitos específicos con una sola fórmula.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---

# Capacite y evalúe un modelo en la interfaz de usuario de Data Science Workspace

En Adobe Experience Platform Data Science Workspace, se crea un modelo de aprendizaje automático mediante la incorporación de una fórmula existente que es adecuada para la intención del modelo. A continuación, el Modelo es entrenado y evaluado para optimizar su eficacia y eficiencia operativa mediante el ajuste de sus hiperparámetros asociados. Las fórmulas son reutilizables, lo que significa que se pueden crear varios modelos y adaptarlos a propósitos específicos con una sola fórmula.

Este tutorial recorre los pasos para crear, entrenar y evaluar un modelo.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere una fórmula existente. Si no tiene una fórmula, siga la [Importar una fórmula empaquetada en la interfaz de usuario](./import-packaged-recipe-ui.md) antes de continuar.

## Crear un modelo

En el Experience Platform, seleccione la opción **[!UICONTROL Modelos]** situado en la parte izquierda de la navegación, seleccione la pestaña examinar para ver los modelos existentes. Select **[!UICONTROL Crear modelo]** cerca de la parte superior derecha de la página para iniciar un proceso de creación de Modelo.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Busque la lista de fórmulas existentes, busque y seleccione la fórmula que desea utilizar para crear el modelo y seleccione **[!UICONTROL Siguiente]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Seleccione un conjunto de datos de entrada adecuado y seleccione **[!UICONTROL Siguiente]**. Esto establecerá el conjunto de datos de capacitación de entrada predeterminado para el modelo.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Proporcione un nombre para el Modelo y revise las configuraciones predeterminadas del Modelo. Las configuraciones predeterminadas se aplicaron durante la creación de Recipe, revisan y modifican los valores de configuración haciendo doble clic en los valores.

Para proporcionar un nuevo conjunto de configuraciones, seleccione **[!UICONTROL Cargar nueva configuración]** y arrastre un archivo JSON que contenga configuraciones de modelo a la ventana del explorador. Select **[!UICONTROL Finalizar]** para crear el modelo.

>[!NOTE]
>
>Las configuraciones son únicas y específicas de su fórmula deseada, lo que significa que las configuraciones de la fórmula de ventas minoristas no funcionarán para la fórmula de Recommendations de producto. Consulte la [referencia](#reference) para obtener una lista de las configuraciones de fórmula de venta minorista.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Creación de una ejecución de formación

En el Experience Platform, seleccione la opción **[!UICONTROL Modelos]** situado en la parte izquierda de la navegación, seleccione la pestaña examinar para ver los modelos existentes. Busque y seleccione el hipervínculo adjunto al nombre del Modelo que desea entrenar.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Se muestran todas las ejecuciones de formación existentes con sus estados de formación actuales. Para modelos creados con el [!DNL Data Science Workspace] interfaz de usuario, se genera y ejecuta automáticamente una ejecución de formación utilizando las configuraciones predeterminadas y el conjunto de datos de capacitación de entrada.

Cree una nueva ejecución de formación seleccionando **[!UICONTROL Tren]** cerca de la parte superior derecha de la página de información general del modelo.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Seleccione el conjunto de datos de entrada de formación para la ejecución de formación y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Las configuraciones predeterminadas proporcionadas durante la creación del Modelo se muestran, cambian y modifican en consecuencia haciendo doble clic en los valores. Select **[!UICONTROL Finalizar]** para crear y ejecutar la ejecución de formación.

>[!NOTE]
>
>Las configuraciones son únicas y específicas de su fórmula deseada, lo que significa que las configuraciones de la fórmula de ventas minoristas no funcionarán para la fórmula de Recommendations de producto. Consulte la [referencia](#reference) para obtener una lista de las configuraciones de fórmula de venta minorista.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Evaluar el modelo

En el Experience Platform, seleccione la opción **[!UICONTROL Modelos]** situado en la parte izquierda de la navegación, seleccione la pestaña examinar para ver los modelos existentes. Busque y seleccione el hipervínculo adjunto al nombre del Modelo que desea evaluar.

![modelo select](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Se muestran todas las ejecuciones de formación existentes con sus estados de formación actuales. Con varias ejecuciones de formación completadas, las métricas de evaluación se pueden comparar en diferentes ejecuciones de formación en el gráfico de evaluación del modelo. Seleccione una métrica de evaluación mediante la lista desplegable situada encima del gráfico.

La métrica Error de porcentaje absoluto medio (MAPE, Mean Absolute Percent Error) expresa la precisión como un porcentaje del error. Se utiliza para identificar el experimento de mayor rendimiento. Cuanto más bajo sea el MAPE, mejor.

![descripción general de las ejecuciones de formación](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

La métrica &quot;Precisión&quot; describe el porcentaje de instancias relevantes comparado con el total *recuperado* Instancias. La precisión puede verse como la probabilidad de que un resultado seleccionado aleatoriamente sea correcto.

![ejecución de varias ejecuciones](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Al seleccionar una ejecución de formación específica, se proporcionan los detalles de dicha ejecución abriendo la página de evaluación. Esto se puede hacer incluso antes de que se haya completado la ejecución. En la página de evaluación, puede ver otras métricas de evaluación, parámetros de configuración y visualizaciones específicos de la ejecución de formación.

![registros de vista previa](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

También puede descargar registros de actividad para ver los detalles de la ejecución. Los registros son especialmente útiles para las ejecuciones fallidas para ver qué ha fallado.

![registros de actividades](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Los hiperparámetros no se pueden entrenar y un modelo debe optimizarse probando diferentes combinaciones de hiperparámetros. Repita este proceso de formación y evaluación del modelo hasta que haya llegado a un Modelo optimizado.

## Pasos siguientes

Este tutorial le guió por la creación, formación y evaluación de un modelo en [!DNL Data Science Workspace]. Una vez que haya llegado a un Modelo optimizado, puede utilizar el Modelo entrenado para generar perspectivas siguiendo el [Puntuación de un modelo en la interfaz de usuario](./score-model-ui.md) tutorial.

## Referencia {#reference}

### Configuraciones de fórmula de venta minorista

Los hiperparámetros determinan el comportamiento de formación del modelo, la modificación de los hiperparámetros afectará la precisión y precisión del modelo:

| Hiperparámetro | Descripción | Intervalo recomendado |
| --- | --- | --- |
| learning_rate | La tasa de aprendizaje reduce la contribución de cada árbol mediante learning_rate. Hay un equilibrio entre learning_rate y n_estimators. | 0.1 |
| n_estimators | Número de etapas de ampliación que se van a realizar. El aumento de degradado es bastante robusto para sobreajustar, por lo que un gran número suele dar como resultado un mejor rendimiento. | 100 |
| max_depth | Profundidad máxima de los estimadores de regresión individuales. La profundidad máxima limita el número de nodos en el árbol. Ajuste este parámetro para obtener el mejor rendimiento; el mejor valor depende de la interacción de las variables de entrada. | 3 |

Los parámetros adicionales determinan las propiedades técnicas del modelo:

| Clave de parámetro | Tipo | Descripción |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Cadena | Lista de los atributos de esquema de entrada separados por comas. |
| `ACP_DSW_TARGET_FEATURES` | Cadena | Lista de los atributos de esquema de salida separados por comas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina si las funciones de entrada y salida se pueden modificar |
| `tenantId` | Cadena | Este ID garantiza que los recursos que cree tengan un espacio de nombres adecuado y estén contenidos dentro de su organización de IMS. [Siga estos pasos aquí](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar su ID de inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Cadena | El esquema de entrada utilizado para entrenar un modelo. |
| `evaluation.labelColumn` | Cadena | Etiqueta de columna para visualizaciones de evaluación. |
| `evaluation.metrics` | Cadena | Lista separada por comas de las métricas de evaluación que se utilizarán para evaluar un modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Cadena | El esquema de salida utilizado para puntuación de un modelo. |
