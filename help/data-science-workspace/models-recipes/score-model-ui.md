---
keywords: Experience Platform;puntuación de modelo;Data Science Workspace;temas populares;iu;ejecución de puntuación;resultados de puntuación
solution: Experience Platform
title: Puntuación de un modelo en la interfaz de usuario de Data Science Workspace
type: Tutorial
description: La puntuación en Adobe Experience Platform Data Science Workspace se puede lograr añadiendo datos de entrada a un modelo entrenado existente. Los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# Puntuación de un modelo en la interfaz de usuario de Data Science Workspace

Puntuación en Adobe Experience Platform [!DNL Data Science Workspace] se puede lograr añadiendo datos de entrada a un modelo entrenado existente. Los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.

Este tutorial muestra los pasos necesarios para marcar un modelo en la variable [!DNL Data Science Workspace] interfaz de usuario.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo entrenado. Si no tiene un modelo entrenado, siga la [entrenar y evaluar un modelo en la interfaz de usuario](./train-evaluate-model-ui.md) antes de continuar.

## Crear una nueva ejecución de puntuación

Se crea una ejecución de puntuación mediante configuraciones optimizadas a partir de una ejecución de formación evaluada y completada anteriormente. El conjunto de configuraciones óptimas para un modelo se suelen determinar revisando las métricas de evaluación de ejecución de capacitación.

Encuentre la ejecución de capacitación más óptima para utilizar sus configuraciones para la puntuación. A continuación, abra la formación deseada seleccionando el hipervínculo adjunto a su nombre.

![Seleccionar ejecución de formación](../images/models-recipes/score/select-run.png)

Desde la ejecución de la formación **[!UICONTROL Evaluación]** , seleccione **[!UICONTROL Puntuación]** situado en la parte superior derecha de la pantalla. Se inicia un nuevo flujo de trabajo de puntuación.

![](../images/models-recipes/score/training_run_overview.png)

Seleccione el conjunto de datos de puntuación de entrada y seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/score/scoring_input.png)

Seleccione el conjunto de datos de puntuación de salida, que es el conjunto de datos de salida dedicado donde se almacenan los resultados de puntuación. Confirme la selección y seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/score/scoring_results.png)

El último paso del flujo de trabajo le solicita que configure su ejecución de puntuación. El modelo utiliza estas configuraciones para la ejecución de puntuación.
Tenga en cuenta que no puede quitar los parámetros heredados que se establecieron durante la creación de los modelos. Puede editar o revertir parámetros no heredados haciendo doble clic en el valor o seleccionando el icono revertir al pasar el ratón por encima de la entrada.

![configuración](../images/models-recipes/score/configuration.png)

Revise y confirme las configuraciones de puntuación y seleccione **[!UICONTROL Finalizar]**  para crear y ejecutar la ejecución de puntuación. Se le redirige a la función **[!UICONTROL Ejecuciones de puntuación]** y la nueva puntuación se ejecutará con la **[!UICONTROL Pendiente]** se muestra.

![ficha ejecución de puntuación](../images/models-recipes/score/scoring_runs_tab.png)

Se puede mostrar una ejecución de puntuación con uno de los siguientes estados:
- Pendiente
- Completar
- Fallido
- Ejecución

Los estados se actualizan automáticamente. Continúe con el paso siguiente si el estado es **[!UICONTROL Completar]** o **[!UICONTROL Error]**.

## Ver resultados de puntuación

Para ver los resultados de puntuación, comience por seleccionar una ejecución de formación.

![Seleccionar ejecución de formación](../images/models-recipes/score/select-run.png)

Se le redirige a las ejecuciones de formación **[!UICONTROL Evaluación]** página. Cerca de la parte superior de la página de evaluación de la ejecución de formación, seleccione la opción **[!UICONTROL Ejecuciones de puntuación]** para ver una lista de las ejecuciones de puntuación existentes.

![página de evaluación](../images/models-recipes/score/view_scoring_runs.png)

A continuación, seleccione una ejecución de puntuación para ver los detalles de ejecución.

![ejecutar detalles](../images/models-recipes/score/view_details.png)

Si la ejecución de puntuación seleccionada tiene el estado &quot;Completado&quot; o &quot;Fallido&quot;, la variable **[!UICONTROL Ver registros de actividades]** está disponible. Si falla una ejecución de puntuación, los registros de ejecución pueden proporcionar información útil para determinar el motivo del error. Para descargar los registros de ejecución, seleccione **[!UICONTROL Ver registros de actividades]**.

![Seleccionar registros de vista](../images/models-recipes/score/view_logs.png)

La variable **[!UICONTROL Ver registros de actividades]** se abre. Seleccione una URL para descargar automáticamente los registros asociados.

![](../images/models-recipes/score/activity_logs.png)

También tiene la opción de ver los resultados de puntuación seleccionando  **[!UICONTROL Vista previa del conjunto de datos de resultados de puntuación]**.

![Seleccionar resultados de vista previa](../images/models-recipes/score/view_results.png)

Se proporciona una vista previa del conjunto de datos de salida.

![resultados de vista previa](../images/models-recipes/score/preview_results.png)

Para el conjunto completo de resultados de puntuación, seleccione la opción **[!UICONTROL Conjunto de datos de resultados de puntuación]** vínculo encontrado en la columna derecha.

## Pasos siguientes

Este tutorial le guía por los pasos para puntuar datos mediante un modelo entrenado en [!DNL Data Science Workspace]. Siga el tutorial en [publicación de un modelo como servicio en la interfaz de usuario](./publish-model-service-ui.md) para permitir a los usuarios de su organización puntuar datos al proporcionar acceso fácil a un servicio de aprendizaje automático.
