---
keywords: Experience Platform;publicar un modelo;Data Science Workspace;temas populares;puntuación de un servicio
solution: Experience Platform
title: Publicación de un modelo como servicio en la interfaz de usuario de Data Science Workspace
type: Tutorial
description: Adobe Experience Platform Data Science Workspace permite publicar el modelo entrenado y evaluado como servicio, lo que permite a los usuarios de la organización IMS puntuar datos sin necesidad de crear sus propios modelos.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Publicación de un modelo como servicio en la interfaz de usuario de Data Science Workspace

Adobe Experience Platform Data Science Workspace permite publicar el modelo entrenado y evaluado como servicio, lo que permite a los usuarios de la organización IMS puntuar datos sin necesidad de crear sus propios modelos.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo existente con una ejecución de formación correcta. Si no tiene un modelo editable, siga la [Capacitar y evaluar un modelo en la interfaz de usuario](./train-evaluate-model-ui.md) antes de continuar.

Si prefiere publicar un modelo utilizando las API de aprendizaje automático de Sensei, consulte la [Tutorial de API](./publish-model-service-api.md).

## Publicación de un modelo {#publish-a-model}

En Adobe Experience Platform, seleccione **[!UICONTROL Modelos]** situado en la columna de navegación izquierda, seleccione la opción **[!UICONTROL Examinar]** para enumerar todos los modelos existentes. Seleccione el nombre del Modelo que desea publicar como Servicio.

![](../images/models-recipes/publish-model/browse_model.png)

Select **[!UICONTROL Publicación]** cerca de la parte superior derecha de la página de información general del modelo para iniciar un proceso de creación del servicio.

![](../images/models-recipes/publish-model/view_training.png)

Introduzca un nombre deseado para el Servicio y, opcionalmente, proporcione una descripción del Servicio, seleccione **[!UICONTROL Siguiente]** cuando termine.

![](../images/models-recipes/publish-model/configure_training.png)

Se muestran todas las ejecuciones de formación correctas para hasta el modelo. El nuevo Servicio heredará las configuraciones de capacitación y puntuación de la ejecución de capacitación seleccionada.

![](../images/models-recipes/publish-model/select_training_run.png)

Select **[!UICONTROL Finalizar]** para crear el servicio y redirigir al **[!UICONTROL Galería de servicios]** para mostrar todos los Servicios disponibles, incluido el Servicio recién creado.

![](../images/models-recipes/publish-model/service_gallery.png)

## Puntuación mediante un servicio {#access-a-service}

En Adobe Experience Platform, seleccione la opción **[!UICONTROL Servicios]** situado en la columna de navegación izquierda para acceder a la **[!UICONTROL Galería de servicios]**. Busque el servicio que desea utilizar y seleccione **[!UICONTROL Apertura]**.

![](../images/models-recipes/publish-model/open_service.png)

En la página de información general del servicio, seleccione **[!UICONTROL Puntuación]**.

![](../images/models-recipes/publish-model/score_service.png)

Seleccione un conjunto de datos de entrada adecuado para la ejecución de puntuación y, a continuación, seleccione **[!UICONTROL Siguiente]**. Se le pedirá que realice el mismo paso para el conjunto de datos de puntuación. Una vez que haya seleccionado el conjunto de datos de entrada y salida, puede actualizar las configuraciones.

![](../images/models-recipes/publish-model/select_datasets.png)

Cuando se crea un servicio, hereda las configuraciones de puntuación predeterminadas. Puede revisar estas configuraciones y ajustarlas según sea necesario haciendo doble clic en los valores. Una vez que esté satisfecho con las configuraciones, seleccione **[!UICONTROL Finalizar]** para comenzar la carrera de puntuación.

![](../images/models-recipes/publish-model/scoring_configs.png)

En el **Información general** , se muestran los detalles del nuevo trabajo de puntuación y su progreso. Una vez finalizado el trabajo, la variable **[!UICONTROL Más reciente]** dentro del **[!UICONTROL Puntuación]** se actualiza.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha publicado correctamente un Modelo como Servicio accesible y ha marcado los datos utilizando el nuevo Servicio a través del [!UICONTROL Galería de servicios]. Continúe con el siguiente tutorial para aprender cómo puede [programar la ejecución automatizada de la formación y la puntuación en un servicio](./schedule-models-ui.md).
