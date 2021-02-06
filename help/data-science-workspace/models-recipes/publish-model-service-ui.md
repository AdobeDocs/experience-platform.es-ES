---
keywords: Experience Platform;publicar un modelo;Área de trabajo de ciencia de datos;temas populares;marcar un servicio
solution: Experience Platform
title: Publicación de un modelo como servicio en la interfaz de usuario de Área de trabajo de ciencia de datos
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace le permite publicar el modelo evaluado y capacitado como un servicio, lo que permite a los usuarios de la organización de IMS puntuar datos sin necesidad de crear sus propios modelos.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# Publicación de un modelo como servicio en la interfaz de usuario de Área de trabajo de ciencia de datos

Adobe Experience Platform Data Science Workspace le permite publicar el modelo evaluado y capacitado como un servicio, lo que permite a los usuarios de la organización de IMS puntuar datos sin necesidad de crear sus propios modelos.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo existente con una ejecución de formación correcta. Si no tiene un modelo editable, siga el tutorial [Train y evalúe un modelo en la IU](./train-evaluate-model-ui.md) antes de continuar.

Si prefiere publicar un modelo mediante las API de aprendizaje automático de Sensei, consulte el [tutorial de API](./publish-model-service-api.md).

## Publicar un modelo {#publish-a-model}

1. En Adobe Experience Platform, haga clic en el vínculo **[!UICONTROL Modelos]** ubicado en la columna de navegación izquierda para lista de todos los modelos existentes. Busque y haga clic en el nombre del modelo que se va a publicar como servicio.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Haga clic en **[!UICONTROL Publicar]** cerca de la parte superior derecha de la página de información general del modelo para inicio de un proceso de creación de servicios.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Escriba un nombre que desee para el Servicio y, si lo desea, proporcione una descripción del Servicio, haga clic en **[!UICONTROL Siguiente]** cuando finalice.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Se muestran todas las ejecuciones de formación correctas para el modelo. El nuevo servicio heredará las configuraciones de capacitación y puntuación de la ejecución de formación seleccionada.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Haga clic en **[!UICONTROL Finalizar]** para crear el Servicio y redirigir a la **[!UICONTROL Galería de servicios]** para mostrar todos los Servicios disponibles, incluido el Servicio recién creado.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Puntuación mediante un servicio {#access-a-service}

1. En Adobe Experience Platform, haga clic en la ficha **[!UICONTROL Servicios]** ubicada en la columna de navegación izquierda para acceder a la **[!UICONTROL Galería de servicios]**. Busque el servicio que desee utilizar y haga clic en **[!UICONTROL Puntuación]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Seleccione un conjunto de datos de entrada adecuado para la ejecución de puntuación y haga clic en **[!UICONTROL Siguiente]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Seleccione un conjunto de datos de salida adecuado para los resultados de puntuación y haga clic en **[!UICONTROL Siguiente]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Cuando se crea un servicio, hereda las configuraciones de puntuación predeterminadas. Puede revisar estas configuraciones y ajustarlas según sea necesario haciendo clic con el doble en los valores. Una vez que esté satisfecho con las configuraciones, haga clic en **[!UICONTROL Finalizar]** para comenzar la ejecución de la puntuación.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. En la página **Información general** del servicio, se muestran detalles del nuevo trabajo de puntuación y su progreso. Una vez finalizado el trabajo, se actualizará el encabezado **[!UICONTROL Más reciente]** dentro del contenedor **[!UICONTROL Puntuación]**.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Pasos siguientes {#next-steps}

Siguiendo este tutorial, ha publicado correctamente un modelo como un servicio accesible y puntuado los datos mediante el nuevo servicio a través de la [!UICONTROL Galería de servicios]. Continúe con el siguiente tutorial para conocer cómo puede [programar ejecuciones de puntuación y capacitación automatizadas en un servicio](./schedule-models-ui.md).
