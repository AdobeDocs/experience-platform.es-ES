---
keywords: Experience Platform;puntuar un modelo;Workspace de ciencia de datos;temas populares;iu;ejecución de puntuación;resultados de puntuación
solution: Experience Platform
title: Puntuación de un modelo en la IU de Workspace de ciencia de datos
type: Tutorial
description: La puntuación en Adobe Experience Platform Data Science Workspace se puede lograr alimentando los datos de entrada en un modelo entrenado existente. A continuación, los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# Puntuación de un modelo en la IU de Workspace de ciencia de datos

La puntuación en Adobe Experience Platform [!DNL Data Science Workspace] se puede lograr suministrando datos de entrada a un modelo entrenado existente. A continuación, los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.

Este tutorial muestra los pasos necesarios para puntuar un modelo en la interfaz de usuario [!DNL Data Science Workspace].

## Introducción

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo entrenado. Si no tiene un modelo entrenado, siga el [curso de formación y evalúe un modelo en el tutorial de la interfaz de usuario](./train-evaluate-model-ui.md) antes de continuar.

## Crear una nueva ejecución de puntuación

Se crea una ejecución de puntuación utilizando configuraciones optimizadas de una ejecución de formación previamente completada y evaluada. El conjunto de configuraciones óptimas de un modelo se suele determinar revisando las métricas de evaluación de ejecución de formación.

Busque la ejecución de formación más óptima para utilizar sus configuraciones de puntuación. A continuación, abra la ejecución de formación deseada seleccionando el hipervínculo adjunto a su nombre.

![Seleccionar ejecución de formación](../images/models-recipes/score/select-run.png)

En la ficha **[!UICONTROL Evaluación]** de la ejecución de formación, seleccione **[!UICONTROL Puntuación]** en la parte superior derecha de la pantalla. Comienza un nuevo flujo de trabajo de puntuación.

![](../images/models-recipes/score/training_run_overview.png)

Seleccione el conjunto de datos de puntuación de entrada y seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/score/scoring_input.png)

Seleccione el conjunto de datos de puntuación de salida, que es el conjunto de datos de salida dedicado donde se almacenan los resultados de puntuación. Confirme su selección y seleccione **[!UICONTROL Siguiente]**.

![](../images/models-recipes/score/scoring_results.png)

El último paso del flujo de trabajo le pedirá que configure la ejecución de puntuación. El modelo utiliza estas configuraciones para la ejecución de puntuación.
Tenga en cuenta que no puede quitar los parámetros heredados definidos durante la creación de los modelos. Puede editar o revertir parámetros no heredados haciendo doble clic en el valor o seleccionando el icono de revertir mientras pasa el ratón sobre la entrada.

![configuración](../images/models-recipes/score/configuration.png)

Revise y confirme las configuraciones de puntuación y seleccione **[!UICONTROL Finalizar]** para crear y ejecutar la ejecución de puntuación. Se le dirigirá a la ficha **[!UICONTROL Ejecuciones de puntuación]** y se mostrará la nueva ejecución de puntuación con el estado **[!UICONTROL Pendiente]**.

![ficha ejecuciones de puntuación](../images/models-recipes/score/scoring_runs_tab.png)

Una ejecución de puntuación se puede mostrar con uno de los siguientes estados:
- Pendiente
- Completar
- Error
- Ejecutando

Los estados se actualizan automáticamente. Continúe con el paso siguiente si el estado es **[!UICONTROL Completado]** o **[!UICONTROL Error]**.

## Ver resultados de puntuación

Para ver los resultados de la puntuación, comience seleccionando una ejecución de formación.

![Seleccionar ejecución de formación](../images/models-recipes/score/select-run.png)

Se le redirigirá a la página **[!UICONTROL Evaluación]** de ejecuciones de formación. Cerca de la parte superior de la página de evaluación de la ejecución de formación, seleccione la ficha **[!UICONTROL Ejecuciones de puntuación]** para ver una lista de las ejecuciones de puntuación existentes.

![página de evaluación](../images/models-recipes/score/view_scoring_runs.png)

A continuación, seleccione una ejecución de puntuación para ver los detalles de la ejecución.

![ejecutar detalles](../images/models-recipes/score/view_details.png)

Si la ejecución de puntuación seleccionada tiene el estado &quot;Completada&quot; o &quot;Fallida&quot;, está disponible el vínculo **[!UICONTROL Ver registros de actividad]**. Si falla una ejecución de puntuación, los registros de ejecución pueden proporcionar información útil para determinar el motivo del error. Para descargar los registros de ejecución, seleccione **[!UICONTROL Ver registros de actividad]**.

![Seleccionar registros de vista](../images/models-recipes/score/view_logs.png)

Aparece la ventana emergente **[!UICONTROL Ver registros de actividad]**. Seleccione una URL para descargar automáticamente los registros asociados.

![](../images/models-recipes/score/activity_logs.png)

También tiene la opción de ver los resultados de puntuación seleccionando **[!UICONTROL Vista previa del conjunto de datos de resultados de puntuación]**.

![Seleccionar resultados de vista previa](../images/models-recipes/score/view_results.png)

Se proporciona una previsualización del conjunto de datos de salida.

![resultados de vista previa](../images/models-recipes/score/preview_results.png)

Para obtener el conjunto completo de resultados de puntuación, seleccione el vínculo **[!UICONTROL Conjunto de datos de resultados de puntuación]** que se encuentra en la columna derecha.

## Pasos siguientes

Este tutorial lo guió para puntuar los datos mediante un modelo entrenado en [!DNL Data Science Workspace]. Siga el tutorial de [publicación de un modelo como servicio en la interfaz de usuario](./publish-model-service-ui.md) para permitir que los usuarios de su organización puntúen los datos proporcionando un acceso fácil a un servicio de aprendizaje automático.
