---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics;ui;scoring run;scoring results
solution: Experience Platform
title: Puntuación de un modelo (IU)
topic: tutorial
type: Tutorial
description: 'La puntuación en Adobe Experience Platform Data Science Workspace se puede conseguir mediante la incorporación de datos de entrada a un modelo ya existente. Los resultados de puntuación se almacenan y se pueden ver en un conjunto de datos de salida especificado como un nuevo lote. '
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---


# Puntuación de un modelo (IU)

La puntuación en Adobe Experience Platform [!DNL Data Science Workspace] se puede lograr mediante la alimentación de datos de entrada en un modelo capacitado existente. Los resultados de puntuación se almacenan y se pueden ver en un conjunto de datos de salida especificado como un nuevo lote.

Este tutorial muestra los pasos necesarios para marcar un modelo en la interfaz de usuario [!DNL Data Science Workspace] .

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo capacitado. Si no dispone de un modelo capacitado, siga el [tren y evalúe un modelo en el tutorial de la interfaz de usuario](./train-evaluate-model-ui.md) antes de continuar.

## Crear una nueva carrera de puntuación

Se crea una ejecución de puntuación mediante configuraciones optimizadas a partir de una ejecución de formación previamente completada y evaluada. El conjunto de configuraciones óptimas para un modelo generalmente se determina mediante la revisión de las métricas de evaluación de la ejecución de formación.

1. Encuentre la ejecución de capacitación más óptima para utilizar sus configuraciones para la puntuación. Abra la ejecución de formación deseada haciendo clic en su nombre.

2. En la ficha **[!UICONTROL Evaluación]** de la ejecución de formación, haga clic en el botón **[!UICONTROL Puntuación]** en la parte superior derecha de la pantalla. Esto iniciará un nuevo flujo de trabajo de *Ejecutar puntuación* .
   ![](../images/models-recipes/score/training_run_overview.png)

3. Seleccione el conjunto de datos de puntuación de entrada y haga clic en **[!UICONTROL Siguiente]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Seleccione el conjunto de datos de puntuación de resultados, que es el conjunto de datos de salida dedicado donde se almacenan los resultados de puntuación. Confirme la selección y haga clic en **[!UICONTROL Siguiente]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. El paso final del flujo de trabajo le solicita que configure la ejecución de puntuación. El modelo utiliza estas configuraciones para la ejecución de puntuación.
Tenga en cuenta que no podrá eliminar los parámetros heredados que se establecieron durante la creación del modelo. Puede editar o revertir los parámetros no heredados haciendo clic en el valor o en el icono de revertir al pasar el ratón sobre la entrada.
   ![](../images/models-recipes/score/configuration.png)
Revise y confirme las configuraciones de puntuación y haga clic en **[!UICONTROL Finalizar]** para crear y ejecutar la ejecución de puntuación. Se le dirigirá a la ficha Ejecuciones **[!UICONTROL de]** puntuación y la nueva ejecución de puntuación mostrará un estado.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
Una ejecución de puntuación mostrará cualquiera de los cuatro estados siguientes: Pendiente, Completado, Fallido o En ejecución, y se actualizan automáticamente. Continúe con el paso siguiente si el estado es &quot;Completado&quot; o &quot;Fallido&quot;.

## Resultados de puntuación de vista

1. Busque la ejecución de formación que se utilizó para la ejecución de puntuación y haga clic en el nombre para vista de la página **[!UICONTROL Evaluación]** .

2. Cerca de la parte superior de la página de evaluación de la ejecución de formación, haga clic en la ficha Ejecuciones **[!UICONTROL de]** puntuación para vista de una lista de ejecuciones de puntuación existentes. Haga clic en el listado de puntuación para vista sus detalles en la columna derecha.
   ![](../images/models-recipes/score/view_details.png)

3. Si la ejecución de puntuación seleccionada tiene el estado &quot;Completado&quot; o &quot;Fallido&quot;, se activará el vínculo Registros **[!UICONTROL de Actividad de]** Vista que se encuentra en la columna de la derecha. Haga clic en el vínculo de vista o descargue los registros de ejecución. Si se ha producido un error en una ejecución de puntuación, los registros de ejecución pueden proporcionar información útil para determinar el motivo del error.
   ![](../images/models-recipes/score/activity_logs.png)

4. Haga clic en el vínculo **[!UICONTROL Resultados de puntuación de Previsualizaciones Conjunto de datos]** que se encuentra en la columna derecha. Podrá ver una previsualización del conjunto de datos de salida a partir de la ejecución de puntuación.
   ![](../images/models-recipes/score/preview_results.png)

5. Para obtener el conjunto completo de resultados de puntuación, haga clic en el vínculo Conjunto de datos de resultados de **[!UICONTROL puntuación]** que se encuentra en la columna derecha.

## Pasos siguientes

Este tutorial le guió por los pasos para realizar una puntuación de datos mediante un modelo entrenado en [!DNL Data Science Workspace]. Siga el tutorial sobre la [publicación de un modelo como servicio en la interfaz de usuario](./publish-model-service-ui.md) para permitir que los usuarios de la organización puedan puntuar datos, ya que proporciona un acceso sencillo a un servicio de aprendizaje automático.
