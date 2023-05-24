---
keywords: Experience Platform;puntuar un modelo;Data Science Workspace;temas populares;iu;ejecución de puntuación;resultados de puntuación
solution: Experience Platform
title: Puntuación de un modelo en la IU de Data Science Workspace
type: Tutorial
description: La puntuación en Adobe Experience Platform Data Science Workspace se puede lograr alimentando los datos de entrada en un modelo formado existente. A continuación, los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# Puntuación de un modelo en la IU de Data Science Workspace

Puntuación en Adobe Experience Platform [!DNL Data Science Workspace] se puede lograr introduciendo datos de entrada en un modelo entrenado existente. A continuación, los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.

Este tutorial muestra los pasos necesarios para puntuar un modelo en la [!DNL Data Science Workspace] interfaz de usuario.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo entrenado. Si no dispone de un modelo entrenado, siga las [Formación y evaluación de un modelo en la IU de](./train-evaluate-model-ui.md) tutorial antes de continuar.

## Crear una nueva ejecución de puntuación

Se crea una ejecución de puntuación utilizando configuraciones optimizadas de una ejecución de formación previamente completada y evaluada. El conjunto de configuraciones óptimas de un modelo se suele determinar revisando las métricas de evaluación de ejecución de formación.

Busque la ejecución de formación más óptima para utilizar sus configuraciones de puntuación. A continuación, abra la ejecución de formación deseada seleccionando el hipervínculo adjunto a su nombre.

![Seleccionar ejecución de formación](../images/models-recipes/score/select-run.png)

Desde la ejecución de formación **[!UICONTROL Evaluación]** pestaña, seleccione **[!UICONTROL Puntuación]** situado en la parte superior derecha de la pantalla. Comienza un nuevo flujo de trabajo de puntuación.

![](../images/models-recipes/score/training_run_overview.png)

Seleccione el conjunto de datos de puntuación de entrada y seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/score/scoring_input.png)

Seleccione el conjunto de datos de puntuación de salida, que es el conjunto de datos de salida dedicado donde se almacenan los resultados de puntuación. Confirme la selección y seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/score/scoring_results.png)

El último paso del flujo de trabajo le pedirá que configure la ejecución de puntuación. El modelo utiliza estas configuraciones para la ejecución de puntuación.
Tenga en cuenta que no puede quitar los parámetros heredados definidos durante la creación de los modelos. Puede editar o revertir parámetros no heredados haciendo doble clic en el valor o seleccionando el icono de revertir mientras pasa el ratón sobre la entrada.

![configuración](../images/models-recipes/score/configuration.png)

Revise y confirme las configuraciones de puntuación y seleccione **[!UICONTROL Finalizar]**  para crear y ejecutar la ejecución de puntuación. Se le dirigirá al **[!UICONTROL Ejecuciones de puntuación]** y la nueva ejecución de puntuación con **[!UICONTROL Pendiente]** se muestra el estado.

![pestaña ejecuciones de puntuación](../images/models-recipes/score/scoring_runs_tab.png)

Una ejecución de puntuación se puede mostrar con uno de los siguientes estados:
- Pendiente
- Completar
- Fallido
- Ejecutando

Los estados se actualizan automáticamente. Continúe con el paso siguiente si el estado es **[!UICONTROL Completar]** o **[!UICONTROL Error]**.

## Ver resultados de puntuación

Para ver los resultados de la puntuación, comience seleccionando una ejecución de formación.

![Seleccionar ejecución de formación](../images/models-recipes/score/select-run.png)

Se le redirigirá a las ejecuciones de formación. **[!UICONTROL Evaluación]** página. Cerca de la parte superior de la página de evaluación de la ejecución de formación, seleccione la opción **[!UICONTROL Ejecuciones de puntuación]** para ver una lista de las ejecuciones de puntuación existentes.

![página de evaluación](../images/models-recipes/score/view_scoring_runs.png)

A continuación, seleccione una ejecución de puntuación para ver los detalles de la ejecución.

![ejecutar detalles](../images/models-recipes/score/view_details.png)

Si la ejecución de puntuación seleccionada tiene el estado &quot;Completada&quot; o &quot;Fallido&quot;, la variable **[!UICONTROL Ver registros de actividades]** Este vínculo ya está disponible. Si falla una ejecución de puntuación, los registros de ejecución pueden proporcionar información útil para determinar el motivo del error. Para descargar los registros de ejecución, seleccione **[!UICONTROL Ver registros de actividades]**.

![Seleccionar registros de vista](../images/models-recipes/score/view_logs.png)

El **[!UICONTROL Ver registros de actividad]** aparece la ventana emergente. Seleccione una URL para descargar automáticamente los registros asociados.

![](../images/models-recipes/score/activity_logs.png)

También tiene la opción de ver los resultados de puntuación seleccionando  **[!UICONTROL Previsualizar conjunto de datos de resultados de puntuación]**.

![Seleccionar previsualización de resultados](../images/models-recipes/score/view_results.png)

Se proporciona una previsualización del conjunto de datos de salida.

![previsualizar resultados](../images/models-recipes/score/preview_results.png)

Para obtener el conjunto completo de resultados de puntuación, seleccione la **[!UICONTROL Conjunto de datos de resultados]** vínculo encontrado en la columna derecha.

## Pasos siguientes

En este tutorial, se explican los pasos para puntuar los datos mediante un modelo entrenado en [!DNL Data Science Workspace]. Siga el tutorial de [Publicación de un modelo como servicio en la IU](./publish-model-service-ui.md) para permitir que los usuarios de su organización puntúen los datos mediante un acceso fácil a un servicio de aprendizaje automático.
